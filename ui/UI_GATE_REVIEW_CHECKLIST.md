# UI_GATE_REVIEW_CHECKLIST.md — بوابة فحص حزمة UI/UX قبل الرفع

> **Version:** 1.0 — Proposed · **Date:** 2026-07-06 · **الموضع الهدف:** `ui/UI_GATE_REVIEW_CHECKLIST.md`
> **الغرض:** بوابة قبول **إلزامية** قبل رفع مجلد `ui/` إلى `local-rag-enterprise-specs` وقبل إصدار `v0.4-ui-ux-planning-package`.
> **المنفّذ:** المالك + مراجِع (يجوز فحص آلي مساعد للبنود القابلة للأتمتة). **قاعدة الحكم:** أي بند ❌ في الأقسام A–G **يمنع الرفع** حتى الإصلاح؛ القسم H إجراء الرفع نفسه ويُنفَّذ بعد Accept فقط. تُعاد هذه البوابة عند أي تعديل لاحق على ملفات `ui/` قبل أي إصدار جديد.

## A) الاكتمال (12 ملفاً + شرطان)
- [ ] `ui/UI_UX_ASSUMPTIONS.md`
- [ ] `ui/UI_SITEMAP.md`
- [ ] `ui/UI_SCREEN_INVENTORY.md`
- [ ] `ui/UI_AI_WORKSPACE_MODEL.md`
- [ ] `ui/UI_ACTION_BUTTON_MODEL.md`
- [ ] `ui/UI_ADMIN_CONSOLE_MODEL.md`
- [ ] `ui/UI_FIELD_NAMING.md`
- [ ] `ui/UI_DESIGN_SYSTEM.md`
- [ ] `ui/UI_SCREEN_CARDS_BY_PHASE.md`
- [ ] `ui/UI_STITCH_PROMPTS_BY_PHASE.md`
- [ ] `ui/UI_REFERENCE_USAGE_POLICY.md`
- [ ] `ui/UI_GATE_REVIEW_CHECKLIST.md` (هذا الملف)
- [ ] جرد الشاشات بإصدار **≥ v1.1** ويتضمن صفّي `admin.retrieval_tester` في الجدولين A وB
- [ ] سطر **«اعتماد المالك (2026-07-06)»** لنموذج Dual-Surface موجود في رأس UI_UX_ASSUMPTIONS

## B) النقاء (لا كود — لا أوامر — لا أسرار)
- [ ] لا توجد أسيجة كود (ثلاث علامات اقتباس مائلة متتالية) في أي ملف من الحزمة
- [ ] لا أسطر أوامر طرفية (أنماط مثل: $ · sudo · pip · npm · pnpm · docker · git · bash · curl · wget في بداية سطر)
- [ ] لا endpoints/secrets/tokens/مفاتيح في أي مثال
- [ ] أسماء الملفات والمسارات ASCII بالكامل (المادة 18)
- [ ] لا صور أو أصول منتجات خارجية مضمّنة داخل الحزمة

## C) الاتساق مع v0.3 (لا كسر للمعتمد)
- [ ] ترتيب المراحل P0→P8 كما في PHASE_MASTER_PLAN — بلا تعديل؛ ws من **P6** والبيت قبله **queue.tasks** ثم بوابة التنقّل قبل P3
- [ ] خط التنفيذ المحكوم محفوظ في كل المواضع: Proposal → Preview → Validation → Confirmation → Approval-عند-اللزوم → Execution → Audit (لا تنفيذ مباشراً من مخرَج نموذج)
- [ ] لا dependency/خط/أيقونات جديدة بلا مسار ترخيص (المذكور محصور بوابةً في OD-DS-2)
- [ ] كل screen_id في UI_SCREEN_CARDS_BY_PHASE موجود في الجرد (لا شاشة يتيمة)
- [ ] كل إحالات OD-* (UX/WS/AB/AC/NM/DS) تشير إلى بنود معرَّفة داخل الحزمة

## D) الفلسفة (الثوابت المنتَجية)
- [ ] **ليست chatbot:** الوضع الحتمي موصوف كاملاً (WORKSPACE §9) + الـ Renderer user-facing (A-UX-3) + خط S1–S9 حاضر
- [ ] **ليست low-code للمستخدم:** كل شاشات builder/metadata/config جمهورها admin في الجرد (لا استثناء)
- [ ] **Dual-Surface:** «نفس action_id على السطحين» منصوص في A-UX-1 وملاحظات الجرد وACTION_BUTTON §2
- [ ] **Action Layer واحد:** عقد الحقول الـ13+ كامل في ACTION_BUTTON §1 وترتيب التقييم خادمي §3
- [ ] عمودا permissions وaudit_events **غير فارغين** لكل صف جرد (أو «—» مبرَّرة لقراءةٍ بحتة)
- [ ] **RTL/Arabic-first:** A-UX-9 + DESIGN_SYSTEM §10 (العزل ثنائي الاتجاه) + بند RTL في كل مجموعة prompts

