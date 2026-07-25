# خارطة مسار المصالحة R1–R11 — الرسمية الموجزة

> **Version:** 1.1 — (Δ 2026-07-25 · P3 — تفعيل R2 بأمر SA: صدر في الجلسة الأمر الصريح «SA ACTIVATION ORDER — R2 + RAR SUPPLEMENTARY RECONCILIATION» بتاريخ 2026-07-25 — (أ) **R2 مُفعَّلة**؛ (ب) نطاق R2 الأصلي «مصالحة سطرية للمسودات الأربع مع المقنَّن» **لم يتغيّر**؛ (ج) مصالحة حزمة RAR **نشاطٌ تكميلي مصرَّح به ضمن أمر التفعيل نفسه** لا توسيعٌ لنطاق R2؛ (د) **وليست مساراً R جديداً** ولا تُنشئ R12؛ (هـ) المرجع: أمر التفعيل أعلاه؛ **(و) تصحيح 2026-07-25 — يتجاوز نص commit 5bb7dc0:** حزمة RAR الأصلية مدخلٌ تحليلي **تاريخي موجود**، استُعيدت من مكتبة ملفات ChatGPT (2026-07-25) وتُحقِّق منها (٨ ملفات · بصمات فردية ومجمّعة مطابقة) وأُرشِفت **غيرَ حاكمة** في `references/analysis-inputs/rar-2026-07/`؛ البحث السابق (filesystem/Git) صحيحٌ **فقط ضمن المواقع المفحوصة** ولا يُثبت عدم الوجود أو عدم التسليم — فيُتجاوَز حكمُ عدم التسليم ووصفُ الإغلاق المخفَّض. مصالحة RAR **لم تبدأ** وP3 **غير مكتملة**؛ **§13b: PENDING — TO BE DETERMINED FROM THE COMPLETED RAR RECONCILIATION TABLE** (تجاوز مالك مؤقت مؤرَّخ؛ لا يجمّد المسارات تلقائياً؛ التفصيل في handoff H-0021). R2 تبقى مُفعَّلة بنطاقها الأصلي) — Accepted — R1-B 2026-07-21 (authorized by main merge 6d50a4c41f0fcf76e5db41206f5f5e1eac4869d4; effective upon promotion merge) · **Date:** 2026-07-21 (Δ 2026-07-25) · **الموضع:** `methodology/RECONCILIATION_ROADMAP.md`

**فصل ملزم:** هذا مسار **مصالحة المواصفات والحوكمة** — يُنتج وثائق وعقوداً وقرارات لا كوداً؛ وهو **منفصل تماماً عن مراحل تطوير المنتج P0–P8** (`phases/phase-roadmap.md`) وعن بوابات G التنفيذية (G2 · G3) وعن حزم FP. **قاعدة التفعيل:** كل مرحلة R تُفعَّل بأمر مالك صريح؛ ويجوز دمج مراحل أو تخطيها بقراره؛ وبعضها مشروط بأدلة تشغيل لاحقة (R7 مشروطة بأدلة FP-0001؛ R11 تُغلق المسار بمصفوفة ختامية).

| R | الاسم | الهدف الموجز | المخرج | تغذّي |
|---|---|---|---|---|
| **R1** | Current-State Baseline & Authority Verification | تثبيت خط الأساس المنشور ومصفوفة الفجوات | تقرير R1 + دفعة R1-B التقنينية (تُغلق R1) | كل ما بعدها |
| R2 | Historical Drafts Delta Reconciliation | مصالحة سطرية للمسودات الأربع مع المقنن؛ استيعاب الدلتا أو الإغلاق | تقرير دلتا + دفعة مصغرة إن لزم | نظافة SoT |
| R3 | Contracts Coverage Expansion | توسيع عقود الشاشات ذات الأولوية + تعبئة فهرس الأنواع الموحد | عقود Candidate إضافية | تخطيط FPs |
| R4 | Permissions & Scoped-Admin Detail Spec | عقد الصلاحيات الكامل (التقاطع الرباعي · سياسة إعادة حساب الموروث · معايير قبول المنح المنطاق) | Permission Contract + مواصفة اختبار | P4 |
| R5 | Workflow/Org & SLA Contracts Detail | إغلاق حقول الملكية وusing/step-scope + عقدا SLA-Policy/Templates + حسم CC-WF-2/3 | حزمة عقود Workflow | P3 |
| R6 | Naming/i18n/DTO Mapping Detail | جدول camel↔snake الصريح + ملكية i18n وnamespaces وdeprecation | ملحق معيار التسمية | أول FPs |
| R7 | Context Architecture Finalization | تقنين قواعد Rotating/Design Context من أدلة تشغيل FP-0001 الفعلية | تحديث سياسة السياق | كل الوكلاء |
| R8 | Control-Plane Trial Spec | تصميم trial أدنى قابل للقياس لقدرة AI_DEV_CONTROL_PLANE وسياساته | مواصفة التجربة ومعاييرها | الأتمتة اللاحقة |
| R9 | Data Portability & Scale ADRs | ADRs الخطة الخمسية ومؤشرات الانتقال وrestore-drills | سلسلة ADR | P5/P8 |
| R10 | Real-time & Extension-Store Readiness | هياكل Event Contracts وحوكمة الحزم — توثيقاً بلا اختيار تقنية | وثيقتا جاهزية | P6/P7 |
| **R11** | Reconciliation Closeout | إثبات بلوغ كل بنود الحزمة التاريخية [مقنن] أو [مؤجل بقرار]؛ تقاعد المسار وأرشفته | مصفوفة ختامية + إغلاق | إعلان اكتمال المصالحة |
