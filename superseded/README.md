# superseded/README.md — فهرس الوثائق المتجاوزة

> **Version:** 1.0 · **Status:** Current / Accepted · **Date:** 2026-07-02
> **القاعدة (constitution م20 + A1):** أي وثيقة أو برومبت أو مخطط يخالف الترتيب المرجعي أو القرارات الحالية **يُنقل إلى هذا المجلد أو يُوسم Superseded**، و**لا يُقرأ للتنفيذ إطلاقاً** — مرجع تاريخي فقط.

## لافتة الوسم (تُضاف أعلى كل ملف متجاوز)
`> ⚠️ SUPERSEDED — لا يُستخدم للتنفيذ. المرجع الحالي: <اسم الوثيقة البديلة>. تاريخ الوسم: YYYY-MM-DD.`

## السجل الحالي للمتجاوز (يُنقل إلى هذا المجلد عند الرفع)
| العنصر | سبب التجاوز | البديل المعتمد |
|---|---|---|
| `Phase-0-Prompt.md` (القديم) | سبق اعتماد المنهجية؛ برومبت تنفيذ مبكر | `phases/تصميم_المرحلة_الأولى_Phase0.md` v2.0 |
| `Phase-1-Prompt.md` (القديم) | سبق اعتماد المنهجية | تصميم Phase 1 القادم (محادثة مستقلة) |
| `system-design-v1.md` — خصوصاً قسم خريطة المراحل | خريطة قديمة قبل إعادة التفكير الشامل | `phases/phase-roadmap.md` |
| `pre-design-analysis-v1.md` و`full-architecture-study-v1.md` | وثائق تاريخية استوعبها الكتالوج v2.0 | `catalogs/Feature_Technical_Architecture_Catalog.md` |
| `system-architecture-v1.svg` | يُظهر Open WebUI كسطح دردشة (قرار متجاوز) | `architecture/diagrams/Full_Stack_Architecture.svg` |
| `Component_Diagram.svg` (القديم) | طبقة عرض سابقة لقرار Enterprise UI النهائي | المخطط المعتمد أعلاه |
| النسخ v1.0 من: الكتالوج، المنهجية، تصنيف القرارات، تصميم Phase 0 (الملفات هنا: Feature_Technical_Architecture_Catalog-v1.md · Spec_Driven_Modular_Monolith_Methodology-v1.md · open-decisions-v1.md · phase-0-design-v1.md) | حلّت محلها v2.0 المدمجة (A1–A11) | نسخ v2.0 في الحزمة |
| ترقيم ADRs في المنهجية v1.0 | استُبدل بالسجل الكنسي | `decisions/adr/README.md` |
| أي برومبت سابق يعامل النظام كـ chatbot أو Open WebUI كواجهة نهائية أو LLM كمصدر حقيقة | يخالف constitution | constitution.md + الكتالوج v2.0 |

**قاعدة تشغيل:** عند تجاوز أي وثيقة مستقبلاً: (1) أضف اللافتة أعلاها، (2) انقلها إلى هذا المجلد، (3) أضف صفاً في هذا الجدول، (4) حدّث handoff.
