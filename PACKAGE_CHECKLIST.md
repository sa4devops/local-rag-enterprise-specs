# PACKAGE_CHECKLIST.md — Final GitHub Package Checklist

> **Version:** 1.1 (D1–D9 مدمجة) · **Status:** Current · **Date:** 2026-07-04
> **Purpose:** خريطة الحزمة النهائية: كل ملف، مساره، حالته، جاهزيته للرفع، وما يلزم قبل **التنفيذ** (لا قبل الرفع).

| الملف | المسار داخل GitHub | الحالة | جاهز للرفع؟ | يحتاج قراراً قبل التنفيذ؟ |
|---|---|---|---|---|
| README.md | `/README.md` | v1.1 — الستاك D1–D3 + سياسة D8 | ✅ | لا |
| vision.md | `/vision.md` | v1.0 (غير متأثرة) | ✅ | لا |
| constitution.md | `/constitution.md` | v1.0 — **لم يتغيّر عمداً** (لا يذكر ستاكات؛ D8 امتداد م7) | ✅ | لا |
| PACKAGE_CHECKLIST.md | `/PACKAGE_CHECKLIST.md` | v1.1 | ✅ | لا |
| github-docs-structure.md | `/github-docs-structure.md` | v1.0 (بنية فقط — غير متأثرة) | ✅ | لا |
| Feature_Technical_Architecture_Catalog.md | `/catalogs/…` | **v2.1** — D1–D9 مدمجة (§2 + §3.1/3.3/3.8 + §5 + §15) | ✅ | لا |
| Spec_Driven_Modular_Monolith_Methodology.md | `/methodology/…` | **v2.1** — عقود shared + §16/§17 + D8 | ✅ | لا |
| coding-standards.md | `/methodology/coding-standards.md` | **v1.1** — C5 محسوم + §9 Reference-aware + §10 Observability | ✅ | تثبيت إصدارات Python/Node عند بدء التنفيذ |
| testing-strategy.md | `/methodology/testing-strategy.md` | **v1.1** — +Provider-Equivalence +Logging/Error-Contract | ✅ | لا |
| open-decisions.md | `/decisions/open-decisions.md` | **v2.1** — C1–C5 مُغلقة؛ إعادة تصنيف كاملة | ✅ | هو ذاته سجل بوابات التنفيذ |
| license-review.md | `/decisions/license-review.md` | **v1.1** — صفوف الستاك + uv/pnpm + OpenWebUI-كمرجع + سياسة المراجع | ✅ | **نعم:** إقرار صفوف الستاك قبل أول كود؛ الفئة 3 عند تفعيل صورة اختيارية |
| adr/README.md | `/decisions/adr/README.md` | **v1.1** — السجل الكنسي **ADR-0001..0022** | ✅ | لا |
| phase-roadmap.md | `/phases/phase-roadmap.md` | **v1.1** — بوابات P0/P5 محدّثة + بند D1–D9 | ✅ | لا |
| phases/README.md | `/phases/README.md` | v1.0 (قواعد المجلد — غير متأثرة) | ✅ | لا |
| phase-0-foundation-full-stack-skeleton.md | `/phases/…` | **v2.1 — Accepted for Design** (C1–C5 مُغلقة؛ FR-0.4/0.9/0.11/0.13 + FR-0.19) | ✅ | **قبل تنفيذها:** صفوف ترخيص الستاك فقط (لا بوابة فئة 3 على P0.4) |
| handoff.md | `/handoff/handoff.md` | H-0002 (دمج D1–D9) فوق H-0001 | ✅ | لا |
| architecture/README.md | `/architecture/README.md` | **v1.1** — فقرة تحديث D1–D9 + ملاحظة SVG الحاكمة | ✅ | لا |
| Full_Stack_Architecture.svg (+Agent/Deployment) | `/architecture/diagrams/…` | معتمد مفهومياً؛ **التحديث البصري لاحقاً** (النص يحكم الفروق) | ✅ | لا |
| superseded/README.md + 11 أرشيفاً | `/superseded/…` | v1.0 — تاريخية موسومة | ✅ | لا تُستخدم إطلاقاً |

**تُنشأ لاحقاً (ليست نقصاً):** ملفات المعمارية المستخرجة · ملفات ADR الفردية · تصاميم Phase 1→8 · handoff/archive · runbooks.

**خلاصة الجاهزية:** لا قرار يمنع **الرفع**. قبل **التنفيذ**: إقرار صفوف ترخيص الستاك المعتمد فقط. **بوابة compose (فئة 3)** تنطبق حصراً عند **تفعيل** صورة اختيارية (Valkey / MinIO أو SeaweedFS / خادم مراقبة). قبل **مرحلة الوسائط**: OCR/PDF-tooling/ffmpeg/أوزان النماذج. قبل **الإنتاج/التوزيع**: فئة 4 كاملة.
