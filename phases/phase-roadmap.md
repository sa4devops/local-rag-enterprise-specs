# phase-roadmap.md — خريطة مراحل المشروع الكاملة

> **Document Title:** Phase Roadmap · **Version:** 1.1 (D1–D9 مدمجة) · **Status:** Current / Accepted · **Date:** 2026-07-04
> **Authority Order:** المرتبة 5 (بعد Open-Decisions وقبل تصاميم المراحل) — **المرجع المُلزم الوحيد لترتيب المراحل ونطاقها العام**؛ تفاصيل كل مرحلة في وثيقة تصميمها.
> **Related:** constitution.md · Methodology · Catalog · open-decisions.md · phases/
> **Purpose:** خريطة تنفيذية عامة من Phase 0 إلى Phase 8 + Backlog، ليعرف المالك وأي Coding Agent أين تبدأ كل مرحلة وأين تنتهي.

**قواعد عامة:**
- كل مرحلة تمرّ بدورتين منفصلتين: **تصميم** (Vision→Specify→Clarify→Plan→Tasks في محادثة مستقلة، بلا كود) ثم **تنفيذ** لاحق بأي Coding Agent وفق المنهجية. **لا تنفيذ لمرحلة قبل اعتماد تصميمها، ولا تنفيذ لمرحلة قبل استيفاء DoD المرحلة السابقة.**
- تُسمّى المراحل دائماً **بالرقم + الاسم**.
- **Handoff requirement موحّد لكل المراحل:** لا تُغلق أي جلسة/مرحلة دون تحديث `handoff/handoff.md` (المنجز/غير المنجز/الملفات/القرارات/المخاطر/الاختبارات/الخطوة التالية/ما لا يُلمس) + أرشفة نسخة في `handoff/archive/`.
- **تعديل نطاقي وحيد مُبرَّر** عن التسمية الأولية: **الحد الأدنى من LLM Gateway** (توجيه embedding/reranking/transcription/OCR) يدخل **Phase 5** لأن RAG وMedia لا يعملان بدونه؛ **اكتمال** الـ Gateway (per-agent model selection UI + وكلاء التفكير + Chat) في **Phase 6**. لا تغيير آخر على الترتيب.
- **قرارات ما قبل التنفيذ (D1–D9، 2026-07-04) مدمجة:** الستاك (React+Vite / FastAPI / uv+pnpm) · التجريدات الثلاث بافتراضي memory/PostgreSQL · التخزين filesystem-أولاً · الخط الرقابي الأساسي · GitHub-الآن مع نقل مغلق موقّع — التفاصيل الملزمة في open-decisions.md وcoding-standards.md.
- **الهوية المعتمدة (v1.0-baseline):** Enterprise AI Platform with Progressive Implementation — المنصة هي المنتج؛ التنفيذ والتفعيل مرحليان (constitution م22).
- **قالب «التزام معماري مستقبلي» (Future Architecture Commitment — موحَّد):** كل قدرة مؤجلة تُوثَّق بخمسة حقول: **الحدود** (boundary) · **العقود المتوقعة** (expected contracts) · **التبعيات** · **القرارات المؤجلة المسماة** · **مرحلة التفعيل**. بنود القدرات المؤجلة في هذه الخريطة (الجدول ب والصف B) تُقرأ وتُستكمل وفق هذا القالب — لا تُبنى قبل مرحلتها ولا يُحذف موطؤها (م22 وسلّم الجاهزية في agent-execution-model §10/§11).

---

## الجدول أ — الهوية والترتيب

