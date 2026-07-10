# ADR-0004 — معمارية البحث: PostgreSQL مصدر الحقيقة · Qdrant للمتجهات · OpenSearch للنص/الهجين

> **ملاحظة زرع:** الرقم قائم في السجل الكنسي منذ الحزمة التأسيسية (Qdrant + OpenSearch حاضران في Local Demo). يُزرع ملفه هنا ضمن إغلاق خط الأساس v1.0 مع توثيق البروفايلات (D10) — دون تغيير جوهر القرار.

**السياق (Context):** RAG هجين محكوم الصلاحية يحتاج بحثاً متجهياً ونصياً/هجيناً معاً، مع بيئة تطوير على جهاز واحد وشبكة مغلقة، ومطلب ثابت: نتائج البحث لا تتجاوز صلاحيات الناظر.

**الوضع السابق (Previous state):** صف ADR-0004 (Accepted) في السجل الكنسي وconstitution م12: الحاضران في Local وpgvector/PG-FTS ضمن low-resource bundle الصريح فقط — دون ملف يفصّل الأدوار والبروفايلات.

**القرار (Decision):**
1. **PostgreSQL هو مصدر الحقيقة** (السجلات والميتاداتا والصلاحيات والتدقيق) — محركات البحث فهارس مشتقة قابلة لإعادة البناء، لا مصدر حقيقة.
2. **Qdrant = البحث المتجهي (vector)** · **OpenSearch = البحث النصي الكامل والهجين**.
3. **pgvector + PostgreSQL-FTS = بروفايل الموارد المنخفضة/الاحتياط فقط** (low_resource) — ليسا الافتراضي.
4. **البروفايل الافتراضي للـ Demo = المحركات الكاملة** (Qdrant + OpenSearch بإعدادات خفيفة)؛ **low_resource علم إعداد اختياري** صريح.

**البدائل (Alternatives):** pgvector/PG-FTS افتراضاً (مرفوض — أداء/جودة أدنى للهجين والإعادة الترتيبية، ويخفي مشاكل التكامل حتى الإنتاج) · Elasticsearch (مرفوض — ترخيص غير Apache منذ 7.11؛ OpenSearch مكافئ بترخيص Apache-2.0) · محرك واحد للكل (مرفوض — لا محرك واحداً يتقن المتجهي والنصي الهجين معاً بمستوى مؤسسي).

**السبب (Rationale):** فصل الأدوار يعطي أفضل أداء لكل نمط استرجاع؛ وإبقاء PG مصدرَ الحقيقة يجعل الفهارس قابلة للهدم وإعادة البناء عند تغيير embedding أو استعادة نسخة احتياطية.

**العواقب (Consequences):** الفهرسة تحمل وسوم الصلاحية/التصنيف من المصدر (الترشيح قبل الإرجاع)؛ تغيير نموذج embedding يستوجب خطة إعادة فهرسة (حوار admin.capabilities)؛ الصورتان حاضرتان في compose بإعداد demo وصف ترخيص شكلي (Apache-2.0).

**خطة الانتقال (Migration plan):** بين البروفايلات بالإعداد فقط: تفعيل low_resource يوجّه SearchAPI/RagAPI إلى pgvector/PG-FTS — دون تغيير كود أعمال؛ العودة كذلك.

**الحالة (Status):** Accepted
**التاريخ (Date):** 2026-07-10 (الأصل: الحزمة التأسيسية 2026-07-02 · constitution م12)
**الوثائق المرتبطة (Related documents):** ../../constitution.md (م12) · ../open-decisions.md (صف Qdrant + OpenSearch) · ../../methodology/Spec_Driven_Modular_Monolith_Methodology.md (§7 — search/rag) · ../../phases/phase-0-foundation-full-stack-skeleton.md (FR-0.9) · ../license-review.md (صفا Qdrant/OpenSearch)
