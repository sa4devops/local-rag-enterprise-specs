> ⚠️ SUPERSEDED — لا يُستخدم للتنفيذ. المرجع الحالي: حزمة v2.0 (انظر superseded/README.md). تاريخ الوسم: 2026-07-03.

# دراسة معمارية كاملة — منصة تشغيل معرفي مؤسسي تعمل في شبكة مغلقة
## Full Architecture Study (لا كود · لا برومبتات تنفيذ · دراسة وroadmap فقط)

> إعادة تفكير شاملة في المنظومة كمنتج كامل الطبقات، مع احترام القرارات المثبتة في النقاش. الهدف: فهم موحّد + معمارية كاملة + كتالوجات + roadmap عام، لمراجعتها قبل تصميم المرحلة الأولى لاحقاً في محادثة مستقلة.

**فهرس:** ١) فهم موحّد · ٢) ما الذي تغيّر · ٣) قرارات مثبتة · ٤) افتراضات · ٥) نواقص · ٦) المعمارية الكاملة · ٧) الطبقات والخدمات · ٨) Service Catalog · ٩) Module Catalog · ١٠) Agent Catalog · ١١) Screens Catalog · ١٢) Configuration & Profiles · ١٣) إدارة المزايا من الأدمن · ١٤) Deployment/Portability · ١٥) Data · ١٦) Permission · ١٧) Workflow · ١٨) RAG/SQL/Media · ١٩) Model & Provider · ٢٠) MCP/API Integration · ٢١) Audit/Logging/Monitoring · ٢٢) Security & Governance · ٢٣) Roadmap.

---

## 1) فهم موحّد جديد للنظام (Unified Understanding v3)

نبني **منصة تشغيل معرفي مؤسسي كاملة الطبقات** (Enterprise Knowledge Operations Platform)، تعمل في **شبكة مغلقة** داخل Docker، وتُصمَّم مرة واحدة كمنتج قابل للنقل من جهاز التطوير إلى سيرفرات الإنتاج **بتغيير configuration فقط**. النظام **ليس chatbot**، والـ LLM **ليس مصدر الحقيقة**، والواجهة النهائية **واجهة مؤسسية خاصة** تدعم العربية/الإنجليزية وRTL.

النظام **metadata-driven**: الشاشات والحقول والصلاحيات والروابط والمزايا تُعرَّف كبيانات وتُدار من لوحة الأدمن دون تعديل كود. توليد الشاشات وقواعدها يمرّ عبر **خط أنابيب محكوم** (metadata → migration → فحص → اعتماد → تطبيق → versioning → audit → توثيق)، بلا DDL مباشر من نموذج. الحقيقة من: قواعد البيانات + المستندات المعتمدة + الـ APIs الداخلية + السجلات الرسمية. الوكلاء يجلبون البيانات ضمن الصلاحية، والـ LLM يعالج فقط ما يُجلب، ويُمنع التخمين. كل تغيير وكل عملية حرجة تُسجَّل في Audit، مع إعادة تحقق live قبل التعديل/الاعتماد/التصدير.

**الجديد الجوهري:** المنظومة تُصمَّم **كاملة الطبقات والخدمات منذ البداية** (لا حذف لخدمة بحجّة ثقلها على جهاز التطوير)؛ الفرق بين البيئات = إعدادات وأحمال، لا وجود/غياب. ودعم **الوسائط المتعددة (Multimodal/Media)** — مستندات/صور/صوت/فيديو/OCR/vision — **جاهز معمارياً وبرمجياً من البداية** (interfaces + pipeline + registry + gateway)؛ المؤجَّل فقط هو **تشغيل نموذج ثقيل فعلياً** إن لم يكن العتاد مناسباً، ويُضبط ذلك من **Model/Provider Registry** عبر الإعداد لا الكود.

---

## 2) ما الذي تغيّر عن الرد السابق (Deltas)

1. **الوسائط لم تعد مؤجَّلة معمارياً:** كانت "video understanding" ميزة مؤجَّلة؛ الآن **Media/Multimodal** طبقة أولى كاملة (خدمة Media/OCR + Pipeline + Model/Provider Registry + ربط بالـ Gateway + تخزين MinIO + ربط بالمصدر وAudit). المؤجَّل = تشغيل نموذج ثقيل حسب العتاد، عبر الإعداد.
2. **كل الطبقات والخدمات حاضرة في كل profile** (بما فيها التطوير) بإعدادات خفيفة؛ لا حذف خدمات. Local Demo = إثبات end-to-end ببيانات قليلة ونموذج خفيف، لا production load.
3. **توسّع نموذج الإعداد:** فصل **Environment Profiles** (Local/Demo/Staging/Production) عن **Capability Bundles قابلة للتركيب** (Low-resource/Full-stack/Media-enabled/Security-enabled)، لتفادي انفجار عدد الـ profiles. وإضافة خدمات منصّة جديدة: **System Configuration Registry** + **Feature Flag Service** + **Service Registry** + **Deployment/Operations Controller** (رفيع، طبقة عمليات).
4. **حوكمة إدارة المزايا عبر ثلاث طبقات تحكّم (Three Control Planes):** Capability (أدمن) / Configuration (Super Admin) / Operations (عمليات)، مع خدمات أساسية **محميّة** لا تُعطَّل من الواجهة.
5. **إعادة تأطير الـ Roadmap:** المرحلة ٠ صارت **هيكلاً كامل الطبقات (Full-Stack Skeleton)** فيه كل الخدمات حاضرة (خفيفة) + أسس Config/Profile/Feature-Flag/Service-Registry + interfaces للوسائط والنماذج — لا هيكلاً أدنى. **لا برومبتات تنفيذ في هذه المرحلة** (دراسة فقط).
6. **بقيت ثابتة:** قابلية النقل بالإعداد فقط، الواجهة المؤسسية الخاصة بديلاً عن Open WebUI، نموذج `database.docx` بدرجات الفصل الثلاث، التوليد المحكوم بالاعتماد، الصلاحية قبل الاسترجاع، Local Auth مع IdP-adapter، Spec Kit محايد لأي Coding Agent، التصنيف الخماسي.

