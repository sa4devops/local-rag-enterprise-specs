# PHASE_MASTER_PLAN.md — الخطة الرئيسية لمراحل التنفيذ

> **Version:** 1.0 — Proposed (تصبح Accepted باعتماد المالك ضمن إصدار v0.3-phase-design-package) · **Date:** 2026-07-06
> **Authority:** عند الاعتماد: تفصيلٌ مُلزم تحت `phases/phase-roadmap.md` (المرتبة 5)؛ تصاميم المراحل الفردية في `phases/designs/` (المرتبة 6).
> **Related:** constitution.md · Methodology · Catalog v2.1 · open-decisions v2.1 · phase-0 design v2.1 · AGENT_EXECUTION_MODEL.md · BACKLOG_DEFERRED_SCOPE.md
> **قاعدة:** لا تنفيذ لأي مرحلة قبل: اعتماد تصميمها + استيفاء DoD المرحلة السابقة + إغلاق بنود الفئة 2 الخاصة بها + جلسة Tasks (بطاقات المهام تُولَّد عند التفعيل، لا هنا).

## 0) منطق إعادة الهندسة (من الصفر)
أُعيد اشتقاق الخطة من أربعة قيود حاكمة: (١) **الحوكمة قبل القدرة** — لا استرجاع/ذكاء قبل صلاحيات وaudit مُنفَّذين؛ (٢) **الميتاداتا قبل البيانات** — لا records قبل Screen/Field Registry وخط توليد محكوم؛ (٣) **المعرفة قبل الاستدلال** — لا Chat/SQL-Agent/تقارير قبل RAG محكوم؛ (٤) **التكامل والتصلّب أخيراً** — لا ربط أنظمة ولا packaging قبل نضج الجوهر. النتيجة تطابق بنيوياً الخريطة المعتمدة (0→8) — وهذا **تثبيت هندسي** لها لا مصادفة؛ التحسينات أدناه نطاقية فقط (موثّقة في §3).

## 1) الجدول الرئيسي — الهوية والترتيب

| # | الاسم | Purpose | لماذا توجد | لماذا في هذا الموضع | يعتمد على |
|---|---|---|---|---|---|
| 0 | Foundation &amp; Full-Stack Skeleton | أساس مفروض تقنياً: repo/حدود/إعداد/كل الطبقات حاضرة خفيفة | لا يُبنى شيء آمن بلا حدود مفروضة وconfig-driven | قبل كل شيء — يمنع الديون المعمارية من اليوم الأول | لا شيء (تصميمها v2.1 معتمد) |
| 1 | Governed Core + Screen Builder | إثبات جوهر المشروع end-to-end تحت الحوكمة (Walking Skeleton) | القيمة المميزة = توليد شاشات محكوم؛ وأعلى مجهولية تقنية | الهوية/الصلاحيات/الميتاداتا/Audit أساس كل ما بعدها | P0 |
| 2 | Advanced Screens, Records &amp; Initial Entity Profile | نضج البناء وإنفاذ العزل صفاً/حقلاً | بيانات موثوقة العزل شرط أي عمليات فوقها | RLS/FLS قبل workflows وقبل فهرسة أي محتوى | P1 |
| 3 | Workflows, Approvals &amp; Action Buttons | دورة حياة العمليات بنوعيها + مهام/مشاريع/إشعارات | المؤسسة تُدار بعمليات معتمدة لا بشاشات فقط | العمليات قبل إدخال الذكاء كي يعمل الذكاء داخل حوكمتها | P2 |
| 4 | Advanced Permissions &amp; Feature Management | اكتمال نموذج الوصول (RBAC+ABAC+ReBAC+تصنيف) + حوكمة المزايا + Entity Profile كامل | فتح المعرفة يتطلب ضبط وصول نهائياً + Safe Mode | آخر تحصين قبل فهرسة المحتوى واسترجاعه | P3 |
| 5 | Knowledge Foundation: Files, RAG, OCR &amp; Media | تفعيل الملفات والمعرفة والوسائط (نماذج خفيفة) + Registry UI + الحد الأدنى من الـ Gateway | مصدر قيمة المنصة المعرفي؛ الوسائط جاهزة معمارياً تُفعَّل هنا | RAG يحتاج صلاحيات مكتملة (P4) وembedding routing | P4 |
| 6 | Intelligence Layer: Gateway الكامل، Agents، SQL Agent، Chat، Reports | الاستدلال المسنود: دردشة مؤسسية + SQL آمن + تقارير طويلة بالاستشهاد | الذكاء **فوق** المعرفة المحكومة لا قبلها | يحتاج فهرس P5 + capabilities routing | P5 |
| 7 | Integrations &amp; Enterprise App Store | ربط الأنظمة الداخلية (MCP/API/Webhook/DB) + متجر بتفويض لكل مستخدم | قيمة "منصة تشغيل" لا تكتمل بلا أنظمة المؤسسة | التكامل بعد نضج الحوكمة والذكاء (أفعال خطرة ببوابات) | P6 |
| 8 | Production Readiness: Observability, Offline Packaging &amp; Hardening | جاهزية الإنتاج: مراقبة موسّعة، حزمة نقل موقّعة، backup/restore، ترقية config-only مُثبتة | air-gapped promise يُثبَت هنا نهائياً | التصلّب بعد اكتمال الوظائف | P7 |
| B | Backlog | مؤجَّلات بقرار | خارج مسار التنفيذ الأول | تُفعَّل بقرار وسعة | حسب البند |

