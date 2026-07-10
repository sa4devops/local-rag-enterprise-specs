# ADR-0025 — عقد الواجهة/الخادم: REST + OpenAPI + SSE (وWebSocket مؤجل بشرط)

**السياق (Context):** الواجهة SPA مستقلة منطقياً (ADR-0017) وتحتاج عقداً رسمياً واحداً مع الخادم يغطي الطلب/الاستجابة والبث التدريجي (ردود LLM، تقدم مهام طويلة) داخل شبكة مغلقة.

**الوضع السابق (Previous state):** الوثائق تذكر «SPA تستهلك OpenAPI/SDK» و«عقد OpenAI-compatible للـ Gateway» دون ADR يحسم أسلوب البث، وموقف WebSocket، وشكل عميل TypeScript.

**القرار (Decision):**
1. **REST هو الأسلوب الأساسي**، و**OpenAPI هو العقد الرسمي** الملزم (مصدر التوليد والاختبار).
2. **SSE (Server-Sent Events) للبث**: ردود النماذج المتدفقة، تقدم المهام الطويلة، تحديثات الحالة.
3. **WebSocket لا يُعتمد إلا إذا ظهرت حالة حقيقية يعجز عنها SSE** (تفاعلية ثنائية الاتجاه عالية التواتر) — وذلك بقرار ADR جديد.
4. **عميل TypeScript**: **توليد الأنواع (types) من OpenAPI + غلاف fetch رفيع مكتوب يدوياً** — لا مولّدات عملاء كاملة إلزامية الآن (تبقى خياراً لاحقاً).
5. **منطق الأعمال في الخادم حصراً**؛ الواجهة تملك: حالة UI · التنسيق/العرض · validation عرضية (presentation) · منطق التفاعل.
6. هذا القرار **ADR وليس مادة دستورية** — تعديله يتبع مسار ADR الاعتيادي.

**البدائل (Alternatives):** GraphQL (مرفوض — تعقيد صلاحيات على مستوى الحقول لدينا محسوم في RLS/FLS الخادمية، ولا حاجة لمرونة الاستعلام الحر) · WebSocket أولاً (مرفوض — أثقل تشغيلاً وتوافقاً عبر proxies؛ SSE يكفي حالات البث لدينا) · مولّد عميل كامل (openapi-generator/orval) من الآن (مؤجل — يضيف سطح صيانة قبل استقرار العقود).

**السبب (Rationale):** FastAPI يعطي OpenAPI مجاناً؛ SSE أبسط وأكثر متانة خلف بوابات المؤسسة وقابل للتشغيل بلا بنية إضافية؛ types-first يحفظ أمان الأنواع دون قفل على مولد عميل.

**العواقب (Consequences):** كل endpoint جديد يبدأ من العقد (operationId بنمط UI_FIELD_NAMING)؛ اختبارات contract على العقد المولد؛ أي حاجة WebSocket تمر بـ ADR؛ الـ SDK في packages/shared-types يُبنى من العقد.

**خطة الانتقال (Migration plan):** لا يوجد عملاء قائمون؛ عند اعتماد مولّد عميل كامل لاحقاً يكون إضافة فوق الأنواع المولدة لا استبدالاً كاسراً.

**الحالة (Status):** Accepted
**التاريخ (Date):** 2026-07-10
**الوثائق المرتبطة (Related documents):** ../../ui/UI_FIELD_NAMING.md (§1 api_operation · §2) · ../../methodology/coding-standards.md (§2/§6) · ../../methodology/Spec_Driven_Modular_Monolith_Methodology.md (§6 packages) · ADR-0017-frontend-stack-react-vite-typescript.md · ADR-0024-backend-stack-python-fastapi.md