| # | الاسم | الهدف | لماذا قبل التالية | الحالة الآن | Blockers |
|---|---|---|---|---|---|
| 0 | Foundation &amp; Full-Stack Skeleton | أساس مفروض تقنياً: repo/حدود/إعداد/كل الطبقات حاضرة (خفيفة) وقابلة للنقل | لا شيء يُبنى بأمان بلا أساس portable بحدود مفروضة | **التصميم معتمد** (`phases/phase-0-foundation-full-stack-skeleton.md` v2.1) · التنفيذ لاحقاً | لا للتصميم؛ قبل التنفيذ: صفوف ترخيص الستاك المعتمد (فئة 2)؛ **لا بوابة فئة 3 على P0.4** — تنطبق فقط عند تفعيل صورة اختيارية (Valkey/MinIO|SeaweedFS/monitoring-server) |
| 1 | Governed Core + Screen Builder | إثبات جوهر المشروع تحت الحوكمة end-to-end (Walking Skeleton) | الحوكمة والميتاداتا أساس كل ما بعدها؛ أعلى مجهولية تقنية تُثبت مبكراً | تصميم لاحق (المحادثة المستقلة التالية) | لا (فئة 1 فارغة) |
| 2 | Advanced Screen / Records / Initial Entity Profile | نضج بناء الشاشات وإنفاذ RLS/FLS + Entity Profile مبدئي | بيانات محكومة العزل قبل بناء العمليات فوقها | تصميم لاحق | لا |
| 3 | Workflows + Approvals + Action Buttons | دورة حياة العمليات (النوعان) + Notifications/Tasks/Projects | العمليات والاعتمادات قبل إدخال المعرفة/الذكاء | تصميم لاحق | لا |
| 4 | Advanced Permissions + Full Entity Profile | نموذج الصلاحيات الكامل + حوكمة المزايا (Feature Mgmt) | ضبط الوصول نهائياً قبل فتح المعرفة والأنظمة | تصميم لاحق | لا |
| 5 | RAG + Files + OCR + Media Pipeline | تفعيل المعرفة والوسائط (نماذج خفيفة) + OKF + Registry UI + **حد أدنى من الـ Gateway** | المعرفة قبل الاستعلام المتقدم والدردشة والتقارير | تصميم لاحق | قبل تنفيذها: تراخيص OCR/PDF-tooling/ffmpeg + **أوزان النماذج** (بوابة مزدوجة) |
| 6 | LLM Gateway + Agents + SQL Agent + Reports | اكتمال الـ Gateway + وكلاء التفكير + Chat (module `chat`) + SQL آمن + تقارير طويلة | إتقان الإجابة المسنودة قبل ربط الأنظمة | تصميم لاحق | لا (يرث بوابات P5) |
| 7 | MCP/API Integrations + Enterprise App Store | الربط الداخلي والمتجر وربط الحسابات وبوابات الاعتماد | التكامل بعد نضج الحوكمة والمعرفة والعمليات | تصميم لاحق | قبل تنفيذها: جرد الأنظمة الداخلية + مراجعة كل connector |
| 8 | Monitoring + Offline Deployment + Production Readiness | Observability كامل + Ops Controller + offline bundle/backup/restore منفّذة + HA readiness | التصلّب والتوسع بعد اكتمال الوظائف | تصميم لاحق | قبل التوزيع: فئة 4 كاملة (AGPL/أوزان/توقيع/TLS/Attribution) |
| — | Backlog — Deferred / Optional | قدرات مؤجلة بقرار | تُفعَّل بقرار وسعة | — | حسب البند |

---

## الجدول ب — النطاق (الداخل / الخارج / الوحدات)