## 2) الجدول الرئيسي — المدخلات/المخرجات/التمكين/الخروج

| # | Required inputs | Expected outputs | What becomes possible after | Explicitly out of scope | Exit criteria (مختصر — التفصيل في التصميم) | Top risks | Open decisions |
|---|---|---|---|---|---|---|---|
| 0 | حزمة specs v0.2 + حسم صفوف ترخيص الستاك | هيكل كامل، 36 سقالة، عقود Providers، Compose (فعّال+مطفأ)، Profiles، Health، CI-boundaries، offline tests | بدء أي منطق فوق أساس منقول وآمن | أي منطق أعمال | DoD في تصميم P0 v2.1 (بنوده السبعة) | over-engineering؛ عتاد | صفوف ترخيص الستاك (فئة 2) |
| 1 | P0 منفَّذة + تصميم P1 معتمد | Auth/Org/Permission-spine/Audit-spine + دورة توليد شاشة محكومة + CRUD مدقَّق + Admin shell عربي | بناء أي شاشة/كيان بأمان؛ أساس كل الوحدات | RAG/وسائط/وكلاء/workflows | دورة "تعريف→اعتماد→تطبيق→CRUD" تعمل بالكامل مع deny+audit tests | تعقيد الحوكمة | OD-P1 (انظر تصميمها) |
| 2 | P1 + تصميم P2 | كل أنواع الحقول، RLS/FLS مُنفَّذان، شاشة توثيق التوليد، Entity Profile مبدئي | شاشات إنتاجية معقدة ببيانات معزولة | وكلاء/تكاملات | عزل صف/حقل مُختبر + توثيق كامل لكل توليد | أداء RLS | ملكية entity-profile |
| 3 | P2 + تصميم P3 | Workflow lifecycle كامل + Approvals(SoD) + Actions/CTA + Notifications(+دردشة الإشعار) + Tasks + Projects | أتمتة عمليات المؤسسة باعتماد | تنفيذ عبر LLM | لا تفعيل workflow مستخدم دون اعتماد؛ rollback يعمل | حلقات/أثر واسع | مصفوفة الاعتماد الافتراضية |
| 4 | P3 + تصميم P4 | RBAC+ABAC+ReBAC+Need-to-know+SoD كاملة + Entity Profile كامل + Feature Mgmt + Safe Mode + Security Policies + قائمة A10 | فتح المعرفة بأمان؛ إدارة المزايا دون كسر النظام | وسائط ثقيلة/تكاملات | سياسات مركّبة تُنفَّذ وتُدقَّق؛ استحالة تعطيل أساسي من UI | تصعيد صلاحية | صيغ سياسات ABAC الافتراضية |
| 5 | P4 + بوابات P5 (OCR/PDF/ffmpeg/أوزان-1/مزوّد تخزين عند التفعيل) + تصميم P5 | File Service + فهرسة هجينة محكومة + OCR/docs + صوت/صورة/فيديو-keyframes + OKF + Registry UI + Gateway-min + No-Guessing + RAG-over-media | سؤال المؤسسة عن مستنداتها ووسائطها بأمان | نماذج ثقيلة/فيديو كامل | رفع→معالجة→فهرسة→استرجاع مصفّى + provenance + تبديل نموذج من UI | جودة عربي؛ تسريب كاش | مزوّد التخزين عند التفعيل؛ chunking defaults |
| 6 | P5 + تصميم P6 | Gateway كامل (per-agent selection) + chat module + Safe SQL Agent + Long Reports مسنودة + Validation fail-closed | الإجابة المؤسسية المسنودة كمنتج | تكاملات خارجية | إجابات باستشهاد؛ لا SQL خارج allow-list/RLS؛ تقرير طويل مُستشهَد | حقن/هلوسة | قوالب التقارير الافتراضية |
| 7 | P6 + جرد الأنظمة والعقود (فئة 2) + تصميم P7 | Integration Mgmt + App Store + ربط حسابات/تفويض + بوابات human-in-the-loop + استخدام التطبيقات داخل Chat/Tasks/Workflows/Reports | المنصة تشغّل أنظمة المؤسسة لا تجاورها | SaaS خارجي (proxy لاحقاً) | استدعاء ضمن صلاحية الحساب المربوط + بوابة للأفعال + تدقيق كامل | تنفيذ خطير | نموذج service-accounts التفصيلي |
| 8 | P7 + بوابات الفئة 4 + تصميم P8 | Observability موسّعة (رهن مراجعة) + Ops surface + offline bundle موقّعة + backup/restore مُختبرة + ترقية config-only مُثبتة + HA readiness | تسليم production فعلي داخل شبكة مغلقة | — | استعادة ناجحة من bundle؛ ترقية Local→Prod بالإعداد فقط مُوثّقة | تعقيد تشغيلي | مكوّنات المراقبة النهائية (Legal) |

