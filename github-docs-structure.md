# github-docs-structure.md — هيكل مستودع الوثائق على GitHub

> **Version:** 1.3 · **Status:** Current / Accepted · **Date:** 2026-07-07  
> **Purpose:** الهيكل الرسمي لحزمة الوثائق على GitHub، متوافق مع **GitHub Spec Kit / Spacekit-compatible workflow** (`Vision → Specify → Clarify → Plan → Tasks → Implement` — وImplement ليس الآن)، وكيف يستخدمه أي AI Coding Agent.

## الشجرة النهائية

```text
local-rag-enterprise-docs/                                  # حزمة الوثائق الرسمية
  README.md                                                 # نقطة الدخول + ترتيب القراءة + Authority Order
  vision.md                                                 # رؤية المشروع
  constitution.md                                           # القواعد غير القابلة للتفاوض (المرتبة 1)
  PACKAGE_CHECKLIST.md                                      # خريطة الحزمة وحالة كل ملف
  github-docs-structure.md                                  # هذه الوثيقة

  architecture/
    README.md                                               # فهرس وثائق المعمارية + خريطة الاستخراج
    diagrams/
      Full_Stack_Architecture.svg                           # المخطط المعتمد
    …-architecture.md                                       # لاحقاً: تُستخرج من الكتالوج عند الحاجة

  catalogs/
    Feature_Technical_Architecture_Catalog.md               # الكتالوج المعماري/الفني (المرتبة 3)
    …                                                       # لاحقاً/اختياري: كتالوجات فرعية إن لزم

  methodology/
    Spec_Driven_Modular_Monolith_Methodology.md             # المنهجية (المرتبة 2)
    coding-standards.md                                     # قواعد الكود والوكلاء
    testing-strategy.md                                     # استراتيجية الاختبار
    agent-execution-model.md                                # نموذج تشغيل الوكلاء: Clarify → Tasks → Execute → Handoff

  decisions/
    open-decisions.md                                       # Open Decisions (المرتبة 4)
    license-review.md                                       # سجل مراجعة التراخيص وبوابات الاعتماد
    adr/
      README.md                                             # السجل الكنسي للـ ADRs
      ADR-XXXX-*.md                                         # لاحقاً: ملف لكل قرار عند الحاجة

  references/
    OSS_REFERENCE_CATALOG.md                                # كتالوج مشاريع OSS المسموح دراستها كمرجع فقط

  phases/
    README.md                                               # قواعد مجلد المراحل
    phase-roadmap.md                                        # خريطة المراحل (المرتبة 5)
    phase-0-foundation-full-stack-skeleton.md               # تصميم Phase 0 المعتمد
    PHASE_MASTER_PLAN.md                                    # خطة المراحل الكاملة المعتمدة في v0.3
    BACKLOG_DEFERRED_SCOPE.md                               # النطاق المؤجل/المستقبلي
    designs/
      phase-1-governed-core-screen-builder.md
      phase-2-advanced-screens-records-entity-profile.md
      phase-3-workflows-approvals-actions.md
      phase-4-advanced-permissions-feature-management.md
      phase-5-files-rag-ocr-media.md
      phase-6-gateway-agents-sql-chat-reports.md
      phase-7-integrations-app-store.md
      phase-8-monitoring-offline-production.md

  ui/
    UI_UX_ASSUMPTIONS.md                                    # فلسفة UI/UX وافتراضات Dual-Surface
    UI_SITEMAP.md                                           # خريطة واجهات النظام
    UI_SCREEN_INVENTORY.md                                  # جرد الشاشات والمعرّفات
    UI_AI_WORKSPACE_MODEL.md                                # نموذج Enterprise AI Workspace
    UI_ACTION_BUTTON_MODEL.md                               # نموذج Action Button / Governed Action Contract
    UI_ADMIN_CONSOLE_MODEL.md                               # نموذج Admin Console / Control Plane
    UI_FIELD_NAMING.md                                      # قواعد تسمية screen/action/permission/field/audit/API
    UI_DESIGN_SYSTEM.md                                     # نظام التصميم المؤسسي العربي/الإنجليزي
    UI_SCREEN_CARDS_BY_PHASE.md                             # ربط الشاشات بالمراحل
    UI_STITCH_PROMPTS_BY_PHASE.md                           # مجموعات Google Stitch prompts G1–G13
    UI_REFERENCE_USAGE_POLICY.md                            # سياسة استخدام الصور والمراجع في التصميم
    UI_GATE_REVIEW_CHECKLIST.md                             # بوابة مراجعة حزمة UI/UX
    prototypes/                                             # لاحقاً: مخرجات Stitch/Figma كـ prototypes فقط
    design-notes/                                           # لاحقاً: ملاحظات التصميم والمراجع المستخدمة

  handoff/
    handoff.md                                              # سجل التسليم الحالي + H-0001..H-0004
    archive/                                                # لاحقاً: أرشيف نسخ handoff بتاريخها

  superseded/
    README.md                                               # فهرس الوثائق المتجاوزة + قاعدة الوسم
    …                                                       # لاحقاً: نقل الملفات القديمة إليه
