# الأحداث (Events)

هذه أمثلة لأحداث يمكن أن تطلقها خدمة OTP لدعم التكامل مع خدمات أخرى (بنمط Event-Driven).

## أمثلة أحداث

- `otp.requested`: تم إنشاء OTP وطلب إرساله.
- `otp.sent`: تم إرسال OTP عبر القناة.
- `otp.verify_succeeded`: تحقق الرمز بنجاح.
- `otp.verify_failed`: فشل تحقق الرمز (مع سبب عام).
- `otp.consumed`: تم استهلاك الرمز ومنع إعادة استخدامه.
- `otp.rate_limited`: تم منع الطلب بسبب حد الطلبات.

## حمولة الحدث (Payload) - حقول مقترحة

- `purpose`
- `channel`
- `destination_masked` (قيمة مُخفاة)
- `request_id` / `otp_id`
- `created_at`

