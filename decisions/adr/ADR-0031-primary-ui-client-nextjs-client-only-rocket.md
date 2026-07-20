# ADR-0031 — عميل الواجهة الأساسي: Next.js Client-Only عبر قناة Rocket المحكومة

**السياق (Context):** قرر مالك المشروع (Q1 — ‏Final Decision Addendum ‏2026-07-19) اعتماد مسار Rocket لبناء واجهة AQL، وأنتجت التجربة مستودع `aql` (‏Next.js ‏15، ‏App Router) بأربع شاشات مرشّحة، دون أي Server Actions أو Route Handlers أو Middleware لمنطق الأعمال (تحقق جرد 2026-07-18). يلزم تقنين هذا الاتجاه بحراس قابلة للفحص تحفظ مبدأ العميل القابل للاستبدال (م23/ADR-0029) وعقد الواجهة (ADR-0025).

**الوضع السابق (Previous state):** ‏ADR-0017 (‏Accepted) يعتمد React + Vite + TypeScript للعميل؛ ‏`platform/AGENTS.md` و`platform/docs/SPEC_SOURCE.md` يكرران ذلك؛ لا يوجد قرار سابق يذكر Next.js أو Rocket؛ تجربة Flutter مُنحّاة نهائياً (دفعة 2026-07-11) وOpen WebUI جسر مؤقت حصراً (ADR-0030).

**القرار (Decision):**
1. مستودع `aql` (‏Next.js **client-only**) هو **عميل الواجهة الأساسي** لمنصة AQL Enterprise AI Platform — by AQLORA.
2. **الحراس الأربعة** — ملزمة وقابلة للفحص الآلي في CI:
   ‏(أ) **يُمنع** استخدام Server Actions أو Route Handlers أو Middleware لأي منطق أعمال — فحص آلي يفشل عند وجودها؛
   ‏(ب) كل البيانات **حصراً** عبر عقود المنصة (‏ADR-0025: ‏REST + OpenAPI + SSE من FastAPI) بعميل API **مولَّد من OpenAPI** — لا نداء endpoints يدوياً لأفعال الأعمال (‏UI_FIELD_NAMING §2)؛
   ‏(ج) منطق الميزات معزول عن `next/*` قدر الإمكان في طبقة features قابلة للنقل؛
   ‏(د) بوابة **strip-externals**: بروفايل الإنتاج صفر موارد/سكربتات خارجية (تفصيلها التشغيلي في `methodology/ROCKET_OPERATING_MODEL.md`).
3. **بوابات الجودة عقدها أسماء سكربتات المستودع الموحدة** — ‏`pnpm typecheck` · ‏`pnpm lint` · ‏`pnpm build` — وما تنفذه هذه السكربتات داخلياً (‏tsc، أداة lint الإطار، …) **تفصيل تنفيذ قابل للتغيير لا عقد** (قرار مالك، أمر G1 بند 6).
4. قابلية الاستبدال (م23) تُثبَت لاحقاً بـ**عميل React/Vite مصغر** على العقود ذاتها — بند سجل المؤجلات القائم («اختبار الاستبدال») يظل مرجعها؛ لا عميل موازٍ كامل الآن.
5. لا منطق أعمال في أي طبقة من طبقات Next.js؛ الخادم (‏FastAPI) يبقى مصدر التحقق والصلاحيات والتنفيذ والتدقيق (ADR-0029).

**البدائل (Alternatives):** إبقاء React + Vite حرفياً وإسقاط مسار Rocket (مرفوض — يهدر تجربةً قائمةً قرَّر المالك اعتمادها ولا يضيف ضماناً معمارياً فوق الحراس)؛ اعتماد Next.js بكامل قدراته الخادمية (مرفوض — يخلق مصدر منطق ثانياً ويكسر ADR-0025/0029)؛ عميلان متوازيان كاملان (مرفوض — كلفة مضاعفة بلا حاجة مثبتة، ‏Anti-overengineering §11).

**السبب (Rationale):** الحراس الأربعة تجعل اختيار الإطار تفصيلاً قابلاً للاستبدال فوق عقود ثابتة — وهو جوهر م23 — بينما تحفظ قناة Rocket سرعة الإنتاج البصري تحت حوكمة كاملة.

**العواقب (Consequences):** أدوات Rocket (‏component-tagger وسكربتاته) **dev-only** وتُجرَّد من الإنتاج؛ يُحدَّث `platform/AGENTS.md` و`platform/docs/SPEC_SOURCE.md` (نفس الدفعة)؛ بوابة UI Foundation ‏(G4) تشترط اجتياز الحراس بالأدلة؛ ‏ADR-0017 يُوسم Superseded-in-scope (اختيار الإطار للعميل الأساسي فقط) وتبقى مبادئه نافذة.

**خطة الانتقال (Migration plan):** لا هجرة كود (لا كود منصة بعد)؛ مواءمة مسارات/تسميات `aql` مع الجرد الكنسي تُحسم في بوابة G4 ‏(FG-3) بوصفها Correction candidates مسجلة — لا حسم صامتاً قبلها.

**الحالة (Status):** Accepted — G1-B 2026-07-20 (merge dd098dff9bed7a1f267ec5552b0e3366e368883d · tag v1.2-governance-baseline) (بوابة الإغلاق مستوفاة ضمن الدفعة ذاتها)
**التاريخ (Date):** 2026-07-19
**الوثائق المرتبطة (Related documents):** ../../constitution.md (م23) · ADR-0017-frontend-stack-react-vite-typescript.md (‏Superseded-in-scope) · ADR-0025 (سجل README — عقد REST+OpenAPI+SSE) · ADR-0029-replaceable-client-principle.md · ../DEFERRED_IMPLEMENTATION.md (بند اختبار الاستبدال) · ../../methodology/ROCKET_OPERATING_MODEL.md · ../../ui/UI_FIELD_NAMING.md §2 · `aql@eab9f99` (حالة التجربة المرجعية)