---

## 3) قائمة القرارات المثبتة (Locked Decisions)

منتج واحد قابل للنقل (config-driven، Twelve-Factor) · الواجهة مؤسسية خاصة (Arabic/English/RTL/white-label)، **لا كود من أي مشروع دون مراجعة ترخيص تجيز التعديل/التوزيع/white-label/الاستخدام المؤسسي/التشغيل المغلق ودون قيود branding أو عدد مستخدمين** · نموذج `database.docx` (platform/apps/integration/reporting + Qdrant/OpenSearch/MinIO/Redis + Neo4j اختياري) بثلاث درجات فصل (Logical/Schema/Physical) · توليد = migrations محكومة بالاعتماد، لا DDL من نموذج، مع شاشة توثيق · معرّفات تقنية آمنة (ASCII) والعربية **labels في الميتاداتا** · صلاحيات RBAC+ABAC+ReBAC + تصنيف خماسي + field/row/screen/action + Least Privilege + Need-to-know + SoD، **تُقيَّم قبل أي استرجاع** و default-deny · الوكلاء مع اختيار model/provider لكل وكيل من قاعدة المنصة دون كود · OKF محلي بدور فهرس/قاموس/مسرد/تعريفات/تعليمات · Local Auth مع IdP-adapter (LDAP/AD/Keycloak/OIDC/SAML لاحقاً) والرقم الوظيفي/اسم المستخدم محميان · Spec Kit، ومخرجات محايدة لأي Coding Agent، وCoding Model منفصل · الكاش تسريع فقط، RAG cache مربوط بالنسخ والصلاحية، إعادة تحقق live · PentAGI/RedAmon أنماط فقط (تكامل أدوات لاحقاً) · **الوسائط مدعومة معمارياً من البداية** · **كل الطبقات والخدمات حاضرة في كل profile** · workflows نوعان مع lifecycle كامل · App Store بمستويين (أدمن تكامل + متجر مستخدم).

---

## 4) قائمة الافتراضات (Assumptions — قابلة للتصحيح)

- تزامن مبدئي مفترض 2–5% من 20–30k مسجّل (≈ 400–1500 متزامن) للتحقق لاحقاً.
- بيئة التطوير: MSI Titan (RTX 5090 Laptop، ~24GB VRAM، 64GB RAM)، مستخدم/مستخدمان، نموذج خفيف يُبدَّل عبر Ollama.
- الإنتاج: عُقد GPU منفصلة (vLLM)، backend متعدد خلف LB، قواعد مُدارة/منسوخة، عناقيد للمخازن.
- الربط أساساً **داخلي**؛ الخارجي اختياري لاحقاً عبر proxy/gateway.
- runtimes: Ollama (تطوير) / vLLM (إنتاج)؛ نماذج مرشحة: Qwen3 / Qwen3-Coder، Qwen2.5-VL (vision)، nomic-embed، bge-reranker، Whisper (صوت)، محرك OCR محلي.
- التخزين S3-compatible عبر MinIO؛ Neo4j معطَّل افتراضياً لكنه حاضر.

---

## 5) قائمة النواقص التي تحتاج قراراً (Open Gaps)

لا تُعطّل الدراسة، وتُحسم كإعدادات/قياسات لاحقاً: العدد المتزامن الفعلي · عتاد الإنتاج النهائي · الأحجام النهائية (إدارات/شاشات/مستندات/سجلات/متجهات) · جرد الأنظمة الداخلية وعقودها (API/MCP) · الـ IdP المحدَّد وخريطة الصفات · مصفوفات الاعتماد وقواعد SoD التفصيلية · النماذج المعتمدة لكل نوع وسائط + سياسة تشغيلها حسب العتاد · نهج TLS/PKI وسياسات الاحتفاظ/النسخ الاحتياطي داخل الشبكة المغلقة · هل يُعتمد Graph module في الإنتاج · نطاق أدوات الأمن (PentAGI/RedAmon) إن أُدمجت.

---

## 6) المعمارية الكاملة (Full Architecture)

راجع **`Full_Stack_Architecture.svg`** (كل الخدمات حاضرة مع حالات core/optional). ثماني طبقات داخل حدود مغلقة + مستوى عمليات (Operations) منفصل + شريط عرضي دائم:

1. **Presentation** — Enterprise UI (Admin Console + User Workspace + Chat + Screen/Field/Workflow Builders + App Store + i18n/RTL/white-label).
2. **API / Application** — Backend (FastAPI, stateless): Auth، Authorization، Metadata، Records، Migration/Generation، Workflow، Integration، Media/OCR، RAG، Reports، Notifications، App Store، Config/Profile، Feature-Flags، Service-Registry، LLM-Gateway-Client.
3. **Orchestration & Agents** — Orchestrator/Router + الوكلاء (worker layer قابل للتوسع).
4. **Knowledge & Models** — OKF (فهرس/قاموس) + Model/Provider Registry + LLM Gateway → Ollama/vLLM (نصوص/كود/vision/embed/rerank/transcription/OCR/multimodal).
5. **Media Processing** — pipeline الوسائط (استيعاب/كشف نوع/توجيه/معالجة/فهرسة) مربوط بالـ Gateway والـ Registry.
6. **Data & Storage** — PostgreSQL (4 قواعد) + Qdrant + OpenSearch + MinIO + Redis (+ Neo4j اختياري).
7. **Connectors** — MCP / Internal API / Webhook / DB Connectors → الأنظمة الداخلية.
8. **Cross-Cutting** — Audit · Cache · Monitoring/Health · License · Hardware/Runtime Manager · Security/Policy · Configuration/Feature-Flags/Service-Registry.
- **Operations Plane (منفصل، عمليات فقط):** Deployment/Operations Controller · lifecycle الخدمات · النقل/الترقية · النسخ الاحتياطي/الاستعادة · TLS/secrets.

**القاعدة الذهبية:** الصلاحية قبل أي استرجاع/SQL/API؛ الـ LLM يعالج فقط ما جلبه الوكيل؛ العمليات الحرجة تُعيد التحقق live؛ كل خدمة **حاضرة** حتى لو قدرتها مُعطَّلة بعلم (flag).

---

## 7) جميع الطبقات والخدمات (Layers & Services Overview)

**مبدأ حاكم:** «الطبقة حاضرة حتى لو الميزة غير مفعّلة» — الحضور = وجود الخدمة + interface + pipeline + registry؛ التعطيل = flag مطفأ لا كود غائب. في التطوير تعمل كل الخدمات بإعدادات demo (بيانات قليلة، نموذج خفيف، replica واحدة، Neo4j مطفأ). في الإنتاج نفس الخدمات بأحمال وعناقيد أكبر عبر الإعداد.

---

## 8) Service Catalog

| الخدمة | الغرض | الحالة | يعتمد على |
|---|---|---|---|
| Enterprise UI | واجهة المستخدم والأدمن | Core | Backend API |
| Backend API (FastAPI) | مدخل API والتنسيق | Core | Postgres, Redis |
| Auth/Identity | مصادقة + IdP-adapter | Core (محميّة) | platform_db |
| Authorization/Permission | محرّك الصلاحيات | Core (محميّة) | platform_db |
| Metadata Service | تعريفات شاشات/حقول/تطبيقات | Core | platform_db |
| Records/CRUD | عمليات بيانات الكيانات المولّدة | Core | apps_db |
| Migration/Generation | توليد DB/شاشات محكوم بالاعتماد | Core | platform_db, apps_db |
| Workflow Service | محرك دورة حياة الـ workflows | Core | platform_db |
| Integration Service | MCP/API/Webhook/DB connectors | Core (قدرات flaggable) | integration_db |
| Media/OCR Service | pipeline الوسائط | Core (قدرات flaggable) | MinIO, Gateway, Registry |
| RAG/Retrieval | فهرسة + بحث هجين | Core | Qdrant, OpenSearch |
| SQL Agent Service | SQL آمن للقراءة فقط | Core | apps_db (RLS) |
| Orchestrator + Agents | تنسيق ووكلاء | Core | Redis (queue), Gateway |
| LLM Gateway | تجريد توجيه النماذج | Core | Ollama/vLLM |
| Model/Provider Registry | كتالوج النماذج + خريطة المهام | Core | platform_db |
| Report Service | تقارير طويلة/تصدير | Core | reporting_db |
| Notification Service | إشعارات + دردشة لكل إشعار | Core | platform_db |
| App Store Service | متجر المستخدم + ربط الحسابات | Core (قدرات flaggable) | integration_db |
| Audit Service | تدقيق append-only | Core (محميّة) | platform_db |
| Configuration/Profile (Config Registry) | إعدادات + profiles | Core (محميّة) | platform_db |
| Feature Flag Service | أعلام القدرات | Core (محميّة) | platform_db |
| Service Registry | كتالوج/صحة/تبعيات الخدمات | Core (محميّة) | – |
| Deployment/Operations Controller | lifecycle/ترقية (طبقة عمليات) | Core (Ops-only) | orchestrator |
| Monitoring/Health | Prometheus/Grafana/Loki + /health | Core | كل الخدمات |
| PostgreSQL (×4) / Qdrant / OpenSearch / MinIO / Redis | بيانات وتخزين وبحث وكاش/طابور | Core | – |
| Neo4j / Graph | علاقات ورسم بياني | Optional (off by default، حاضر) | – |