| # | المميزات الداخلة | المميزات الخارجة صراحةً | modules/services الداخلة |
|---|---|---|---|
| 0 | هيكل repo + constitution/specs + سقالات **36 module** + عقود التجريد (Cache/Queue/Lock · ObjectStorage-fs|s3 · LLM · Identity · DB-Router · EventBus · Media) + Config Registry + Feature Flags + Service Registry + Compose (فعّال: Postgres×4 بأقل صلاحية لكل قاعدة · Qdrant · OpenSearch؛ ومعرّف مطفأ: cache-queue · object-storage · Neo4j) + افتراضيات D4/D5 (memory/Postgres · filesystem) + الخط الرقابي الأساسي D6 + Profiles/Bundles + Health + قشرة Web (i18n/RTL/tokens) + Worker skeleton + lockfiles/digest pinning + no-external-call + license-review seed | أي منطق أعمال، auth حقيقي، شاشات أعمال، وكلاء، نماذج تعمل، تكاملات، تقارير | كل الـ modules كسقالات + حاويات البنية + monitoring أساسي |
| 1 | Local Auth (IdP-adapter) + Organization + Permission spine مُنفَّذ (default-deny) + Metadata Registry + **Audit spine كامل** + شريحة Screen Builder (تعريف→migration→فحص→اعتماد→تطبيق→توثيق→CRUD) + Admin shell عربي | RAG/Media فعلي، وكلاء، workflow كامل، صلاحيات متقدمة كاملة، متجر، تقارير | identity, organization, permissions, admin, screens, fields, migrations, database-generation, records (أساسي), audit, config, flags |
| 2 | كل أنواع الحقول/التحققات + Row/Field-Level enforcement + شاشة توثيق كاملة + **Entity Profile مبدئي** | وكلاء/وسائط/تكاملات | screens, fields, records, permissions (+entity-profile ownership يُحسم بتصميمها) |
| 3 | Draft→Validation→Permission→Risk→Approval→Activation→Versioning→Rollback→Audit + Action/CTA + Notifications (دردشة لكل إشعار) + Tasks + Projects | RAG/وسائط، تكاملات | workflows, approvals, tasks, projects, notifications |
| 4 | RBAC+ABAC+ReBAC كامل + Need-to-know + SoD + field/row كامل + **Entity Profile كامل** + Feature/Module Management + Safe Mode + رسم تبعيات + Security Policies + **القائمة الحصرية لغير القابل للتعطيل (A10)** | وسائط ثقيلة، تكاملات | permissions, security-policy, feature-flags (شاشة), config |
| 5 | RAG هجين محكوم الصلاحية + File Service + OCR/Docs (PDF/Office) + Media pipeline (صوت/صور/فيديو-keyframes) + **RAG-over-media** + OKF + Model/Provider Registry UI + **Gateway الحد الأدنى** + وكلاء Retrieval/Validation + No-Guessing | نماذج ثقيلة لا يحتملها العتاد (تبقى قابلة للتوصيل)، فهم الفيديو الكامل | files, media, rag, search, okf, model-registry, provider-registry, llm-gateway (جزئي) |
| 6 | اكتمال الـ Gateway (per-agent selection UI) + Reasoning/Report agents + **Chat (module `chat`)** + Safe SQL Agent (read-only/allow-list/RLS) + Long Reports قسماً قسماً بالاستشهاد | تكاملات خارجية | llm-gateway (كامل), chat, sql_agent, reports + orchestrator/agents |
| 7 | Integration Management (MCP/API/Webhook/DB) + Enterprise App Store + ربط حسابات/تفويض (per-user/service-account) + الاستخدام داخل Chat/Tasks/Workflows/Reports/Notifications + بوابات human-in-the-loop | SaaS خارجي (اختياري لاحقاً عبر proxy وبموافقة صريحة) | integrations, mcp_connectors, app_store |
| 8 | Observability كامل (قابل للتبديل) + Deployment/Operations Controller + offline bundle موقّعة + backup/restore منفّذة ومختبرة + HA readiness + (Graph module اختياري) + (أدوات أمن اختيارية بنمط PentAGI/RedAmon في المتجر) | — | monitoring, backup_restore, service_registry (نضج), ops plane |
| B | فهم الفيديو الكامل · فصل قواعد فيزيائي عند الحاجة · K8s/OpenShift · تكامل أدوات Red Team/CERT · SSO موسّع/SAML · تكاملات خارجية عبر proxy | — | حسب البند |

---

## الجدول ج — البوابات (مخرجات/قبول/مخاطر/وثائق/قرارات)