## 3) تحسينات نطاقية على الخريطة v1.1 (تُعتمد مع هذه الحزمة)
1. **تسمية موسّعة لا تغييرَ ترتيب:** P4 يشمل صراحة Feature Management (كان ضمنياً)؛ P5 باسم Knowledge Foundation؛ P6 باسم Intelligence Layer — المحتوى مطابق للخريطة.
2. **تأكيد قرار الـ Gateway المجزّأ:** الحد الأدنى (embedding/rerank/ASR/OCR routing) في P5، والاكتمال في P6 (كما في v1.1).
3. **بطاقات المهام (T-cards) تُولَّد عند تفعيل كل مرحلة** في جلسة Tasks مستقلة — التصاميم هنا تشمل حتى مستوى **Epics** (Plan skeleton) عمداً، لضبط الحجم ولإبقاء one-task-per-session ممكناً.

## 4) Common Phase Baseline — يَرِثه كل تصميم مرحلة (لا يُكرَّر داخلها)
- **الثوابت:** كل مواد constitution + الستاك D1–D3 (React+Vite+TS+Tailwind+shadcn-style SPA · FastAPI+Pydantic+SQLAlchemy+Alembic · PostgreSQL · Qdrant · OpenSearch · uv+pnpm) + التجريدات (Cache/Queue/Lock=memory/Postgres · ObjectStorage=fs · LLM/Embedding/Reranker/OCR/Vision/MediaProcessing عبر Registry+Gateway فقط).
- **NFRs مشتركة:** stateless api · JSON logs بحقول القسم 10 من coding-standards · fail-fast للإعداد الحرج · RTL/ar-en لكل شاشة (فحص قبول) · لا نداء خارجي وقت التشغيل · lockfiles+digest pinning · معرّفات ASCII.
- **Security مشترك:** default-deny · Permission Gate **قبل** أي retrieval/SQL/API · الثوابت immutable (رقم وظيفي/username/مرجعي) · لا secrets في logs.
- **Audit مشترك:** كل حدث في كتالوج §11 المنطبق على المرحلة + أحداثها الجديدة؛ append-only في PG؛ permission-aware viewer.
- **Testing مشترك:** الأنواع المنطبقة من testing-strategy v1.1 (deny لكل endpoint، audit، migration، profile، flags، boundary-CI، offline، RTL، logging-contract) — تصميم كل مرحلة يضيف الخاص بها فقط.
- **DoD مشترك:** Quality Gates (Methodology §11) + تحديث الوثائق + handoff كامل + لا dependency خارج license-review + بطاقات المهام كلها مقفلة.
- **Coding Agent Prompt المشترك:** قالب موحّد في AGENT_EXECUTION_MODEL.md §6 — كل تصميم يذكر **سطر التخصيص فقط**.

## 5) Dependency &amp; Ordering Rationale (لماذا هذا الترتيب حصراً)
- **لماذا لا RAG قبل P5؟** الاسترجاع المصفّى يفترض RLS/FLS (P2) وسياسات كاملة (P4)؛ فهرسة قبل ذلك = بناء قناة تسريب ثم ترقيعها.
- **لماذا Workflows في P3 لا P1؟** الاعتماد (SoD) يحتاج org/roles/permission-spine ناضجة من P1 وسجلات P2 ليعمل على شيء حقيقي.
- **لماذا access-control hardening في P4 تحديداً؟** بعد وجود شاشات وworkflows حقيقية تُختبر عليها السياسات المركّبة، وقبل فتح المحتوى للفهرسة مباشرة.
- **لماذا Chat/SQL-Agent في P6 لا P5؟** حتى لا يُبنى سطح إجابة فوق فهرس غير مكتمل الحوكمة؛ وSQL الآمن يحتاج allow-list مشتقة من ميتاداتا ناضجة.
- **لماذا Integrations في P7؟** أفعال تغيّر أنظمة خارجية = أعلى خطورة؛ تتطلب بوابات الاعتماد (P3/P4) وسياق الذكاء (P6) وتدقيقاً مكتملاً.
- **لماذا packaging/air-gapped في P8 مع أن الجاهزية من P0؟** الجاهزية (بنية/اختبارات/pinning) تُزرع في P0 وتُختبر كل مرحلة؛ أما **الإثبات النهائي** (bundle موقّعة، استعادة، ترقية config-only على نظام مكتمل) فلا معنى له قبل اكتمال الوظائف.
