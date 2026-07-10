# Constitution — القواعد غير القابلة للتفاوض

> **Document Title:** constitution.md · **Version:** 1.1 (+م21 خط الأساس المعماري · +م22 القدرات المستقبلية — v1.0-architecture-baseline) · **Status:** Current / Accepted · **Date:** 2026-07-10 (الأصل 2026-07-02)
> **Authority:** **المرتبة الأولى** — تحكم كل الوثائق والكود والوكلاء. أي تعارض يُحسم لصالح هذا الملف. تعديل أي مادة يتطلب قرار مالك المشروع + ADR.
> **Purpose:** دستور المشروع الذي يلتزم به كل إنسان وكل AI Coding Agent.

## المواد

1. **الـ LLM ليس Source of Truth.** مصادر الحقيقة حصراً: قواعد البيانات الرسمية، المستندات المعتمدة، الـ APIs الداخلية، السجلات الرسمية. النموذج يعالج ما يُجلب له فقط.
2. **الصلاحية قبل الجلب.** تُقيَّم الصلاحيات (RBAC+ABAC+ReBAC+التصنيف+RLS/FLS+Need-to-know+SoD) **قبل** أي retrieval أو SQL أو استدعاء API، بمبدأ **default-deny**.
3. **Audit شامل.** كل عملية مهمة (قراءة حرجة/إنشاء/تعديل/حذف/تصدير/اعتماد/تغيير إعداد أو علم أو نموذج أو profile) تُسجَّل في Audit Log **append-only** مع قرار الصلاحية.
4. **لا اتصال خارجي وقت التشغيل.** النظام air-gapped؛ أي tool/model/connector يحتاج الخارج **ممنوع** ما لم يُنص ويُعتمد صراحةً (عبر proxy/gateway اختياري لاحقاً).
5. **الانتقال إلى الإنتاج configuration-only.** نفس الكود/الـ repo/الصور في كل البيئات؛ الفرق env/config/resources/endpoints/secrets/replicas فقط. **ممنوع** تعديل كود أو معمارية أو fork للإنتاج.
6. **الواجهة النهائية Enterprise UI خاصة** (Arabic/English، RTL كامل، white-label). **Open WebUI ليس الواجهة النهائية** — مرجع دراسة فقط، وأي استخدام داخلي مشروط بمراجعة قانونية.
7. **License Review إلزامي.** لا يدخل أي dependency أو repository أو container image أو **model weights** إلى المنتج قبل صف مراجعة معتمد في `decisions/license-review.md` (للإصدار/الصورة المحددة). البوابة **متكررة** لكل إضافة جديدة.
8. **Modular Monolith أولاً** (ADR-0001). backend واحد قابل للنشر، حدود modules **مفروضة تقنياً** (لا وصول لجداول module آخر؛ النداء عبر واجهات معلنة؛ منع الاعتماد الصاعد/الدوري)، مع قابلية فصل modules لاحقاً.
9. **Spec-driven Development** متوافقة مع GitHub Spec Kit / Spacekit: `Vision → Specify → Clarify → Plan → Tasks → Implement`. لا كود قبل مواصفة معتمدة؛ الوكيل ينفّذ المكتوب فقط ويسأل عند الغموض.
10. **لا DDL مباشر من LLM.** توليد قواعد البيانات = metadata → migration file → فحص تعارض/مخاطر → **اعتماد** → تطبيق → versioning → audit → شاشة توثيق. (Baseline migrations للمطوّر تمرّ بمراجعة PR — مسار منفصل ومسمّى.)
11. **لا استدعاء نموذج خارج LLM Gateway** (عقد OpenAI-compatible). النماذج مربوطة بـ **capabilities** عبر Model/Provider Registry، وتغييرها من الأدمن دون كود، مع fallback معرّف وValidation لا تفشل مفتوحة.
12. **Qdrant وOpenSearch حاضران في Local Demo** بإعدادات خفيفة. pgvector/PostgreSQL-FTS **fallback ضمن low-resource bundle صريح فقط** — ليسا بديلاً افتراضياً.
13. **دعم الوسائط معماري من البداية.** OCR/صور/صوت/فيديو/Multimodal عبر pipeline + Registry + Gateway، بمعالجة محكومة الصلاحية ومربوطة بالمصدر ومدقَّقة؛ تشغيل النماذج الثقيلة يتبع العتاد عبر الإعداد، **لا يُحذف الدعم ولا يؤجَّل معمارياً**.
14. **فصل مستويات التحكم:** Admin يدير **capabilities/features** (flags)؛ Super Admin يدير الإعداد والسياسات؛ **Operations فقط** يشغّل/يوقف/يوسّع services وcontainers ويدير secrets/TLS/النسخ الاحتياطي. الخدمات الأساسية (Auth/Permissions/Audit/Config/Flags/Registry/DB) **محميّة** لا تُعطَّل من الواجهة.
15. **كل الطبقات حاضرة.** لا تُحذف خدمة/طبقة لثقلها؛ الحالات المسموحة: enabled/disabled/lightweight/demo/production/optional/protected.
16. **الكاش تسريع فقط.** لا final-response cache لبيانات الأعمال؛ مفاتيح RAG cache تشمل نسخة المستند/الفهرس/السكيم/نطاق الصلاحية؛ **إعادة تحقق live** قبل أي تعديل/اعتماد/تصدير رسمي.
17. **الثوابت المحمية:** الرقم الوظيفي واسم المستخدم والرقم المرجعي **immutable** على مستوى قاعدة البيانات.
18. **معرّفات تقنية ASCII؛ العربية labels في الميتاداتا.**
19. **قابلية إعادة البناء مغلقاً:** lockfiles لكل مديري الحزم + **digest pinning** لصور الحاويات + حزمة offline موقّتة/متحقَّقة، ومستخدم DB بأدنى صلاحية لكل قاعدة من التهيئة الأولى.
20. **الوثائق تحكم.** ترتيب المرجعية: constitution → Methodology → Catalog → Open-Decisions → phase-roadmap → تصاميم المراحل → superseded. كل جلسة تنفيذ تنتهي بتحديث `handoff.md`. أي وثيقة/برومبت قديم يخالف = **Superseded**.
21. خط الأساس المعماري (Architecture Baseline). المعمارية مجمّدة للتنفيذ اعتباراً من الإصدار الموسوم v1.0-architecture-baseline. التجميد لا يعني الاستحالة: أي تغيير معماري لاحق لا يمر إلا عبر ADR وفق decisions/adr/README.md؛ أما التوضيحات وتصحيح الأخطاء الكتابية وإصلاحات الاتساق والتفاصيل التنفيذية غير المعمارية فلا تعيد فتح المعمارية.
22. القدرات المستقبلية التزامات معمارية. Future capabilities are architectural commitments. They shall not be implemented prematurely, and they shall not be removed merely because they are scheduled for later phases. لا تُبنى قدرة قبل مرحلتها ولا يُحذف موطؤها المعماري لأنها مؤجلة؛ سلّم الجاهزية وشروط الـabstraction المبكر في methodology/agent-execution-model.md.
