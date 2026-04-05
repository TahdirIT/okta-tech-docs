---
title: نموذج البيانات — ExamSubject
---

## الغرض
تعريف مادة اختبار مجدولة ضمن فترة يوم محددة، مع ربطها بالمستويات/الفصول المستهدفة.

## الحقول المقترحة
- id: مفتاح أساسي.
- exam_day_period_id: مرجع إلى `ExamDayPeriod`.
- subject_id: مرجع إلى `Subject` من منصة الأساس.
- notes: ملاحظات اختيارية.
- created_at, updated_at, deleted_at.

## العلاقات
- belongsTo ExamDayPeriod.
- belongsTo Subject.
- belongsToMany Section/Level/Class (حسب هيكلة المنصة) لربط من يختبر هذه المادة.

## الفهارس والقيود
- فهرس على (exam_day_period_id).
- قيد وجود `subject_id` صالح ومتوافق مع الدولة/المستوى عند اللزوم.

## ملاحظات أعمال
- تُرتّب المواد للطالب بحسب تاريخ اليوم والفترة الزمنية عند العرض.

