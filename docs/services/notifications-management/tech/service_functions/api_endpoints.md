# وظائف الخدمة: واجهات برمجية (APIs)

## تعريفات الإشعارات (منصة)
- POST /api/admin/notification-definitions
- GET /api/admin/notification-definitions
- GET /api/admin/notification-definitions/{key}
- PUT /api/admin/notification-definitions/{key}
- DELETE /api/admin/notification-definitions/{key}

## قوالب الإشعارات (منصة/جهة)
- POST /api/{scope}/notification-templates
- GET /api/{scope}/notification-templates
- PUT /api/{scope}/notification-templates/{id}
- DELETE /api/{scope}/notification-templates/{id}

حيث {scope} ∈ {admin, tenant}

## تفضيلات الإشعارات (مستخدم)
- GET /api/me/notification-preferences
- PUT /api/me/notification-preferences/{definition_key}/{channel}

## تشغيل إشعار
- POST /api/notifications/trigger
  - body: { definition_key, recipient, data, channels? }