---

## 9) Module Catalog (مزايا أعمال قابلة للتفعيل عبر flags)

Identity & Org · Authorization · Screen/Field Builder · Records · Workflow Builder · Tasks · Projects · Notifications · Chat · Knowledge/RAG · **Media/Multimodal** · Data Query (SQL) · Reports · App Store · Integration Management · Model/Provider Management · Media/OCR Settings · Feature/Module Management · Configuration/Profiles · Audit Viewer · Monitoring/Health · About/Licenses · Graph/Relationship (optional) · Security Tools (مستقبلي؛ نمط PentAGI/RedAmon داخل المتجر لفريق الأمن/CERT).

**قاعدة:** المزايا تُفعَّل/تُعطَّل كـ **capability flags**؛ الوحدات الأساسية (Auth/Authorization/Audit/Config/Metadata/DB) **محميّة** لا تُعطَّل من الواجهة.

---

## 10) Agent Catalog

Orchestrator/Router (تصنيف/سياق/Permission Gate/No-Guessing) · Retrieval (بحث هجين + rerank) · SQL (read-only, schema+RLS) · Validation (grounded/citations/classification) · Reasoning (تركيب من البيانات فقط) · Security/Policy (سياسات/PII/بوابات تنفيذ) · **Media/Multimodal group**: OCR/Doc · Vision · Audio/Transcription · Video (keyframes + توجيه لنموذج فيديو عند توفّره) · API-Integration (أدوات MCP/APIs ضمن الصلاحية + بوابات اعتماد) · Report (تقارير قسماً قسماً) · Admin/Metadata (يولّد مخرجات للمراجعة، لا يطبّق).

**لكل وكيل** model/provider قابل للضبط من Registry دون كود؛ human-in-the-loop على أي إجراء يغيّر حالة.

---

## 11) UI / Admin / User Screens Catalog

**Admin Console:** Dashboard · Users · Organization (Sectors/Departments) · Roles & Permissions · Data Classification · Screen Builder · Field Builder · Generation/Migration Review & Approval · Generation Documentation · Workflow Builder & Approvals · Integration Management (MCP/API/Connectors) · Model & Provider Management · Media/OCR Settings · **Feature/Module Management (flags)** · **Configuration & Profiles** · Service Registry & Health · Audit Viewer · Reports Admin · App Store Admin (نشر التطبيقات) · License/About.

**Operations Surface (عمليات فقط، منفصلة):** Deployment/Service Lifecycle · Profile Promotion · Backup/Restore · Secrets/TLS.

**User Workspace:** Home/Dashboard · Dynamic Screens (CRUD) · Records · Entity Profile · Chat (أوامر LLM طبيعية) · Tasks · Projects · Notifications (بدردشة لكل إشعار) · App Store · Reports/Export · Profile/Settings · About.

**عام:** Enterprise-grade، RTL/LTR، Action/CTA buttons، Wizards للعمليات المعقّدة، white-label theming.

---

## 12) Configuration & Profiles Architecture

**بُعدان منفصلان (لتفادي انفجار الـ profiles):**
- **Environment Profile (واحد نشط):** Local · Demo · Staging · Production — يضبط endpoints/الموارد/الأسرار/TLS/replicas.
- **Capability Bundles (قابلة للتركيب):** Low-resource · Full-stack · Media-enabled · Security-enabled — presets لأعلام القدرات تُركَّب فوق البيئة. مثال: `Local + Low-resource + Media-enabled (نماذج خفيفة)`.

**System Configuration Registry (في platform_db):** المصدر الموحّد للإعداد الفعّال + الأعلام + تعريفات الـ profiles/bundles، **مُؤرشَف (versioned) ومدقَّق**، مع API وشاشة أدمن. تمييز: **إعداد static** (يُقرأ عند الإقلاع، يحتاج إعادة تشغيل) مقابل **dynamic** (runtime، يتغيّر حياً عبر Registry).

**Feature Flag Service:** يحلّ الأعلام بنطاقات (global/module/capability) وحسب (environment/profile/role) مع أعلام **محميّة**. **Service Registry:** كتالوج الخدمات + صحتها + تبعياتها + endpoints (من الإعداد) + حالة (core/optional/disabled) — يغذّي شاشة الصحة وحُرّاس التبعية.

**هرمية الإعداد:** defaults → environment profile → capability bundles → runtime overrides (Registry) → secrets، مع **تحقّق fail-fast** عند الإقلاع.

راجع **`Config_Profiles_Admin.svg`**.

---

## 13) إدارة المزايا من الأدمن (Admin-Controlled Feature/Module Management)

**التوصية: ثلاث طبقات تحكّم (Three Control Planes)** بفصل واضح للمسؤوليات:

- **Capability Plane — App Admin:** تفعيل/تعطيل **قدرات/مزايا** عبر feature flags (Media، Graph، Connector معيّن، RAG، Reports، تفعيل وكيل، تطبيق في المتجر). **لا تهدم بنية تحتية**؛ الأعلام المحميّة مستثناة.
- **Configuration Plane — Super Admin:** قيم Config Registry، defaults الـ profiles، endpoints منطقية للمزوّدين، إعدادات السياسات/التصنيف. **versioned + audited**.
- **Operations Plane — Operations/Ops:** **lifecycle الخدمات** (تشغيل/إيقاف/scale)، الحاويات/التنسيق، TLS/secrets، النسخ/الاستعادة، ترقية/تبديل الـ profile — عبر **سطح عمليات + orchestrator، لا واجهة الأدمن العادية**.

