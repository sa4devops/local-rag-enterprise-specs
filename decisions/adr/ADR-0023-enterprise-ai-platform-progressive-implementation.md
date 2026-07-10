# ADR-0023 — الهوية: Enterprise AI Platform with Progressive Implementation

**السياق (Context):** تعددت الصياغات الواصفة للمشروع (منصة معرفية، Command Center، «ليست chatbot»، اقتراح «Product-led Platform») واحتاج إغلاق مرحلة المعمارية إلى هوية رسمية واحدة تضبط القراءة والتنفيذ وتمنع بناء القدرات قبل أوانها أو حذفها لتأجيلها.

**الوضع السابق (Previous state):** README/vision يعرّفان المشروع وصفياً («منصة تشغيل معرفي مؤسسي مغلق») مع قوائم «ما ليس هو المشروع»، دون سطر هوية معتمد موحّد؛ مبدأ «كل الطبقات حاضرة» موجود (constitution م13/م15) بلا قاعدة صريحة تحكم توقيت التنفيذ مقابل الالتزام المعماري، ولا سلّم جاهزية مسمى.

**القرار (Decision):** الهوية الرسمية: **Enterprise AI Platform with Progressive Implementation** — المنصة هي المنتج؛ ليست chatbot وليست تطبيقاً واحداً؛ المعمارية الكاملة والحدود المستقبلية توثَّق من البداية؛ التنفيذ والتفعيل مرحليان. لا يُستخدم مسمى «Product-led Platform» رسمياً. الجملة الحاكمة (حرفية): "Future capabilities are architectural commitments. They shall not be implemented prematurely, and they shall not be removed merely because they are scheduled for later phases." ويعتمد **سلّم الجاهزية السداسي**: Architecture-ready → Contract-ready → Provider-ready → Implementation-ready → Runtime-activated → Production-scaled (المرجع المعياري: methodology/agent-execution-model.md §10/§11 وconstitution م22).

**البدائل (Alternatives):** «Product-led Platform» كمسمى رسمي (مرفوض — يوحي بمنهج تسويقي ولا يضبط التدرج التنفيذي) · هوية «Chatbot/Assistant مؤسسي» (مرفوضة — الدردشة سطح واحد لا المنتج) · بناء كل القدرات دفعة واحدة (مرفوض — over-engineering وحمل عتادي سابق لأوانه) · حذف القدرات المؤجلة من المعمارية (مرفوض — يهدم constitution م13/م15).

**السبب (Rationale):** سطر هوية واحد يمنع انحراف الوكلاء والتصاميم؛ والجملة الحاكمة تحسم التوتر الدائم بين «لا تنفيذ مبكر» و«لا حذف معماري»؛ والسلّم يعطي لغة قياس موحدة لحالة كل قدرة.

**العواقب (Consequences):** كل وثيقة تقديمية تحمل سطر الهوية؛ القدرات المؤجلة تُوثَّق بقالب «التزام معماري مستقبلي» (phase-roadmap)؛ أي محاولة تنفيذ مبكر أو حذف موطئ معماري تُرفض استناداً إلى م22.

**خطة الانتقال (Migration plan):** لا انتقال تقنياً — تحديث نصي منفَّذ في vision/README/phase-roadmap ضمن حزمة خط الأساس.

**الحالة (Status):** Accepted
**التاريخ (Date):** 2026-07-10
**الوثائق المرتبطة (Related documents):** ../../vision.md · ../../README.md · ../../constitution.md (م13/م15/م21/م22) · ../../methodology/agent-execution-model.md (§10/§11) · ../../phases/phase-roadmap.md · ADR-0028-architecture-baseline-frozen.md
