# handoff.md — سجل التسليم بين الجلسات والوكلاء

> **Version:** 1.0 · **Status:** Current / Accepted · **Date:** 2026-07-02 · **Authority:** ينفّذ Methodology §14.
> **القواعد:** لا تُغلق أي جلسة/مهمة/مرحلة دون تعبئة إدخال كامل هنا · يُؤرشف الإدخال السابق في `handoff/archive/` بتاريخه · الوكيل التالي **يقرأ هذا الملف قبل أي عمل** ويحترم قائمة «Do not touch» حرفياً · إن كانت المتطلبات غامضة: يسأل ولا يكتب.

## القالب (يُنسخ لكل إدخال)
```
## Handoff H-XXXX
- date:
- phase:
- task:
- goal:
- completed:
- not completed:
- files changed:
- decisions:
- risks:
- tests: (ناجح/فاشل + الأسماء)
- next step:
- do not touch:
- notes for next agent:
```

---

## Handoff H-0002 (الإدخال الحالي)
- **date:** 2026-07-04
- **phase:** ما قبل التنفيذ — دمج قرارات D1–D9
- **task:** تحديث الحزمة إلى الإصدار 2026-07-04 (ستاك الواجهة/الخادم، التجريدات الثلاث، التخزين FS-أولاً، الخط الرقابي الأساسي، GitHub-الآن، سياسة Reference-aware)
- **goal:** حزمة متسقة بلا تعارض (لا وثيقة تقول Next.js/SvelteKit وأخرى React)
- **completed:** تحديث 13 ملفاً (انظر PACKAGE_CHECKLIST v1.1) + ADR-0017..0022 + إغلاق C1–C5 + إعادة بناء ZIP بـ SHA جديد
- **not completed (مقصود):** لا كود · لا Phase 1 · لا تحديث بصري للـ SVG (ملاحظة حاكمة في architecture/README)
- **files changed:** README · catalogs/Catalog · methodology/{Methodology, coding-standards, testing-strategy} · decisions/{open-decisions, license-review, adr/README} · phases/{phase-roadmap, phase-0} · architecture/README · PACKAGE_CHECKLIST · handoff
- **decisions:** D1–D9 مثبتة (الكتالوج §2 + open-decisions v2.1 + ADR-0017..0022)
- **risks:** تفعيل صورة اختيارية لاحقاً دون بوابة الفئة 3 — البوابة متكررة ومنصوصة في كل المواضع
- **tests:** لا كود بعد؛ أُضيف نوعا Provider-Equivalence وLogging/Error-Contract للاستراتيجية
- **next step:** تصميم **Phase 1 — Governed Core + Screen Builder** في محادثة مستقلة (بلا كود)
- **do not touch:** superseded/ · decisions/adr/ دون طلب · constitution.md (لم يتغيّر عمداً)
- **notes for next agent:** التزم بالستاك المعتمد وبسياسة Reference-aware؛ اقرأ الترتيب في README؛ لا تبدأ كوداً وأي قرار لازم غير محسوم

---

## Handoff H-0001
- **date:** 2026-07-02
- **phase:** ما قبل التنفيذ — تجهيز حزمة الوثائق النهائية
- **task:** إصدار الحزمة v2.0 المدمجة (A1–A11) الجاهزة للرفع على GitHub
- **goal:** مرجع رسمي كامل لأي AI Coding Agent قبل أي كود
- **completed:** README · vision · constitution · Methodology v2.0 · Catalog v2.0 · Open-Decisions v2.0 · Phase-0 Design v2.0 (Accepted for design) · phase-roadmap · github-docs-structure · license-review (مزروع) · adr/README (السجل الكنسي) · testing-strategy · coding-standards · architecture/README · phases/README · superseded/README · PACKAGE_CHECKLIST
- **not completed (مقصود — ليس نقصاً):** لا كود · لا تنفيذ Phase 0 · لا تصميم Phase 1 · ملفات ADR الفردية والمعماريات المستخرجة وrunbooks تُنشأ عند زرع specs (T-0.1.3) وما بعده
- **files changed:** كل محتويات `final/` (الحزمة كاملة)
- **decisions:** ADR-0001 **Accepted** · التعديلات A1–A11 مدمجة · التسمية بالرقم+الاسم (C8 مُغلق) · الترقيم الكنسي للـ ADRs في decisions/adr/README.md
- **risks:** بنود الفئة 3 (C1–C3) غير محسومة — تحجب مهمة الـ Compose فقط · تراخيص Needs Legal Review قائمة
- **tests:** لا اختبارات بعد (لا كود) — استراتيجية الاختبار معتمدة
- **next step:** تصميم **Phase 1 — Governed Core + Screen Builder** في محادثة مستقلة (Vision→Specify→Clarify→Plan→Tasks، بلا كود)؛ وبالتوازي حسم C4/C5 وC1–C3 قبل تنفيذ Phase 0
- **do not touch:** `superseded/` وكل ما يُنقل إليه (برومبتات Phase-0/1 القديمة، المخططات القديمة، نسخ v1.0) · `decisions/adr/` دون طلب صريح · constitution.md دون قرار مالك المشروع
- **notes for next agent:** اقرأ بالترتيب المحدد في README؛ نفّذ المكتوب فقط؛ أي dependency جديدة تبدأ بصف في license-review.md