**إجابات أسئلتك (تحليلاً لا افتراضاً):**
1. **ما يُفعَّل/يُعطَّل من الأدمن:** المزايا على مستوى **القدرة** (flags) — Media/Graph/Connectors/RAG/Reports/وكلاء/تطبيقات المتجر.
2. **ما يقتصر على Super Admin/Operations:** endpoints البنية، الموارد، replicas، lifecycle الحاويات، TLS/secrets، ترقية الـ profile، النسخ الاحتياطي.
3. **تعطيل Media/Graph/Connector؟** نعم على مستوى **القدرة (flag)** — تُخفى/تُمنع القدرة، والخدمة قد تبقى تعمل مبوّبة. للاختياري المطفأ (Neo4j) التفعيل = flag + ضمان توفّر الخدمة (شأن عمليات إن لم تكن مُشغّلة).
4. **تعطيل خدمة كاملة أم قدرة؟** من الواجهة: **قدرة (flag)** لا حاوية. lifecycle الحاويات **شأن عمليات** (Deployment Controller/orchestrator) لتفادي كسر البنية، ولأن المنسّق يملك دورة الحياة في الإنتاج.
5. **الحماية من تعطيل خدمة أساسية بالخطأ:** وسم الخدمات الأساسية **protected/essential** بلا زر تعطيل في الواجهة إطلاقاً + **رسم تبعيات** (يمنع تعطيل X إن اعتمد عليه Y) + تأكيد + سبب + قاعدة موافقة ثنائية للحساسة + **Safe Mode** يمنع تعطيل الأسس (Auth/Permission/Audit/Config/DB).
6. **تسجيل كل تغيير:** كل تغيير إعداد/علم/profile يمرّ عبر Config Service → تحقّق → تطبيق → **Audit** (من/ماذا/قديم→جديد/متى/سبب) + إصدار قابل للـ rollback.
7. **profiles دون كود:** حزم إعداد مسمّاة (env + defaults أعلام + موارد) تُختار بالإعداد؛ لا فروع كود.
8. **الانتقال بين profiles:** تغيير الـ profile النشط → إعادة تشغيل/إعادة نشر للإعدادات static؛ الأعلام dynamic تتغيّر حياً عبر Registry. الترقية تنسخ نفس الصور وتبدّل حزمة الإعداد.
9. **System Configuration Registry؟** **نعم** (ضروري) — مركزي، versioned، مدقَّق، بـ API وواجهة.
10. **Feature Flag Service؟** **نعم** — طبقة فوق الـ Registry بنطاقات وأعلام محميّة.
11. **Service Registry؟** **نعم** (خفيف) — كتالوج/صحة/تبعيات؛ يتكامل مع اكتشاف المنسّق في الإنتاج.
12. **Deployment Controller؟** **نعم لكن رفيع وفي طبقة العمليات** — يجرّد lifecycle والترقية؛ الحاويات تبقى بيد المنسّق (compose/K8s/systemd). مبدئياً scripts + شاشة حالة؛ متكامل لاحقاً.
13. **تشغيل/إيقاف الحاويات من الواجهة؟** **لا** — طبقة العمليات فقط (فصل مسؤوليات + نطاق أثر + المنسّق يملك الحياة). الأدمن: أعلام قدرات + عرض صحة للقراءة فقط؛ Ops/Super-Admin: lifecycle عبر سطح مخصّص، والكل مدقَّق.

---

## 14) Deployment / Portability Architecture

**غير قابل للتفاوض:** نفس الكود/الـ repo/الصور ينتقل بتغيير **إعداد فقط** (env/config/resources/model-selection/provider-endpoints/paths/hosts/workers/secrets/TLS/backup/monitoring/profile). **لا** إعادة كتابة كود، لا معمارية إنتاج مختلفة، لا fork.

**آليات:** Twelve-Factor · صورة واحدة لكل خدمة تُبنى مرة · `docker-compose.yml` + `override` (dev) + `prod` (replicas/resources/TLS/endpoints خارجية) + `.env.*` · طبقات تجريد قابلة للتبديل بالإعداد (LLM Provider، Identity Provider، Object Storage، Database Router، Media Processor) · backend عديم الحالة (جلسات Redis/JWT) → توسّع أفقي · workers مستقلة · inference على عُقد GPU منفصلة يُشار إليها بالإعداد · نفس migrations في كل البيئات · **النقل المغلق:** حزمة offline (images + wheels + models) + استعادة + تحقق. (راجع `Deployment_Architecture.svg` من الحزمة السابقة — ما زال صالحاً؛ يُضاف إليه بُعد الـ Capability Bundles أعلاه.)

---

## 15) Data Architecture

