# NAMING_AND_CONTRACTS_STANDARD.md — معيار العقود والتسمية (طبقة contracts/)

```contract
id: contracts.standard
version: 1.0
status: Proposed
owner: Specification Architect (SA-delegated)
since: 2026-07-19 (G1)
relates: ADR-0035 · ui/UI_FIELD_NAMING.md · AUTHORITY.md (المرتبة 5)
```

> **Purpose:** يعرّف شكلَ العقد ودورةَ حياته وبنيةَ طبقة `contracts/`، ويثبّت مرجعية التسمية القائمة **دون تكرارها** (‏EC-11: صفر ازدواج).

## §1 مرجعية التسمية — إحالة ملزمة لا نسخ
**المصدر الكنسي الوحيد لأنظمة المعرفات هو `ui/UI_FIELD_NAMING.md` §1–§3**: الأنواع الثمانية (screen_id · route · action_id · permission · api_operation · audit_event · field_name · component_name) بأنماطها ونطاقات تفردها وأمثلتها، والفصل الحاسم action_id ≠ endpoint، وسلسلة الربط القياسية. أي عقد يخالفها مرفوض شكلاً. **الإضافات الثلاث فقط** (لم تكن مقننة):
| النوع | الاصطلاح | النمط | أمثلة |
|---|---|---|---|
| `domain_event` (أحداث النطاق التقنية — ‏SSE/تكاملات؛ **غير** أحداث التدقيق UPPER) | dot.notation صغير، فعل ماضٍ | `{domain}.{event}_{past}` | `record.created` · ‏`workflow.item_returned` · ‏`ingestion.job_failed` |
| مفاتيح i18n | dot.notation صغير ASCII، مسطّحة | `{screen_id}.{element}` · ‏`common.{term}` · ‏`enum.{enum_id}.{value}` · ‏`error.{code}` | `run.list.create_button` · ‏`common.save` · ‏`enum.risk_level.high` |
| قيم التعدادات | ‏snake_case صغيرة مفردة من **قاموس مركزي** | القيمة تُعرَّف مرة واحدة في `contracts/enums/ENUMS_DICTIONARY.md` وتُستهلك بالمعرف | `under_review` · ‏`top_secret` |

## §2 ترويسة العقد الآلية ودورة الحياة
كل ملف عقد يبدأ بكتلة ` ```contract ` بالحقول الستة: **id** (dot.notation فريد) · **version** (يرتفع عند أي تغيير كاسر؛ القديم يُوسم Deprecated بإحالة) · **status** · **owner** (دور لا اسم شخص) · **since** · **relates**.
**دورة الحياة:** ‏Draft → **Proposed** → **Approved** → Deprecated. مخرجات أي وكيل/أداة (بما فيها Rocket) تدخل **Proposed** حكماً (بذور هذه الدفعة الأربع = ‏**Candidate**، وهي Proposed اصطلاحاً مع وسم منشئها التجريبي)؛ **Approved حصراً بتوقيع SA أو بوابة FP معتمدة** — والعقد Approved يكتسب المرتبة 5 في `AUTHORITY.md`.

## §3 بنية الطبقة (تُنشأ المجلدات عند أول محتوى — لا مجلدات فارغة)
`identity/` (هوية السجل — الآن) · ‏`screens/` (قالب + عقد لكل شاشة تبعياً — 4 بذور الآن) · ‏`enums/` (القاموس المركزي — الآن) · لاحقاً مع حِزم الميزات: ‏`entities/` · ‏`fields/` · ‏`api/` · ‏`events/`. السجل المركزي للشاشات والمسارات يبقى `ui/UI_SCREEN_INVENTORY.md` (‏ADR-0035 بند 3) — عقود الشاشات تكوّد سلوكها ولا تنافس الجرد على المعرفات.

## §4 المشتقات والإقفال
قاعدة GENERATED وwrite-back وخط توليد الوثائق: **المرجع الوحيد ADR-0035 (البنود 4–6)** — لا تُكرَّر هنا. عقود هذه الطبقة نفسها **مصادر تأليف** يقرؤها المولد ولا يكتب فيها.

## §5 قرارات المالك (R1)
- **قرار مالك (R1، 2026-07-21):** عقود v1 **مدمجة داخل عقود الشاشات** مع فهرس موحد للأنواع؛ لا تُفكك لملفات مستقلة إلا عند حاجة فعلية في حزمة تطوير.
- **قيد تسمية قانوني (R1):** الوحدة المالكة = `owning_org_unit_id` حصراً في الوثائق الحية؛ وتعداد وراثة النطاق = `scope_inheritance` ‏(ADR-0037).

**Related:** `../ui/UI_FIELD_NAMING.md` · `../decisions/adr/ADR-0035-contracts-layer-single-source.md` · `../AUTHORITY.md` · `identity/RECORD_IDENTITY.md` · `screens/SCREEN_CONTRACT_TEMPLATE.md` · `enums/ENUMS_DICTIONARY.md`
