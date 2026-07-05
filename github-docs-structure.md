# github-docs-structure.md — هيكل مستودع الوثائق على GitHub

> **Version:** 1.0 · **Status:** Current / Accepted · **Date:** 2026-07-02
> **Purpose:** الهيكل الرسمي لحزمة الوثائق على GitHub، متوافق مع **GitHub Spec Kit / Spacekit-compatible workflow** (`Vision → Specify → Clarify → Plan → Tasks → Implement` — وImplement ليس الآن)، وكيف يستخدمه أي AI Coding Agent.

## الشجرة النهائية
```
local-rag-enterprise-docs/                                  # حزمة الوثائق (تُرفع الآن كما هي)
  README.md                                 # نقطة الدخول + ترتيب القراءة + Authority Order
  vision.md                                 # رؤية المشروع
  constitution.md                           # القواعد غير القابلة للتفاوض (المرتبة 1)
  PACKAGE_CHECKLIST.md                      # خريطة الحزمة وحالة كل ملف
  github-docs-structure.md                  # هذه الوثيقة
  architecture/
    README.md                               # فهرس وثائق المعمارية + خريطة الاستخراج
    diagrams/                               # (يُرفع) Full_Stack_Architecture.svg — المخطط المعتمد
    …-architecture.md                       # (لاحقاً) تُستخرج من الكتالوج عند زرع specs (T-0.1.3)
  catalogs/
    Feature_Technical_Architecture_Catalog.md   # الكتالوج v2.0 (المرتبة 3)
    …                                       # (لاحقاً/اختياري) فصل كتالوجات فرعية إن لزم
  methodology/
    Spec_Driven_Modular_Monolith_Methodology.md # المنهجية v2.0 (المرتبة 2)
    coding-standards.md                     # قواعد الكود والوكلاء (المرجع الموسّع لـ §9/§16)
    testing-strategy.md                     # استراتيجية الاختبار (المرجع الموسّع لـ §10)
  decisions/
    open-decisions.md               # Open Decisions (المرتبة 4)
    license-review.md                       # سجل مراجعة التراخيص (بوابة إلزامية)
    adr/
      README.md                             # السجل الكنسي للـ ADRs (الترقيم + الحالات)
      ADR-XXXX-*.md                         # (لاحقاً) ملف لكل قرار عند زرع specs
  phases/
    README.md                               # قواعد مجلد المراحل
    phase-roadmap.md                        # خريطة المراحل (المرتبة 5)
    phase-0-foundation-full-stack-skeleton.md           # تصميم Phase 0 v2.0 (معتمد)
    phase-1-…md … phase-8-…md               # (لاحقاً) تصميم كل مرحلة في محادثة مستقلة
  handoff/
    handoff.md                              # التسليم الحالي + القالب
    archive/                                # (لاحقاً) أرشيف نسخ handoff بتاريخها
  superseded/
    README.md                               # فهرس الوثائق المتجاوزة + قاعدة الوسم
    …                                       # (لاحقاً) نقل الملفات القديمة إليه
```

## وظيفة كل مجلد وأين يوضع كل شيء
- **الجذر:** الهوية والدستور والرؤية والفهرس.
- **architecture/:** وثائق المعمارية الفرعية (data/permission/agent/orchestration/media/integration/deployment/configuration-and-profiles) — محتواها الآن مُوحَّد داخل الكتالوج؛ **تُستخرج لاحقاً** في مهمة زرع specs. المخططات في `diagrams/` والمعتمد بصرياً `Full_Stack_Architecture.svg`.
- **catalogs/:** الكتالوج المرجعي (ميزات/خدمات/شاشات/تقنيات/سيناريوهات/أحداث تدقيق).
- **methodology/:** المنهجية + معايير الكود + استراتيجية الاختبار (handoff-strategy ضمن المنهجية §14 + قالب handoff/).
- **decisions/:** **open decisions** هنا · **license reviews** هنا · **ADRs** في `decisions/adr/`.
- **phases/:** **خريطة المراحل** + **تصاميم المراحل** (ملف لكل مرحلة باسم `phase-N-name.md`؛ العربية في العنوان الداخلي).
- **handoff/:** **handoff logs** — الحالي في `handoff.md` والأرشيف في `archive/`.
- **superseded/:** الوثائق/البرومبتات القديمة المخالفة للقرارات الحالية — تُنقل أو تُوسم هنا ولا تُقرأ للتنفيذ.

## ما يُرفع الآن / ما يُنشأ لاحقاً
- **يُرفع الآن (جاهز):** كل ملفات الشجرة غير الموسومة (لاحقاً) — القائمة الكاملة في `PACKAGE_CHECKLIST.md` — إضافة إلى `architecture/diagrams/Full_Stack_Architecture.svg`.
- **يُنشأ لاحقاً:** ملفات المعمارية المستخرجة · ملفات ADR الفردية · تصاميم Phase 1–8 · أرشيف handoff · محتويات superseded المنقولة · runbooks (troubleshooting/backup-restore/offline-install) عند نضج التشغيل.
- **علاقة الحزمة بالمنتج:** عند بدء تنفيذ Phase 0، تُزرع هذه الحزمة داخل `specs/` في المستودع الموحّد (مهمة T-0.1.3) وتبقى نسخة الوثائق مرجعاً؛ **الترتيب المرجعي واحد في الحالتين**.
- **سياسة الأسماء (مُنفَّذة):** كل مسارات الحزمة **ASCII** التزاماً بـ constitution م18؛ العناوين العربية داخل الملفات. الملفات العربية السابقة أُرشفت بأسماء ASCII داخل `superseded/`.

## كيف يستخدمها AI Coding Agent
يقرأ بالترتيب: `README.md → constitution.md → methodology/… → catalogs/… → decisions/open-decisions.md → phases/phase-roadmap.md → تصميم مرحلته فقط → handoff/handoff.md → بطاقة مهمته` · ينفّذ **المكتوب فقط** · لا dependency بلا صف في `decisions/license-review.md` · لا يلمس `decisions/adr/` أو ملفات خارج بطاقته · يُنهي بتحديث `handoff/handoff.md` · أي ملف داخل `superseded/` **لا يُستخدم**.
