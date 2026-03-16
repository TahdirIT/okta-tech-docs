# الوسائط (Middleware)

## نظرة عامة

يستخدم النظام عدة Middleware لإدارة السياق والتحقق من الصلاحيات. تعمل هذه Middleware معاً لضمان أن المستخدم لديه السياق الصحيح والصلاحيات المطلوبة للوصول إلى الصفحات المحددة.

## Middleware المتاحة

### 1. EnsureContext

**الغرض:** التحقق من وجود سياق نشط في الجلسة.

**السلوك:**
- يتحقق من وجود مفتاح `context` في الجلسة
- إذا لم يكن موجوداً، يتم إعادة التوجيه إلى صفحة اختيار السياق (`/auth/context`)
- يتم تنفيذه قبل الوصول إلى الصفحات المحمية

**الاستخدام:**
```php
Route::middleware(['auth', 'context'])->group(function () {
    // Routes that require context
});
```

### 2. EnsureActiveTenantContext

**الغرض:** التحقق من صحة سياق المستأجر النشط.

**السلوك:**
- يتحقق من وجود سياق نشط في الجلسة
- إذا كان السياق على مستوى النظام (`scope === 'system'`)، يتم التجاوز (pass through)
- إذا كان السياق على مستوى المستأجر:
  - يتحقق من وجود `tenant_id` و `tenant_user_id` في السياق
  - يتحقق من أن المستأجر موجود ونشط وغير محذوف
  - يتحقق من أن رابط المستأجر-المستخدم موجود وصالح
  - إذا فشل أي تحقق، يتم إرجاع خطأ 403

**الاستخدام:**
```php
Route::middleware(['auth', 'active-tenant-context'])->group(function () {
    // Routes that require active tenant context
});
```

### 3. EnsureActiveRoles

**الغرض:** التحقق من وجود أدوار نشطة في السياق.

**السلوك:**
- يتحقق من وجود أدوار نشطة في السياق (`role_ids` في الجلسة)
- إذا لم تكن هناك أدوار نشطة، يتم إعادة التوجيه إلى صفحة اختيار السياق
- يتم تنفيذه على الصفحات التي تتطلب أدواراً نشطة

**الاستخدام:**
```php
Route::middleware(['auth', 'active-roles'])->group(function () {
    // Routes that require active roles
});
```

### 4. CheckPermission

**الغرض:** التحقق من صلاحية محددة للمستخدم.

**السلوك:**
- يتحقق من وجود صلاحية محددة في الصلاحيات النشطة للمستخدم
- يتم التحقق من الصلاحيات المحفوظة في الجلسة (`permission_names`)
- إذا لم تكن الصلاحية موجودة، يتم إرجاع خطأ 403

**الاستخدام:**
```php
Route::middleware(['auth', 'permission:users.create'])->group(function () {
    // Routes that require 'users.create' permission
});
```

## Middleware لإدارة Teams (spatie/laravel-permission)

### SetPermissionsTeamId Middleware (مقترح)

**الغرض:** إدارة `team_id` في حزمة `spatie/laravel-permission` بناءً على سياق المستأجر.

**السلوك:**
- إذا كان السياق على مستوى المستأجر:
  - يتم استدعاء `setPermissionsTeamId($tenantId)` لتعيين معرف المستأجر كـ team_id
- إذا كان السياق على مستوى النظام:
  - يتم استدعاء `setPermissionsTeamId(null)` لإزالة team_id
- عند تغيير المستأجر:
  - يتم استدعاء `forgetCachedPermissions()` لمسح ذاكرة التخزين المؤقت

**التكامل مع EnsureActiveTenantContext:**

يمكن دمج هذا Middleware مع `EnsureActiveTenantContext` أو إنشاؤه كـ Middleware منفصل يتم تنفيذه قبل التحقق من الصلاحيات.

**مثال التطبيق:**
```php
public function handle(Request $request, Closure $next)
{
    $context = session('context');
    
    if ($context && $context['scope'] === 'tenant' && $context['tenant_id']) {
        // Set team ID for tenant context
        app(\Spatie\Permission\PermissionRegistrar::class)->setPermissionsTeamId($context['tenant_id']);
    } else {
        // Remove team ID for system context
        app(\Spatie\Permission\PermissionRegistrar::class)->setPermissionsTeamId(null);
    }
    
    // Check if tenant changed
    $previousTenantId = session('previous_tenant_id');
    if ($previousTenantId !== ($context['tenant_id'] ?? null)) {
        app(\Spatie\Permission\PermissionRegistrar::class)->forgetCachedPermissions();
        session(['previous_tenant_id' => $context['tenant_id'] ?? null]);
    }
    
    return $next($request);
}
```

## ترتيب تنفيذ Middleware

الترتيب الموصى به في `bootstrap/app.php`:

1. **SetLocale** - تعيين اللغة
2. **EnsureContext** - التحقق من وجود سياق
3. **SetPermissionsTeamId** (مقترح) - تعيين team_id بناءً على السياق
4. **EnsureActiveTenantContext** - التحقق من صحة سياق المستأجر
5. **EnsureActiveRoles** - التحقق من وجود أدوار نشطة
6. **CheckPermission** - التحقق من صلاحيات محددة

## التكامل مع spatie/laravel-permission

### تفعيل Teams Feature

لتفعيل ميزة Teams في حزمة `spatie/laravel-permission`:

1. تحديث `config/permission.php`:
```php
'teams' => true,
```

2. تحديث Middleware لتعيين `team_id` بناءً على سياق المستأجر

3. التأكد من أن Migrations تحتوي على `team_id` في الجداول المطلوبة

### مسح ذاكرة التخزين المؤقت

عند تغيير السياق (خاصة عند تغيير المستأجر)، يجب مسح ذاكرة التخزين المؤقت:

```php
app(\Spatie\Permission\PermissionRegistrar::class)->forgetCachedPermissions();
```

يتم استدعاء هذا عادة في:
- Middleware عند تغيير المستأجر
- ContextBuilder عند بناء السياق الجديد
- SelectTenantService عند اختيار مستأجر جديد
