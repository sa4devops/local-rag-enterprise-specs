# github-docs-structure.md — هيكل مستودع الوثائق على GitHub

> **Version:** 1.7 (v1.0-baseline: ملفات ADR الفردية المزروعة تحت decisions/adr/؛ سبقه FIX-9 v0.8) · **Status:** Current / Accepted · **Date:** 2026-07-10  
> **Purpose:** الهيكل الرسمي لحزمة الوثائق على GitHub، متوافق مع **GitHub Spec Kit / Spacekit-compatible workflow** (`Vision → Specify → Clarify → Plan → Tasks → Implement` — وImplement ليس الآن)، وكيف يستخدمه أي AI Coding Agent.

## الشجرة النهائية

```text
local-rag-enterprise-specs/                                 # حزمة الوثائق الرسمية (الاسم الفعلي للمستودع)
  README.md                                                 # نقطة الدخول + ترتيب القراءة + Authority Order
  vision.md                                                 # رؤية المشروع
  constitution.md                                           # القواعد غير القابلة للتفاوض (المرتبة 1)
  PACKAGE_CHECKLIST.md                                      # خريطة الحزمة وحالة كل ملف
  github-docs-structure.md                                  # هذه الوثيقة
  EXECUTION_REPORT.md                                       # تقرير تنفيذ دفعة v0.8 (جرد/تدقيق/إصلاحات/بصمات)

  architecture/
    README.md                                               # فهرس وثائق المعمارية + خريطة الاستخراج
    diagrams/
      Full_Stack_Architecture.svg                           # المخطط المعتمد
    …-architecture.md                                       # لاحقاً: تُستخرج من الكتالوج عند الحاجة
    PROVIDER_MODEL_SECRET_CONFIG_SPEC.md                    # عقد المزوّد/السر بين Config/Ops والـ Backend والواجهة (D9/الخيار A)

  catalogs/
    Feature_Technical_Architecture_Catalog.md               # الكتالوج المعماري/الفني (المرتبة 3)
    …                                                       # لاحقاً/اختياري: كتالوجات فرعية إن لزم

  methodology/
    Spec_Driven_Modular_Monolith_Methodology.md             # المنهجية (المرتبة 2)
    coding-standards.md                                     # قواعد الكود والوكلاء
    testing-strategy.md                                     # استراتيجية الاختبار
    agent-execution-model.md                                # نموذج تشغيل الوكلاء: Clarify → Tasks → Execute → Handoff
    PRE_IMPLEMENTATION_CONSOLIDATION_REVIEW.md              # بوابة التجميع قبل التنفيذ وترتيب الدمج وتعليمات الوكلاء

  decisions/
    open-decisions.md                                       # Open Decisions (المرتبة 4) (+فهرس قرارات v0.8 المقفلة Δv0.8)
    license-review.md                                       # سجل مراجعة التراخيص وبوابات الاعتماد
    adr/
      README.md                                             # السجل الكنسي للـ ADRs (v1.2 — سياسة D15)
      ADR-XXXX-*.md                                         # ملفات فردية مزروعة (v1.0-baseline): 0004 · 0017–0022 (مزروعة) + 0023–0028 (جديدة)؛ البقية تُزرع عند الحاجة

  references/
    OSS_REFERENCE_CATALOG.md                                # كتالوج مشاريع OSS المسموح دراستها كمرجع فقط

  phases/
    README.md                                               # قواعد مجلد المراحل
    phase-roadmap.md                                        # خريطة المراحل (المرتبة 5)
    phase-0-foundation-full-stack-skeleton.md               # تصميم Phase 0 المعتمد
    PHASE_MASTER_PLAN.md                                    # خطة المراحل الكاملة المعتمدة في v0.3 — ⚠️ غير موجودة في الريبو حالياً (Finding F-3 في EXECUTION_REPORT v0.8)
    BACKLOG_DEFERRED_SCOPE.md                               # النطاق المؤجل/المستقبلي — ⚠️ غير موجود في الريبو حالياً (Finding F-3)
    designs/                                                # ⚠️ ملفات phase-1..8 أدناه مُحالة من v0.3 لكنها غير مرفوعة في الريبو (Finding F-3) — رفعها بقرار SA
      DELTA_V08_FR_WORKFLOW_ORG.md                          # (v0.8) نصوص FR-3.11/FR-3.12/FR-1.Org-Ext المعتمدة + OD-WF-1/2 وOD-ORG-1 — تُدمج في تصميمَي Phase 1/Phase 3 عند توفرهما
      phase-1-governed-core-screen-builder.md
      phase-2-advanced-screens-records-entity-profile.md
      phase-3-workflows-approvals-actions.md
      phase-4-advanced-permissions-feature-management.md
      phase-5-files-rag-ocr-media.md
      phase-6-gateway-agents-sql-chat-reports.md
      phase-7-integrations-app-store.md
      phase-8-monitoring-offline-production.md

  ui/                                                        # يضم حزم v0.4 + v0.5 + v0.6 (+Δ v0.7.1 responsive +Δ v0.8) — كل حزمة تُضاف فوق سابقتها دون استبدال
    # —— حزمة v0.4 (UI/UX Planning) ——
    UI_UX_ASSUMPTIONS.md                                    # فلسفة UI/UX وافتراضات Dual-Surface (+A-UX-15 Δv0.6 · A-UX-16 Δv0.7.1 · A-UX-17 Δv0.8)
    UI_SITEMAP.md                                           # خريطة واجهات النظام (+/me/runs Δv0.6)
    UI_SCREEN_INVENTORY.md                                  # جرد الشاشات والمعرّفات (v1.3: +retrieval_tester +runs.* +تحديثات v0.8)
    UI_AI_WORKSPACE_MODEL.md                                # نموذج Enterprise AI Workspace (+§14 وضعا العرض Δv0.8)
    UI_ACTION_BUTTON_MODEL.md                               # نموذج Action Button / Governed Action Contract (+6.c Δv0.6 · +§2.1 inline message action Δv0.8)
    UI_ADMIN_CONSOLE_MODEL.md                               # نموذج Admin Console / Control Plane (+ملاحظة F Δv0.6 · +OD-BLD-1 Δv0.8)
    UI_FIELD_NAMING.md                                      # قواعد تسمية screen/action/permission/field/audit/API (+run/escalate/compare Δv0.6 · +WORKFLOW_ITEM_RETURNED Δv0.8)
    UI_DESIGN_SYSTEM.md                                     # نظام التصميم المؤسسي العربي/الإنجليزي (+عائلة شارات النموذج Δv0.6 · +Responsive Δv0.7.1)
    UI_SCREEN_CARDS_BY_PHASE.md                             # ربط الشاشات بالمراحل (+صفا runs Δ ما-بعد الدمج)
    UI_STITCH_PROMPTS_BY_PHASE.md                           # مجموعات Google Stitch prompts G1–G13 (+تنبيه أسبقية النسخ المحسّنة)
    UI_REFERENCE_USAGE_POLICY.md                            # سياسة استخدام الصور والمراجع في التصميم (+صفّا PentAGI/RedAmon Δv0.6 · +مشاعية الأنماط المحادثية Δv0.8)
    UI_GATE_REVIEW_CHECKLIST.md                             # بوابة مراجعة حزمة UI/UX v0.4
    # —— حزمة v0.5 (Interaction & Visibility Refinement) —— (FIX-9)
    UI_INTERACTION_MODEL.md                                 # قاموس الأسطح الستة ومصفوفة الحسم (+صفوف runs Δv0.6)
    UI_VISIBILITY_RULES.md                                  # درجات الرؤية الأربع + وسوم الظهور الـ15 (+قاعدة D9 البنيوية Δv0.6)
    UI_PROGRESSIVE_DISCLOSURE.md                            # هرم الإظهار L0–L3 وقواعد مكافحة الازدحام
    UI_COMPONENT_STATES.md                                  # كتالوج الحالات الـ15 لكل مكوّن (+مكوّنات 14–17 Δv0.6)
    UI_SCREEN_BEHAVIOR_CARDS.md                             # بطاقات سلوك الشاشات (+بطاقات 20–23 Δv0.6 · +بطاقة 24 admin.org وتحديثات v0.8)
    UI_STITCH_REFINED_PROMPTS.md                            # الموجّهات المحسّنة G1/G3/G4/G5/G7/G9/G13 (+G14 Δv0.6)
    UI_REFINEMENT_GATE_REVIEW.md                            # بوابة قبول حزمة v0.5
    # —— حزمة v0.6 (Provider · Model · Run UX) —— (FIX-9)
    UI_PROVIDER_MODEL_MANAGEMENT.md                         # إدارة المزوّدات والنماذج (الخيار A — D9)
    UI_RUN_EXECUTION_MODEL.md                               # نموذج عرض التشغيل runs.list/runs.detail
    UI_V06_DELTA_AMENDMENTS.md                              # سجل Δ v0.6 للتتبع
    UI_V06_GATE_REVIEW.md                                   # بوابة قبول حزمة v0.6
    prototypes/                                             # لاحقاً: مخرجات Stitch/Figma كـ prototypes فقط
    design-notes/                                           # لاحقاً: ملاحظات التصميم والمراجع المستخدمة

  handoff/
    handoff.md                                              # سجل التسليم الحالي + H-0001..H-0009
    archive/                                                # لاحقاً: أرشيف نسخ handoff بتاريخها

  superseded/
    README.md                                               # فهرس الوثائق المتجاوزة + قاعدة الوسم
    …                                                       # لاحقاً: نقل الملفات القديمة إليه