**القواعد الأربع:** `platform_db` (ميتاداتا/حوكمة/صلاحيات/تعريفات/registry نماذج/إعداد/أعلام/audit) · `apps_db` (بيانات التطبيقات، **schema-per-app/domain**، أعمدة `department_id/sector_id/owner_user_id/classification` + تدقيق) · `integration_db` (تسجيل الأنظمة/ربط الحسابات/رموز مُعمّاة/سجلات) · `reporting_db` (قراءة تحليلية، قابلة لـ read-replica).

**درجات الفصل الثلاث (معاً):** Logical (RLS/FLS + ملكية + تصنيف + Need-to-know) · Schema (لكل تطبيق/domain) · Physical (نقل تطبيق حسّاس لقاعدة مستقلة **بتغيير endpoint في الإعداد**؛ الكود يستخدم Database Router ولا يفترض قاعدة واحدة).

**المخازن:** Qdrant (متجهات، quantization/sharding) · OpenSearch (نصي/BM25 + سجلات) · MinIO (ملفات/وسائط، S3-compatible، erasure coding إنتاجاً) · Redis (كاش تسريع + طابور + جلسات) · Neo4j (اختياري).

**التوليد/الترحيل:** تعريف (metadata) → مولِّد migration → فحص تعارض + مخاطر → **اعتماد** → تطبيق داخل schema → versioning → audit → **شاشة توثيق**. **معرّفات تقنية ASCII، والعربية labels في الميتاداتا**. لا DDL من نموذج.

**Sizing:** dev خفيف (نموذج واحد يُبدَّل، corpus صغير، replica واحدة)؛ production عناقيد + PgBouncer + read replicas + عُقد GPU. القياسات المطلوبة: ذروة التزامن، رموز/طلب، حجم/عدد المستندات، عدد المتجهات، QPS، نمو السجلات — كلها إعداد لا كود.

---

## 16) Permission Architecture

**تُقيَّم قبل أي استرجاع، default-deny في كل خطوة، بترتيب دفاع متعمّق:** Authentication → RBAC → ABAC → ReBAC → Data Classification (تصريح ≥ تصنيف + Need-to-know) → Row-Level → Field-Level → Screen/Action-Level → SoD → Least Privilege.

**نقاط الإنفاذ:** middleware في الـ API (خشن) → **Permission Gate** في الـ Orchestrator (قبل الاسترجاع) → **query builder** يحقن RLS/FLS → **Answer engine** يخفي الحقول → **Audit** يسجّل القرار (allow/deny + السياسة). كل السياسات **بيانات في platform_db** (role_permissions/abac_policies/classification_levels/field_policies/screen_permissions/sod_rules)، قابلة للتحرير من الواجهة، versioned + مدقَّقة. **كاش:** مفتاح RAG يشمل نطاق الصلاحية + نسخ المستند/الفهرس/السكيم؛ إعادة تحقق live قبل الحرِج.

---

## 17) Workflow Architecture

**نوعان:** (١) يبنيها الأدمن أو تعتمد على ربط مسبق. (٢) ينشئها المستخدم، **ولا تتفعّل إلا بعد approval** من Manager/مدير النظام/المخوّل.

**دورة الحياة الكاملة:** `Draft` → `Validation` (سلامة التعريف) → `Permission Check` (صلاحيات المنشئ/الخطوات) → `Risk Check` (تصنيف/تعارض/أثر) → `Approval` (مخوّل، مع SoD: منشئ ≠ معتمِد) → `Activation` → `Versioning` (كل تعديل نسخة) → `Rollback` (العودة لنسخة سابقة) → `Audit` (كل انتقال مسجَّل). محرك الـ workflow يمرّ كل خطوة عبر Permission + Audit، ويدعم الربط بالشاشات/الإجراءات/الإشعارات/التطبيقات. (يمكن لاحقاً إضافة مخطط حالة مرئي.)

---

## 18) RAG / SQL / Media Architecture

**RAG:** استيعاب مستند → (OCR إن مسحوب) → تقطيع → embedding → فهرسة (Qdrant + OpenSearch) → بحث هجين → rerank → مقاطع **مصفّاة بالصلاحية** مع provenance → No-Guessing إن نقصت الأدلة. طبقة OKF تغذّي السياق (تعريفات/مسرد/تعليمات).

**SQL:** قراءة فقط، مقيّد بالسكيم والصلاحيات؛ SELECT مُعامَل ضمن allow-list + RLS؛ لا DDL/DML؛ يعيد الصفوف + الاستعلام للتدقيق.

**Media/Multimodal (جاهز معمارياً من البداية):** راجع **`Media_Pipeline.svg`**. `استيعاب (رفع إلى MinIO)` → `كشف النوع` → `توجيه عبر Model/Provider Registry + LLM Gateway`:
- **مستندات (PDF/Office/نص):** استخراج/OCR → تقطيع → embedding → فهرسة.
- **صور:** نموذج vision (وصف/OCR/تصنيف).
- **صوت:** transcription (Whisper) → نص → تلخيص/فهرسة.
- **فيديو:** استخراج صوت→transcription + keyframes→vision؛ **نموذج فهم فيديو كامل قابل للتوصيل عبر Registry** (تشغيله مؤجَّل حسب العتاد، والـ pipeline/interface حاضر).
- **Multimodal LLM:** يُوجَّه عبر Gateway.
كل نتيجة **مربوطة بالمصدر + التصنيف + Audit**، مخزّنة/مفهرسة بـ provenance، ومفحوصة بالصلاحية عند الاسترجاع. **اختيار النموذج لكل نوع وسائط من شاشة الأدمن دون كود.**