## E) اتساق التسمية (عيّنات ضد UI_FIELD_NAMING §1)
- [ ] فحص عيّنة ≥8 معرفات من الجرد: screen_id/route/action_id/permission تطابق أنماطها
- [ ] نص الفصل الحاسم **action_id ≠ API endpoint** موجود (FIELD_NAMING §2) وسلسلة الربط §3 سليمة
- [ ] كل audit_event في الحزمة UPPER_SNAKE_CASE؛ وكل field_name في الأمثلة snake_case
- [ ] لا فعل خارج كتالوج الأفعال المغلق (§5) في أي action_id

## F) موجّهات Stitch
- [ ] 13 مجموعة G1–G13 موجودة وتغطي: Design System · Auth · Work Queue · Renderer/G13 · Workspace · Action Cards · Console Shell · Users/Roles/Permissions · Metadata/Actions/Workflow · RAG/Knowledge/Retrieval-Tester · Providers/Models · Integrations/Store · Audit/Ops
- [ ] كل مجموعة تتضمن الحقول الإلزامية: الهدف · الشاشات · المكوّنات · الحالات · RTL/العربية-أولاً · لا-نسخ-منتجات · prototype-only
- [ ] الديباجة المشتركة §1 وترتيب التوليد §2 موجودان
- [ ] G3 موسومة صراحة «ليست chatbot» وG7 «ليست low-code للمستخدم النهائي»
- [ ] قاعدة **البيانات الوهمية فقط** للأداة الخارجية مذكورة في الديباجة وفي رأس الملف

## G) سياسة المراجع
- [ ] «إلهام فقط» + قائمة المنع (branding/logos/أيقونات/layout حرفي/نصوص/كود) — §1/§3
- [ ] قاعدة الأداة الخارجية والبيانات الوهمية كحادثة أمن عند الخرق — §4
- [ ] كود Stitch لا يدخل أياً من الريبوهات؛ الصور المصدَّرة إلى `ui/prototypes/` بمصدرها — §5
- [ ] design-notes إلزامية بحقولها ووجهتها `ui/design-notes/` — §6
- [ ] جدول المراجع (يجوز/يُمنع) حاضر ويشمل قيد Dify/NocoDB (صور فقط) — §7
- [ ] التنفيذ النهائي D1 + بوابة ترخيص لأي إضافة — §8

## H) خطة الرفع والإصدار (تُنفَّذ بعد Accept — بيد المالك حصراً)
- [ ] الوجهة: مجلد `ui/` في specs بالملفات الـ12 كما هي
- [ ] commits مقترحة: (1) `Add ui core docs` [الافتراضات+الخريطة+الجرد] · (2) `Add ui surface models` [Workspace+Actions+Console] · (3) `Add ui standards` [التسمية+نظام التصميم+بطاقات المراحل] · (4) `Add ui prompts, reference policy and gate checklist` · (5) `Update package checklist, docs structure and handoff for ui package`
- [ ] التحديثات الوصفية المرافقة (commit 5): `PACKAGE_CHECKLIST.md → v1.3` بصفوف ملفات ui الـ12 · `github-docs-structure.md` بإضافة `ui/` و`ui/prototypes/` و`ui/design-notes/` (وجهتين مستقبليتين) · `handoff/handoff.md` بإدخال **H-0004** (إنتاج حزمة UI/UX واعتمادها)
- [ ] إنشاء Release: **`v0.4-ui-ux-planning-package`** — Title: *UI/UX Planning Package v0.4* — **Pre-release** — الوصف: وثائق تخطيط واجهات (12 ملفاً) بنموذج Dual-Surface؛ بلا كود وبلا تنفيذ؛ بطاقات مهام الواجهات تُولَّد عند تفعيل مراحلها
- [ ] بعد الإصدار: تحديث `platform/docs/SPEC_SOURCE.md` إلى `v0.4-ui-ux-planning-package` **فقط** (المصدر الوحيد للرقم — لا تغيير آخر في platform ولا إصدار platform جديد)

## قرار البوابة
| النتيجة | ☐ Accept | ☐ Accept with minor edits | ☐ Reject |
|---|---|---|---|

| البند | الملف | الملاحظة | الإجراء المطلوب |
|---|---|---|---|
| | | | |

المراجِع: ____________ · التاريخ: ____________ · مرجع الجلسة/الفحص الآلي: ____________
