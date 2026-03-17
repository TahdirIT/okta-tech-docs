# معيار تنظيم Feature Services في Laravel (Feature Services Structure)

## الهدف

توحيد تنظيم وظائف الـ **Feature** داخل `app/Services` بحيث تكون:

- **قابلة للاكتشاف بسرعة** (واضح أين مكان أي وظيفة)
- **سهلة للصيانة والاختبار** (تجميع واضح حسب الـResource + Use-cases صغيرة)
- **قابلة للتوسع** بدون تضخم ملف Service واحد

---

## الهيكلة المعتمدة

يجب أن تكون كل Feature داخل مجلد مستقل، وداخلها يتم تجميع Use-cases حسب **Resource** (المورد/النطاق الفرعي) أولاً:

`app/Services/<Feature>/<Resource>/<Function>.php`

حيث:

- `<Feature>`: اسم الميزة/المجال (Domain/Bounded Context)
- `<Resource>`: اسم المورد/الجزء الذي تتمحور حوله العمليات (مثل: `Roles`, `Countries`, `Terms`, `EntityRegistrationCustomizations`)
- `<Function>.php`: ملف واحد لكل Use-case/عملية واضحة (CRUD أو عملية خاصة مثل Toggle/SetActive/Assign)

> الهدف من هذا التقسيم: المطور يصل بسرعة إلى العمليات المتعلقة بمورد محدد بدون التنقل بين مجلدات CRUD.

---

## قواعد التسمية (Naming)

- **Feature folder**:
  - PascalCase
  - مثال: `RoleBasedAccessControl`, `CountriesManagement`
- **Resource folder**:
  - PascalCase
  - اسم واضح ومتعارف عليه داخل الميزة
  - أمثلة: `Roles`, `Permissions`, `Countries`, `Regions`, `AcademicYears`, `Terms`, `WeekdaysSettings`
- **Function file**:
  - PascalCase
  - اسم يعكس Use-case محدد (فعل + مفعول/سياق)
  - أمثلة:
    - CRUD: `CreateRole.php`, `UpdatePermission.php`, `ListRoles.php`, `DeleteRole.php`
    - عمليات خاصة: `ToggleCountryActive.php`, `SetActiveTerm.php`, `AssignSubjectEducationLevels.php`

> ملاحظة: لا نستخدم `Service.php` عامة مثل `RoleService.php` التي تتضخم بمرور الوقت؛ الهدف هو ملفات صغيرة وواضحة لكل Use-case.

---

## أمثلة

### مثال: RBAC

- `app/Services/RoleBasedAccessControl/Roles/ListRoles.php`
- `app/Services/RoleBasedAccessControl/Roles/ShowRole.php`
- `app/Services/RoleBasedAccessControl/Roles/CreateRole.php`
- `app/Services/RoleBasedAccessControl/Roles/UpdateRole.php`
- `app/Services/RoleBasedAccessControl/Roles/DeleteRole.php`

### مثال: Countries Management

- `app/Services/CountriesManagement/Countries/ListCountries.php`
- `app/Services/CountriesManagement/Countries/UpdateCountry.php`
- `app/Services/CountriesManagement/Countries/ToggleCountryActive.php`
- `app/Services/CountriesManagement/Terms/SetActiveTerm.php`

---

## شكل الملف (Template)

يفضل أن يكون كل ملف **Class واحدة** مع `__invoke()` لتسهيل الحقن والاستخدام:

```php
<?php

namespace App\Services\RoleBasedAccessControl\Roles;

use App\Models\Role;

final class CreateRole
{
    public function __invoke(array $data): Role
    {
        // validate/authorize outside or via FormRequest/Policy حسب التصميم
        return Role::query()->create($data);
    }
}
```

---

## كيفية الاستخدام

### 1) استخدامه داخل Controller عن طريق Dependency Injection (المفضل)

```php
<?php

namespace App\Http\Controllers;

use App\Services\RoleBasedAccessControl\Roles\CreateRole;
use Illuminate\Http\Request;

final class RolesController
{
    public function store(Request $request, CreateRole $createRole)
    {
        $role = $createRole($request->all());

        return response()->json($role, 201);
    }
}
```

### 2) استخدامه عبر الـ Container (عند الحاجة)

```php
$role = app(\App\Services\RoleBasedAccessControl\Roles\CreateRole::class)($data);
```

### 3) مثال Route سريع

```php
use App\Http\Controllers\RolesController;
use Illuminate\Support\Facades\Route;

Route::post('/roles', [RolesController::class, 'store']);
```

### 4) مثال Test مختصر (Feature/Integration)

```php
public function test_can_create_role(): void
{
    $payload = ['name' => 'Admin'];

    $response = $this->postJson('/roles', $payload);

    $response->assertCreated();
}
```

---

## توصيات إضافية

- **Single responsibility**: كل Function class تمثل Use-case واحد فقط.
- **تحديد المدخلات/المخرجات**: استخدم DTOs عند الحاجة بدل `array` في الحالات المعقدة.
- **تجنب التنقل بين الطبقات**: Service لا تحتوي منطق HTTP (لا Request/Response)، وتترك ذلك للـ Controllers/Actions.