---

## 19) Model & Provider Architecture

**Model/Provider Registry (في platform_db):** كتالوج نماذج {الاسم، النوع: reasoning/coder/vision/embed/rerank/transcription/ocr/multimodal، المزوّد: Ollama/vLLM/غيره، endpoint، parameters، enabled} + **خريطة مهمة→نموذج** (embedding→nomic، rerank→bge، vision→Qwen2.5-VL، transcription→Whisper، reasoning→Qwen3…) + **تجاوزات لكل وكيل**. **LLM Gateway** يحلّ النموذج وقت التشغيل حسب المهمة/الوكيل. تغيير أي نموذج/مزوّد **من الواجهة عبر الإعداد لا الكود**. يدعم نماذج خفيفة في التطوير وثقيلة/موزّعة في الإنتاج. **Hardware/Runtime Manager** يراقب الموارد ويمنع تحميلاً يتجاوز العتاد.

---

## 20) MCP / API Integration Architecture

**مستويان:** (١) **Admin Integration Management** لإدارة الربط الفني (MCP servers / Internal APIs / Webhooks / DB connectors): تسجيل، اعتماد، اختبار اتصال، سياسات، تفعيل/تعطيل قدرة. (٢) **Enterprise App Store** للمستخدم: يرى **فقط** المسموح، يربط حسابه/يفوّض عند الحاجة، ويستخدم التطبيق داخل **Chat/Tasks/Workflows/Reports/Notifications**. الاستدعاءات ضمن صلاحيات الحساب المربوط + **بوابات اعتماد** لأي إجراء يغيّر حالة + تسجيل كامل في Audit. الربط أساساً داخلي؛ الخارجي اختياري لاحقاً عبر proxy/gateway.

---

## 21) Audit / Logging / Monitoring Architecture

**Audit** append-only في platform_db: يُستدعى في كل تغيير/عملية حرجة + **قرار الصلاحية** (allow/deny + السياسة) + تغييرات الإعداد/الأعلام/الـ profile + توليد/ترحيل + استخدام التطبيقات + معالجة الوسائط (مع الربط بالمصدر). **Logging:** سجلات منظّمة (JSON) تُجمع في Loki/OpenSearch. **Monitoring/Health:** Prometheus (مقاييس) + Grafana (لوحات) + `/health` لكل خدمة (اتصال القواعد/التخزين/الكاش/البحث/الـ Gateway) + Service Registry (حالة/تبعيات). تنبيهات موارد عبر Hardware/Runtime Manager.

---

## 22) Security & Governance

Air-gapped بلا اعتماد سحابي وقت التشغيل · default-deny وصلاحية قبل الاسترجاع · تصنيف خماسي + Need-to-know + SoD · معرّفات تقنية آمنة · أسرار/TLS في طبقة العمليات لا الواجهة · خدمات أساسية محميّة + Safe Mode + رسم تبعيات · كل تغيير مدقَّق وقابل للـ rollback · No-Guessing Guard + Validation (استشهادات) لمنع اعتماد هلوسة كحقيقة · **مراجعة تراخيص** لأي كود خارجي (لا Open WebUI المقيّد بالعلامة v0.6.6+؛ OKF محلي فقط) + صفحة About/attribution · كاش تسريع فقط بمفاتيح تراعي الصلاحية + إعادة تحقق live · بوابات human-in-the-loop لأي إجراء يغيّر حالة أو يستدعي نظاماً خارجياً · حزمة offline موقّعة/متحقَّقة للنقل والتحديث.

---

## 23) Roadmap عام للمراحل (بدون كود وبدون برومبتات تنفيذ)

> لكل مرحلة: **الهدف · ما يُبنى · ما لا يُبنى · المخرجات · شروط القبول**. الترتيب قابل للنقاش عند تصميم كل مرحلة لاحقاً.

### Phase 0 — Foundation & Full-Stack Skeleton
- **الهدف:** إثبات أن المنظومة **كاملة الطبقات** تقلع end-to-end وتتصل خدماتها، وأنها config-driven وقابلة للنقل.
- **يُبنى:** repo + Spec Kit (constitution) + Docker Compose + Environment Profiles + Capability Bundles + **Config Registry + Feature Flag + Service Registry (حد أدنى)** + كل الخدمات الأساسية حاضرة بإعدادات demo (بما فيها Media/OCR وModel/Provider Registry كسقالة، Neo4j مطفأ) + interfaces (LLM/Identity/Storage/DB-Router/Media) + Health/Monitoring.
- **لا يُبنى:** أي منطق أعمال، صلاحيات فعلية، شاشات، وكلاء يعملون، نماذج ثقيلة.
- **المخرجات:** منظومة تقلع بكل الخدمات + `/health` أخضر + تبديل profile/bundle بالإعداد + سجل خدمات/أعلام.
- **القبول:** إقلاع كامل ببروفايل Local؛ تبديل إلى Production يغيّر السلوك بالإعداد فقط؛ الخدمات كلها حاضرة (بعضها مبوّب بعلم)؛ لا منطق أعمال.