| # | المخرجات | شروط القبول (مختصرة — التفصيل في تصميم المرحلة) | المخاطر | الوثائق المطلوبة قبلها | قرارات تُحسم قبل تنفيذها |
|---|---|---|---|---|---|
| 0 | منظومة تقلع كاملة الطبقات + /health أخضر + profiles تعمل + CI حدود/أسرار/offline + license-review مُعبّأ | إقلاع Local كامل؛ تبديل profile بالإعداد فقط؛ boundary test يرفض الاعتماد الممنوع؛ no-external-call ناجح؛ كل تغيير config/flag مدقَّق وversioned؛ لا منطق أعمال؛ زمن الإقلاع موثّق | over-engineering؛ ثقل البحث على الجهاز؛ فجوة ترخيص توقف compose | constitution + Methodology + Catalog + Open-Decisions + roadmap + **تصميم Phase 0 (معتمد)** | صفوف ترخيص الستاك المعتمد (فئة 2)؛ الفئة 3 عند تفعيل الصور الاختيارية فقط (C1–C5 مُغلقة بقرارات D) |
| 1 | دورة توليد شاشة محكومة كاملة + CRUD مدقَّق + أساس هوية/تنظيم/صلاحيات | كل خطوة عبر Permission Gate + Audit؛ لا DDL من نموذج؛ الثوابت immutable؛ deny tests؛ RTL صحيح | تعقيد الحوكمة؛ تسريب صلاحية | ما سبق + **تصميم Phase 1 (معتمد)** + Phase 0 منفّذة (DoD) | لا قرارات كبرى (IdP=Local محسوم) |
| 2 | شاشات معقّدة بعزل صف/حقل مُختبر + Entity Profile مبدئي | RLS/FLS يعملان تحت اختبار؛ توثيق التوليد كامل | أداء الاستعلام مع RLS | تصميم Phase 2 + P1 منفّذة | ملكية entity-profile (module) |
| 3 | workflows بنوعيها بدورة حياة كاملة + إشعارات/مهام/مشاريع | لا تفعيل workflow مستخدم قبل اعتماد (SoD)؛ rollback يعمل؛ كل انتقال مدقَّق | حلقات/تعارض workflows | تصميم Phase 3 + P2 منفّذة | مصفوفات الاعتماد الأولية (قابلة للضبط) |
| 4 | سياسات مركّبة تُنفَّذ + شاشة إدارة المزايا + Safe Mode | استحالة تعطيل أساسي من الواجهة؛ default-deny شامل؛ قائمة A10 مثبتة | تصعيد صلاحية؛ تعقيد السياسات | تصميم Phase 4 + P3 منفّذة | قواعد SoD التفصيلية (config) |
| 5 | رفع مستند/صوت/صورة → معالجة → فهرسة → استرجاع مصفّى + provenance + تبديل نموذج من الواجهة | الصلاحية قبل الاسترجاع مُختبرة؛ No-Guessing؛ مخرجات الوسائط في نفس الفهرس المحكوم؛ إبطال الكاش بالنسخ/الصلاحية | عتاد؛ جودة عربي (OCR/ASR)؛ تسريب كاش | تصميم Phase 5 + P4 منفّذة | محرك OCR العربي؛ تراخيص PDF-tooling/ffmpeg؛ **تراخيص أوزان النماذج (بوابة 1)**؛ **مزوّد Object Storage (MinIO|SeaweedFS — فئة 3 عند تفعيله)**؛ وValkey إن لزم لطوابير الوسائط |
| 6 | Chat مؤسسي مسنود + SQL قراءة فقط ضمن الصلاحية + تقرير طويل مُستشهَد | لا SQL خارج allow-list/RLS؛ Validation لا تفشل مفتوحة؛ اختبارات أمان SQL | حقن؛ هلوسة؛ تكلفة سياق | تصميم Phase 6 + P5 منفّذة | اختيار نماذج reasoning/chat الفعلية (Registry) |
| 7 | متجر يعرض المسموح فقط + استخدام تطبيق داخل الدردشة ضمن الصلاحية بتدقيق كامل | كل استدعاء ضمن صلاحية الحساب المربوط + بوابة اعتماد للإجراءات؛ رموز مُعمّاة | تنفيذ خطير؛ ربط ضار | تصميم Phase 7 + P6 منفّذة | جرد الأنظمة + عقود الـ API/MCP + مراجعة كل connector |
| 8 | ترقية Local→Production بالإعداد فقط مُثبتة + نسخ/استعادة متحقَّقة + مراقبة كاملة | config-only promotion مُختبر؛ استعادة ناجحة من bundle؛ lifecycle عبر Ops فقط | تعقيد تشغيلي | تصميم Phase 8 + P7 منفّذة | **فئة 4 كاملة**: موقف AGPL للتوزيع، أوزان النماذج (بوابة 2)، توقيع الحزمة، TLS/PKI، Attribution |
| B | حسب البند | حسب البند | — | ADR لكل تفعيل | حسب البند |

**بوابة بروفة التسليم المغلق (D13 — v1.0-baseline):** قبل **أول نشر إنتاجي داخل الشبكة المغلقة** تُنفَّذ **بروفة موثقة كاملة** لدورة: بناء الحزمة → النقل → التحقق من checksums → التطبيق → التراجع (rollback) — بوابة إلزامية ضمن نطاق Phase 8/الجاهزية الإنتاجية؛ المرجع: ADR تسليم GitHub/الشبكة المغلقة (ADR-0022).
