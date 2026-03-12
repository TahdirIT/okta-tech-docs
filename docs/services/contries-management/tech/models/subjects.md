# `subjects` (مُعاد تصميمه لخدمة إدارة الدول)

## الغرض

تعريف المواد الدراسية على مستوى الدولة، مع إمكانية ربطها بالمراحل/المستويات والفصل النشط.

## الأعمدة (مقترح Laravel 12 + PostgreSQL)

- **id**: `bigint` (PK)
- **country_id**: `bigint` (FK → `countries.id`)
- **term_id**: `bigint` nullable (FK → `terms.id`) — عند الحاجة لنسخ المواد حسب الفصل
- **slug**: `varchar` (مُعرّف ثابت للمادة)
- **name**: `jsonb`
- **short_name**: `jsonb` nullable
- **language**: `varchar` nullable
- **type**: `varchar` nullable (مثل: `core`, `elective`, `activity`)
- **category**: `varchar` nullable (مثل: علوم/رياضيات…)
- **max_score**: `numeric(6,2)` nullable
- **weekly_classes**: `int` default `0`
- **removable**: `boolean` default `false`
- **active**: `boolean` default `true`
- **parent_subject_id**: `bigint` nullable (FK → `subjects.id`) لتجميع مواد/نسخ
- **deleted_at**: `timestamptz` nullable
- **created_at / updated_at**: `timestamptz`

## العلاقات

- **belongsTo**: `countries`
- **belongsTo**: `terms` (اختياري)
- **belongsTo**: `subjects` (parent)
- (مقترح) **belongsToMany**: `education_levels` عبر pivot `subject_education_levels`
- (بديل) **belongsToMany**: `education_level_groups`

## الفهارس/القيود

- **unique**: (`country_id`, `term_id`, `slug`)
- **index**: (`country_id`)
- **index**: (`term_id`)
- **index**: (`parent_subject_id`)

## مقارنة مع `v5website`

في `v5website`:

- `subjects.term_id` إلزامي
- يوجد `group_level_id` و `school_id` (override) و `country_id`
- يوجد self-reference `subject_id`

المقترح هنا:

- جعل الموضوع “مرجعي” على مستوى الدولة، واعتبار `term_id` اختياريًا حسب الحاجة.
- ربط المواد بـ `education_levels`/`education_level_groups` بدل الاعتماد على `group_level` المدرسي.