### Phase 1 — Governed Core + Screen Builder (Walking Skeleton)
- **الهدف:** إثبات التوليد المحكوم للشاشات/القواعد تحت الحوكمة end-to-end.
- **يُبنى:** Local Auth (IdP-adapter) + Org + Permission spine (مُنفَّذة) + Metadata Registry + Audit spine + شريحة باني الشاشات (تعريف→migration→اعتماد→تطبيق→CRUD) + Capability flags + قشرة Enterprise UI (RTL).
- **لا يُبنى:** RAG/Media/وكلاء/LLM، workflow كامل، RBAC/ABAC/ReBAC كامل، متجر/تكاملات، تقارير.
- **المخرجات:** دورة توليد شاشة محكومة كاملة + CRUD مدقَّق + منع بلا صلاحية.
- **القبول:** كل خطوة تمرّ ببوابة الصلاحية وتُسجَّل؛ لا DDL من نموذج؛ RTL صحيح.

### Phase 2 — Full Screen/Field Builder + Records Engine
- **الهدف:** نضج بناء الشاشات وإنفاذ RLS/FLS.
- **يُبنى:** كل أنواع الحقول/التحققات، إنفاذ Row/Field-Level، خط توليد أغنى، شاشة توثيق كاملة.
- **لا يُبنى:** الوكلاء/الوسائط/التكاملات.
- **المخرجات/القبول:** بناء شاشات معقّدة تعمل مع عزل صفوف/حقول مدقَّق.

### Phase 3 — Workflow Engine + Actions + Notifications
- **الهدف:** دورة حياة الـ workflows الكاملة (نوعان).
- **يُبنى:** Draft→Validation→Permission→Risk→Approval→Activation→Versioning→Rollback→Audit + Action Buttons + Notification Service (بدردشة لكل إشعار).
- **المخرجات/القبول:** workflow ينشئه مستخدم لا يتفعّل إلا بعد اعتماد؛ rollback يعمل؛ كل انتقال مدقَّق.

### Phase 4 — Full Authorization + Admin Feature Management
- **الهدف:** نموذج الصلاحيات الكامل + حوكمة المزايا.
- **يُبنى:** RBAC+ABAC+ReBAC + field/row-level + SoD + Entity Profile + شاشة Feature/Module Management (flags) + Safe Mode + رسم تبعيات.
- **المخرجات/القبول:** سياسات مركّبة تُنفَّذ وتُدقَّق؛ تعذّر تعطيل خدمة أساسية من الواجهة.

### Phase 5 — Knowledge & Media (RAG + Multimodal)
- **الهدف:** المعرفة والوسائط جاهزة ومفعّلة (نماذج خفيفة).
- **يُبنى:** RAG/Retrieval + Document/OCR + **Media pipeline (صوت/صور/فيديو-keyframes)** + OKF layer + **Model/Provider Registry UI** + LLM Gateway + وكلاء (Retrieval/Validation/Reasoning/Media) + No-Guessing.
- **لا يُبنى:** نماذج ثقيلة إن لم يناسب العتاد (تبقى قابلة للتوصيل عبر Registry).
- **المخرجات/القبول:** رفع مستند/صوت/صورة → معالجة → فهرسة → استرجاع مصفّى بالصلاحية مع provenance؛ تبديل نموذج نوع وسائط من الواجهة.

### Phase 6 — Data Query & Reasoning + Chat + Reports
- **الهدف:** استعلام آمن وتقارير ودردشة مؤسسية.
- **يُبنى:** Safe SQL Agent + Reasoning/Report agents + تقارير طويلة قسماً قسماً/تصدير + Chat في Enterprise UI.
- **المخرجات/القبول:** إجابات مسنودة بالمصدر؛ SQL قراءة فقط ضمن الصلاحية؛ تقرير طويل مُستشهَد.

### Phase 7 — Integration & App Store
- **الهدف:** الربط الداخلي والمتجر.
- **يُبنى:** Integration Management (MCP/API/Webhook/DB) + Enterprise App Store + ربط حسابات + استخدام التطبيقات في Chat/Tasks/Workflows/Reports/Notifications + بوابات اعتماد.
- **المخرجات/القبول:** المستخدم يرى المسموح فقط ويستخدم تطبيقاً داخل الدردشة/المهام ضمن الصلاحية، مع تدقيق كامل.

### Phase 8 — Operations, Scale & Hardening
- **الهدف:** جاهزية الإنتاج والتوسع.
- **يُبنى:** Monitoring/observability كامل + **Deployment/Operations Controller** (طبقة عمليات) + حزمة offline/backup/restore + HA/تحمّل + Graph module (اختياري) + أدوات أمن (اختياري، نمط PentAGI/RedAmon في المتجر).
- **المخرجات/القبول:** ترقية Local→Production بالإعداد فقط؛ نسخ/استعادة متحقَّقة؛ lifecycle عبر طبقة العمليات لا الأدمن.

**ملاحظة:** لن أُخرج برومبتات تنفيذية لأي مرحلة الآن. عند طلبك، نصمّم **المرحلة الأولى وحدها** في محادثة مستقلة.
