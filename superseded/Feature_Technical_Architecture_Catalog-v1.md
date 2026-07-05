> ⚠️ SUPERSEDED — لا يُستخدم للتنفيذ. المرجع الحالي: حزمة v2.0 (انظر superseded/README.md). تاريخ الوسم: 2026-07-03.

# Feature &amp; Technical Architecture Catalog
## منصة تشغيل معرفي مؤسسي تعمل في شبكة مغلقة — وثيقة تفصيلية مكمّلة للدراسة المعمارية
> لا كود · لا برومبتات تنفيذ · لا انتقال إلى Phase 0/1. مرجع تقني قبل الانتقال لاحقاً إلى Spec-driven development وModular Monolith.

**رموز مستخدمة في الجداول:** DB=PostgreSQL · Vec=Qdrant · Srch=OpenSearch · Obj=MinIO · Cache=Redis · LLM=نموذج لغوي · RAG=استرجاع · MCP=تكامل. الحالة: Core=أساسي · Opt=اختياري · 🔒=محميّة. الأدوار: U=User · A=Admin · SA=Super Admin · Ops=Operations.

---

## 1. Executive Summary

النظام **Enterprise AI / Local RAG / Local LM Platform** يعمل داخل شبكة مغلقة، **ليس chatbot** و**ليس** RAG بسيطاً و**ليس** Open WebUI. الـ LLM **ليس مصدر الحقيقة** (دوره تحليل/تلخيص/تفسير/تنفيذ مهام/طلب توضيح)؛ الحقيقة من قواعد البيانات الرسمية + المستندات المعتمدة + APIs الداخلية + السجلات الرسمية + الأنظمة المرتبطة رسمياً. الواجهة النهائية **Enterprise UI خاصة** (Arabic/English/RTL، white-label). النظام **metadata-driven**، ويُبنى **مرة واحدة** كمنتج قابل للنقل من MSI Titan إلى الإنتاج **بتغيير configuration فقط**.

**التوصية المعمارية الجوهرية:** بناء النظام كـ **Modular Monolith** — backend واحد قابل للنشر، مقسّم إلى modules/bounded-contexts واضحة الحدود (Auth، Authorization، Metadata، Records، Workflow، Integration، Media، RAG، Reports، …)، مع **عمليات غير متزامنة (workers)** للوكلاء والوسائط، ومخازن البيانات كحاويات منفصلة. هذا يوازن: «كل الطبقات حاضرة» + «يعمل خفيفاً على جهاز واحد» + «قابل للنقل والتوسع» (يمكن استخراج module إلى خدمة مستقلة لاحقاً عند الحاجة للتوسع، دون إعادة كتابة). **كل الطبقات حاضرة من البداية** بحالات (enabled/disabled/lightweight/demo/production/optional/protected)، **ودعم الوسائط جاهز معمارياً** عبر Media Pipeline + Model/Provider Registry + LLM Gateway (المؤجَّل فقط تشغيل نموذج ثقيل حسب العتاد).

---

## 2. Confirmed Decisions

منصة لا chatbot · LLM ليس مصدر الحقيقة · Enterprise UI خاصة (لا Open WebUI كوجه) · منتج واحد portable (config-only للإنتاج، Twelve-Factor) · **Modular Monolith** + workers + datastores منفصلة · نموذج `database.docx`: platform/apps/integration/reporting + Qdrant/OpenSearch/MinIO/Redis + Neo4j اختياري · ثلاث درجات فصل (Logical/Schema/Physical) · توليد محكوم بالاعتماد (لا DDL من نموذج، migrations + review + approval + versioning + audit + شاشة توثيق) · معرّفات تقنية ASCII والعربية labels في الميتاداتا · صلاحيات RBAC+ABAC+ReBAC + تصنيف خماسي (Public/Internal/Confidential/Secret/Restricted) + field/row/screen/action + Need-to-know + SoD + Least Privilege، **قبل أي استرجاع**، default-deny · النماذج مربوطة بـ **capabilities** لا بأسماء ثابتة، وقابلة للتغيير من الأدمن عبر Registry · OKF محلي بدور فهرس/قاموس/مسرد/تعليمات · Local Auth مع IdP-adapter · Spec Kit ومخرجات محايدة لأي Coding Agent · كل الطبقات حاضرة · الوسائط مدعومة معمارياً · workflows نوعان بدورة حياة كاملة · App Store بمستويين · **تمييز تعطيل capability عن تعطيل service** · Admin العادي **لا** يوقف services/containers أساسية.

---

## 3. Technology Evaluation Table

> تقييم كاقتراحات لا قرارات مفروضة. **تنبيه تراخيص:** التراخيص أدناه من أفضل معرفتي، وبعضها تغيّر مؤخراً (AGPL/إعادة ترخيص)؛ **يجب التحقق القانوني من الترخيص الحالي قبل الاعتماد** (وهي قاعدتك المثبتة: لا كود خارجي دون مراجعة ترخيص). البنود عالية الحساسية موسومة ⚠️.

### 3.1 قواعد البيانات والتخزين
| التقنية | الدور | Offline / الترخيص | الملاءمة (dev / scale / portable) | الحالة · الآن/لاحقاً | التوصية / البديل |
|---|---|---|---|---|---|
| PostgreSQL | مصدر الحقيقة العلائقي | نعم · PostgreSQL (متساهل) | ممتاز / ممتاز / نعم | Core · الآن | **اعتماد**. العمود الفقري. |
| pgvector | متجهات داخل Postgres | نعم · PostgreSQL | ممتاز / محدود / نعم | Opt · الآن (dev) | بديل خفيف لـ Qdrant في dev/low-resource. |
| Qdrant | vector search للإنتاج | نعم · Apache-2 | جيد / ممتاز (sharding/quantization) / نعم | Core · الآن | **اعتماد** للإنتاج؛ pgvector لـ dev. |
| OpenSearch | بحث نصي/هجين + logs | نعم · Apache-2 | ثقيل RAM / ممتاز / نعم | Core · الآن | **اعتماد**؛ في low-resource استخدم Postgres FTS مؤقتاً. تجنّب Elasticsearch (SSPL). |
| Redis ⚠️ | cache/queue/session | نعم · تغيّر الترخيص (RSAL/SSPL) | ممتاز / ممتاز / نعم | Core · الآن | **فضّل Valkey** (fork مفتوح BSD، متوافق) لتفادي قيود الترخيص، أو Redis-OSS متوافق. |
| MinIO ⚠️ | تخزين ملفات/وسائط | نعم · AGPL v3 | ممتاز / ممتاز / نعم | Core · الآن | S3-compatible ممتاز؛ **AGPL** مقبول للاستخدام الداخلي عادةً لكن لا تُوزّع نسخة معدّلة كخدمة. بديل Apache-2: **SeaweedFS** أو Ceph. |
| Neo4j ⚠️ | graph/علاقات معقدة | نعم · Community=GPLv3 (بلا clustering/RBAC) | جيد / محدود بالمجتمعي / نعم | Opt (off) · لاحقاً | إن لزم graph، **فضّل Apache AGE** (امتداد Postgres، Apache-2) لتفادي مخزن+ترخيص إضافي. |
| SQLite | embedded/tests/cache محلي | نعم · Public Domain | ممتاز / — / نعم | Opt · الآن | لأغراض محلية/اختبار فقط، **ليس** مصدراً رئيسياً. |
| Alembic | migration tooling | نعم · MIT | ممتاز / ممتاز / نعم | Core · الآن | **اعتماد** (Python-native) داخل غلاف حوكمة (review/approval/versioning). بديل JVM: Liquibase/Flyway. |

### 3.2 المعرفة والـ metadata
| التقنية | الدور | Offline / الترخيص | التوصية |
|---|---|---|---|
| OKF | Knowledge Catalog / Data Dictionary / Glossary / agent-instructions | نعم · Apache-2 | **اعتماد بدور محدود** الآن؛ توليد الحزم بأدوات محلية (لا BigQuery/Gemini). ليس مصدر حقيقة. |
| YAML/Markdown metadata | تعريفات مقروءة للـ agents وللبشر | نعم · — | اعتماد لصيغ OKF والتعريفات. |
| Schema/Screen/Field/Entity/Model/Permission/Workflow metadata | جوهر النظام metadata-driven | نعم · — | تُخزَّن في `platform_db` (مصدرها الرسمي) وتُصدَّر إلى OKF كتوثيق. |

### 3.3 واجهة المستخدم (مرجع فقط + الستاك المقترح)
| التقنية | الدور | الترخيص | التوصية |
|---|---|---|---|
| Next.js + React + TypeScript | ستاك Enterprise UI | MIT | **اعتماد** كأساس الواجهة الخاصة. |
| Tailwind CSS + shadcn/ui | نظام تصميم/مكوّنات (copy-in) | MIT | **اعتماد**؛ يناسب white-label وoffline؛ RTL عبر logical properties + `dir`. بديل: Radix/Mantine. |
| Open WebUI ⚠️ | مرجع UX / chat layer داخلي محتمل | v0.6.6+ قيد branding/عدد مستخدمين | **مرجع فقط**؛ لا يُعتمد كوجه. v0.6.5 (BSD-3) للدراسة، بمراجعة قانونية. |
| LibreChat | مرجع chat / مكوّن محتمل | MIT | أكثر ملاءمة من Open WebUI لـ white-label إن لزم اقتباس؛ لكن نبني واجهتنا. |
| NextChat / LobeChat / FastGPT ⚠️ | مراجع UX | MIT (FastGPT: قيود) | مراجع أفكار فقط؛ راجع ترخيص FastGPT. |

### 3.4 النماذج وLLM Gateway
| التقنية | الدور | Offline / الترخيص | التوصية |
|---|---|---|---|
| Ollama | تشغيل نماذج dev + تبديل سهل | نعم · MIT | **اعتماد لـ dev/Local Demo**؛ يبدّل نموذجاً رئيسياً في الذاكرة (غير مثالي للتزامن). |
| vLLM | inference إنتاجي عالي الإنتاجية | نعم · Apache-2 | **اعتماد للإنتاج**؛ يحتاج GPU مناسباً. |
| SGLang | serving بديل (structured/بنية متقدمة) | نعم · Apache-2 | Opt · بديل/مكمّل لـ vLLM حسب الحاجة. |
| llama.cpp | CPU/edge/GGUF | نعم · MIT | Opt · low-resource/CPU؛ يقف تحته Ollama. |
| OpenAI-compatible endpoints | **عقد موحّد** للـ Gateway | نعم | **قِس الـ LLM Gateway على هذا العقد**؛ Ollama وvLLM يوفّرانه → تبديل المزوّد بالإعداد. |

### 3.5 RAG والبحث
| العنصر | الدور | التوصية |
|---|---|---|
| Hybrid RAG (Qdrant + OpenSearch + reranker) | استرجاع دقيق | **اعتماد**؛ vector + BM25 ثم rerank. |
| Embeddings (مثال: nomic-embed / bge-m3) | تمثيل متجهي | عبر Registry (capability=embedding). |
| Reranker (مثال: bge-reranker-v2-m3) | ترتيب النتائج | عبر Registry (capability=reranking). |
| Chunking + metadata filtering + permission-aware retrieval + citation + doc versioning + cache invalidation | pipeline آمن | **اعتماد**؛ المفتاح: الصلاحية قبل الاسترجاع + provenance + إبطال كاش بتغيّر النسخة/الصلاحية. |

### 3.6 الوسائط
| التقنية | الدور | الترخيص | التوصية |
|---|---|---|---|
| Tesseract | OCR أساس | Apache-2 | baseline؛ العربية مقبولة. |
| PaddleOCR / docTR | OCR متعدد اللغات (عربي) | Apache-2 | **فضّل** لجودة العربية. |
| Apache Tika | استخراج نصوص PDF/Office واسع | Apache-2 (JVM) | **اعتماد** للتحليل الواسع. |
| PyMuPDF ⚠️ | parsing PDF قوي | AGPL/تجاري | تنبيه ترخيص؛ بديل: pdfplumber (MIT) / pypdf (BSD). |
| python-docx / openpyxl | Office | MIT | اعتماد. |
| faster-whisper (Whisper) | تفريغ صوتي | MIT | **اعتماد** (كفاءة CTranslate2)؛ العربية مقبولة. |
| Vision / Video / Multimodal models | فهم صور/فيديو | حسب النموذج | عبر Registry (capabilities: image/video understanding, multimodal)؛ تشغيل ثقيل حسب العتاد. |
| keyframe extraction (ffmpeg) | لقطات فيديو | LGPL/GPL | **اعتماد** لاستخراج الإطارات/الصوت. |

### 3.7 التكاملات
| العنصر | الدور | التوصية |
|---|---|---|
| MCP | بروتوكول أدوات/موصلات | **اعتماد** كطبقة تكامل موحّدة. |
| Internal APIs / Webhooks / DB connectors | ربط الأنظمة الداخلية | **اعتماد**؛ الأساس داخلي. |
| Connector Registry + per-user / service-account authorization | حوكمة الربط | **اعتماد**؛ ربط حساب المستخدم أو service account حسب الحالة. |
| Internal OIDC/OAuth | تفويض داخلي | Opt · عند توفّره داخل الشبكة. |
| Integration logs + sync jobs | تدقيق/مزامنة | **اعتماد**؛ كل استدعاء مدقَّق. |
| External SaaS | خارجي | Opt · لاحقاً عبر proxy/gateway فقط (ليس أساساً). |

### 3.8 التشغيل والمراقبة
| التقنية | الدور | الترخيص | التوصية |
|---|---|---|---|
| Docker / Docker Compose / Compose profiles | تشغيل ونقل | Apache-2 | **اعتماد** أساس النشر القابل للنقل. |
| Config files + env vars + health checks | إعداد وصحة | — | **اعتماد** (Twelve-Factor). |
| Prometheus | مقاييس | Apache-2 | **اعتماد**. بديل: VictoriaMetrics (Apache-2). |
| Grafana ⚠️ / Loki ⚠️ | لوحات / سجلات | AGPLv3 | مقبول داخلياً؛ لا تُوزّع نسخة معدّلة كخدمة. |
| OpenTelemetry | tracing | Apache-2 | Opt · موصى لاحقاً للتتبع الموزّع. |
| Backup/Restore + offline bundle | نقل مغلق/تعافي | — | **اعتماد** (images+wheels+models، تحقق واستعادة). |
| Kubernetes / OpenShift | تنسيق إنتاجي/HA | Apache-2 | **لاحقاً** كخيار توسّع؛ ليس مطلوباً الآن (Compose يكفي dev/staging). |

---

## 4. Feature Catalog

> أعمدة: الميزة · المستفيد · مكان الظهور · Core/Opt · تعطيل الأدمن؟ · موافقة؟ · يحتاج · Phase · القبول (مختصر) · المخاطر (مختصر).

| الميزة | المستفيد | الظهور | C/O | تعطيل أدمن؟ | موافقة؟ | يحتاج | Phase | القبول | المخاطر |
|---|---|---|---|---|---|---|---|---|---|
| Chat | U | User Workspace | Core | نعم (capability) | لا | LLM,RAG,DB | 6 | إجابة مسنودة بمصدر + provenance | هلوسة → No-Guessing/Validation |
| User Workspace | U | Home | Core | لا | لا | DB | 1 | يعرض المسموح فقط | تسريب صلاحيات |
| Projects | U | Workspace | Core | نعم | لا | DB,Obj | 3 | تجميع محادثات/ملفات بالصلاحية | خلط نطاقات |
| Tasks | U/A | Workspace/Admin | Core | نعم | أحياناً | DB,LLM | 3 | قوالب/مهام تُنفَّذ بالصلاحية | تنفيذ غير مصرّح |
| Notifications (+chat/إشعار) | U | Workspace | Core | نعم | لا | DB | 3 | إشعار تفاعلي مدقَّق | إزعاج/تسريب |
| Screen Builder | A | Admin | Core | لا (أساسي) | لا (لكنه ينتج migration يحتاج موافقة) | DB | 1 | تعريف شاشة→ميتاداتا | تعريف خاطئ |
| Field Builder | A | Admin | Core | لا | لا | DB | 1/2 | أنواع/تحققات حقول | فقد سلامة |
| Records Engine | U/A | Screens | Core | لا | حسب workflow | DB | 1/2 | CRUD مع RLS/FLS | تجاوز صفوف/حقول |
| Database Generation Review | A | Admin | Core | لا | نعم | DB | 1/2 | فحص تعارض/مخاطر قبل الاعتماد | تطبيق ضار |
| Migration Approval | A/SA | Admin | Core | لا | نعم | DB | 1/2 | لا تطبيق بلا اعتماد | كسر توافق |
| Workflow Builder | A | Admin | Core | نعم | — | DB | 3 | بناء workflow مربوط | حلقات/تعارض |
| User-created Workflows (approval) | U | Workspace | Core | نعم | نعم | DB | 3 | لا تفعيل قبل اعتماد | تفعيل غير آمن |
| Admin-created Workflows | A | Admin | Core | نعم | — | DB | 3 | ربط مسبق يعمل | أثر واسع |
| Action Buttons | U/A | Screens | Core | نعم | حسب الفعل | DB | 3 | فعل محكوم بالصلاحية | فعل خطير |
| CTA Buttons | U | UI | Core | نعم | لا | — | 3 | إجراء موجَّه | — |
| Entity Profile | U | Workspace | Core | نعم | لا | DB,RAG | 4 | تجميع كيان بالصلاحية | تجميع مفرط |
| Reports | U/A | Reports | Core | نعم | لا | DB | 6 | تقرير من مصادر الحقيقة | بيانات قديمة |
| Long Reports | U/A | Reports | Core | نعم | لا | LLM,RAG,DB | 6 | بناء قسماً قسماً + استشهاد | تكلفة/هلوسة |
| File Upload | U | Workspace | Core | نعم | لا | Obj | 5 | رفع مدقَّق إلى MinIO | ملفات ضارة |
| PDF/Office Processing | U/A | Media | Core | نعم | لا | Obj,Srch,Vec | 5 | استخراج/فهرسة | parsing رديء |
| OCR | U/A | Media | Core | نعم | لا | Obj | 5 | نص من صور/مسح | جودة عربي |
| Image Understanding | U/A | Media | Opt | نعم | لا | LLM(vision),Obj | 5 | وصف/تصنيف صورة | عتاد ثقيل |
| Audio Transcription | U/A | Media | Core | نعم | لا | LLM(whisper),Obj | 5 | صوت→نص | لهجات |
| Video Understanding | U/A | Media | Opt | نعم | لا | LLM,Obj | 5(معماري)/لاحقاً(ثقيل) | صوت+keyframes الآن؛ فيديو كامل لاحقاً | عتاد ثقيل جداً |
| RAG | U/A | Chat/Reports | Core | نعم | لا | Vec,Srch,LLM | 5 | استرجاع مصفّى بالصلاحية | تسريب/هلوسة |
| SQL Agent | U/A | Chat/Reports | Core | نعم | لا | DB | 6 | SELECT آمن ضمن الصلاحية | حقن/تسريب |
| App Store | U | Workspace | Core | نعم | حسب التطبيق | MCP,DB | 7 | يرى المسموح فقط | وصول واسع |
| MCP/API Integrations | U/A | Store/Admin | Core | نعم | نعم (إجراءات) | MCP | 7 | استدعاء ضمن الصلاحية + بوابة | تنفيذ خطير |
| Connector Management | A/SA | Admin | Core | نعم | نعم | MCP,DB | 7 | تسجيل/اختبار/تفعيل موصل | ربط ضار |
| Model/Provider Management | A/SA | Admin | Core | جزئي (capability) | حسب السياسة | DB | 5/6 | تغيير نموذج من الواجهة | نموذج غير آمن |
| Feature Flags | A/SA | Admin | 🔒Core | لا (الأعلام نفسها) | حسب العلم | DB | 0/4 | تفعيل/تعطيل قدرة مدقَّق | تعطيل خاطئ |
| Profiles | SA/Ops | Admin/Ops | 🔒Core | لا | نعم (بيئة) | DB | 0 | تبديل profile بالإعداد | انقطاع |
| Configuration Management | SA/Ops | Admin/Ops | 🔒Core | لا | نعم | DB | 0 | تغيير مدقَّق + versioning | كسر إقلاع |
| Audit Viewer | A/SA | Admin | 🔒Core | لا | لا | DB | 1+ | عرض/بحث السجل | كشف حسّاس |
| Monitoring View | A/SA/Ops | Admin/Ops | Core | لا | لا | — | 0/8 | صحة الخدمات | إنذار كاذب |
| License/About | U/A | UI | Core | لا | لا | — | 0 | attribution صحيح | خرق ترخيص |
| Backup/Restore | Ops | Ops | Core | لا | نعم | Obj,DB | 8 | نسخ/استعادة متحقَّقة | فقد بيانات |
| Security/Policy | SA | Admin | 🔒Core | لا | نعم | DB | 4 | سياسات تُنفَّذ | سوء ضبط |
| Permission Management | A/SA | Admin | 🔒Core | لا | حسب التغيير | DB | 1/4 | سياسات مدقَّقة | تصعيد صلاحية |
| Organization Management | A/SA | Admin | Core | لا | حسب التغيير | DB | 1 | قطاعات/إدارات/عضوية | خلط تنظيمي |
| User Management | A/SA | Admin | Core | لا | حسب التغيير | DB | 1 | تعطيل/تفعيل/تغيير كلمة | تصعيد/تعطيل خاطئ |

---

## 5. Service Catalog (modules داخل Modular Monolith، ما لم يُذكر خلاف)

> أعمدة: الخدمة/الموديول · الدور · C/O · يعطّلها · التبعيات · أهم config keys · Health · Local→Prod · التوصية.

| الخدمة | الدور | C/O | يعطّلها | تبعيات | config keys | Health | Local→Prod | توصية |
|---|---|---|---|---|---|---|---|---|
| Enterprise UI | واجهة U/A | Core | – | Backend | UI_BASE_URL, LOCALE, THEME | تحميل الأصول | replica واحدة → عدة + CDN داخلي | اعتماد |
| Backend API (Monolith) | مدخل/تنسيق | Core | – | Postgres,Redis | APP_PROFILE, DB_URL, REDIS_URL | /health | 1 → N replicas خلف LB | اعتماد |
| Admin Console (module/UI) | إدارة | Core | – | Backend | – | – | – | اعتماد |
| Auth Service | مصادقة + IdP-adapter | 🔒Core | – | platform_db | AUTH_PROVIDER, JWT_SECRET | – | Local→LDAP/OIDC بالإعداد | اعتماد |
| Organization Service | تنظيم | Core | – | platform_db | – | – | – | اعتماد |
| Permission Service | محرّك صلاحيات | 🔒Core | – | platform_db | POLICY_CACHE_TTL | – | نفسه + كاش | اعتماد |
| Screen Metadata Service | تعريفات شاشات/حقول | Core | – | platform_db | – | – | – | اعتماد |
| Record Service | CRUD الكيانات | Core | – | apps_db | DB_ROUTER_MAP | – | schema→physical بالإعداد | اعتماد |
| Migration/Generation Service | توليد محكوم | Core | – | platform/apps_db | MIGRATION_APPROVAL=on | – | – | اعتماد |
| Workflow Service | دورة حياة workflows | Core | A (capability) | platform_db | – | – | – | اعتماد |
| Task Service | مهام/قوالب | Core | A | platform_db | – | – | – | اعتماد |
| Project Service | مشاريع | Core | A | platform_db,MinIO | – | – | – | اعتماد |
| Notification Service | إشعارات | Core | A | platform_db,Redis | – | – | queue أكبر | اعتماد |
| Audit Service | تدقيق append-only | 🔒Core | – | platform_db | AUDIT_RETENTION | – | partition/archival | اعتماد |
| Config Service (Registry) | إعداد/profiles | 🔒Core | – | platform_db | APP_PROFILE, BUNDLES | – | – | اعتماد |
| Feature Flag Service | أعلام القدرات | 🔒Core | – | platform_db | FLAG_SCOPES | – | – | اعتماد |
| Service Registry | كتالوج/صحة/تبعيات | 🔒Core | – | – | – | يجمع /health | يتكامل مع orchestrator | اعتماد (خفيف) |
| Deployment/Operations Controller | lifecycle/ترقية | Core (Ops) | Ops | orchestrator | OPS_MODE | – | scripts → controller | اعتماد رفيع الآن |
| LLM Gateway | توجيه النماذج | Core | – | Ollama/vLLM | LLM_ENDPOINTS | فحص endpoints | Ollama→vLLM بالإعداد | اعتماد (OpenAI-compatible) |
| Model Registry | كتالوج نماذج | Core | – | platform_db | – | – | – | اعتماد |
| Provider Registry | مزوّدون/endpoints | Core | – | platform_db | PROVIDER_ENDPOINTS | – | – | اعتماد |
| RAG Service | فهرسة/بحث هجين | Core | A | Qdrant,OpenSearch | EMBED_CAP, RERANK_CAP | فحص المخازن | عناقيد | اعتماد |
| SQL Agent Service | SQL آمن للقراءة | Core | A | apps_db(RLS) | SQL_ALLOWLIST | – | read-replica | اعتماد |
| Media/OCR Service | pipeline الوسائط | Core (قدرات Opt) | A (capability) | MinIO,Gateway,Registry | MEDIA_CAPS | – | workers أكثر/عُقد GPU | اعتماد (معماري من البداية) |
| File Service | إدارة الملفات | Core | – | MinIO | S3_ENDPOINT | فحص MinIO | bucket/erasure | اعتماد |
| Report Service | تقارير/تصدير | Core | A | reporting_db,LLM | – | – | – | اعتماد |
| Integration Service | موصلات | Core (قدرات Opt) | A/SA | integration_db | CONNECTORS | – | – | اعتماد |
| App Store Service | متجر المستخدم | Core (قدرات Opt) | A | integration_db | – | – | – | اعتماد |
| MCP Connector Service | جسر MCP | Core | A | Integration | MCP_SERVERS | فحص الخوادم | – | اعتماد |
| PostgreSQL | مصدر الحقيقة | Core | – | – | DB_URL, POOL | فحص اتصال | single→HA+PgBouncer+replicas | اعتماد |
| Qdrant | متجهات | Core | – | – | QDRANT_URL | فحص | single→cluster | اعتماد |
| OpenSearch | بحث/logs | Core | – | – | OS_URL | فحص | single→cluster | اعتماد (RAM) |
| Redis/Valkey ⚠️ | cache/queue/session | Core | – | – | REDIS_URL | فحص | single→cluster/sentinel | Valkey مفضّل |
| MinIO ⚠️ | تخزين | Core | – | – | S3_* | فحص | single→erasure cluster | AGPL؛ بديل SeaweedFS |
| Neo4j/Graph | علاقات | Opt (off) | A/SA | – | GRAPH_ENABLED=false | فحص | – | فضّل Apache AGE |
| Monitoring stack (Prometheus/Grafana/Loki) ⚠️ | مراقبة | Core | – | كل الخدمات | METRICS_* | ذاتي | – | Grafana/Loki AGPL داخلياً |
| Backup/Restore tools | تعافٍ/نقل | Core | Ops | MinIO,DB | BACKUP_PATH | – | – | اعتماد + offline bundle |

---

## 6. Admin Screens Catalog

> أعمدة: الشاشة · الوصول · أهم العمليات · صلاحيات · قابل للتغيير منها · Ops-only · Audit · القبول · مخاطر.

| الشاشة | الوصول | العمليات | صلاحيات | تُغيّر منها | Ops-only | Audit | القبول | مخاطر |
|---|---|---|---|---|---|---|---|---|
| Admin Dashboard | A/SA | ملخصات/تنبيهات | admin.view | – | – | – | يعرض حالة عامة | كشف مؤشرات |
| Users | A/SA | إضافة/تعطيل/دور | user.manage | بيانات مستخدم (لا الرقم الوظيفي) | – | user.* | تعطيل/تفعيل يعمل | تصعيد |
| Organization/Sectors/Departments | A/SA | CRUD تنظيمي | org.manage | الهيكل | – | org.* | عضوية صحيحة | خلط |
| Roles | A/SA | CRUD أدوار | role.manage | الأدوار | – | role.* | ربط صلاحيات | تصعيد |
| Permissions | SA | سياسات RBAC/ABAC/ReBAC | perm.manage | السياسات | – | perm.* | تُنفَّذ فعلاً | ثغرة |
| Data Classification | SA | مستويات/قواعد | class.manage | التصنيفات | – | class.* | تُطبَّق على البيانات | تسريب |
| Screens | A | تعريف شاشات | screen.manage | ميتاداتا شاشة | – | screen.created | تُخزَّن صحيحة | خطأ تعريف |
| Fields | A | تعريف حقول | field.manage | ميتاداتا حقل | – | field.added | أنواع/تحققات | فقد سلامة |
| Database Generation Review | A/SA | فحص migration | migration.review | – (عرض/تعليق) | – | migration.generated | فحص تعارض/مخاطر | تطبيق ضار |
| Migration Approval | A/SA | اعتماد/رفض | migration.approve | حالة الاعتماد | – | migration.approved/rejected/applied | لا تطبيق بلا اعتماد | كسر |
| Records Admin | A | إدارة سجلات | record.admin | سجلات ضمن الصلاحية | – | record.* | RLS/FLS مطبّق | تجاوز |
| Workflows | A | بناء/تعديل | workflow.manage | تعريف workflow | – | workflow.* | يعمل مربوطاً | أثر واسع |
| Workflow Approvals | A/Manager | اعتماد workflow المستخدم | workflow.approve | حالة | – | workflow.approved/rejected | SoD (منشئ≠معتمِد) | تجاوز |
| Tasks Templates | A | قوالب | task.manage | القوالب | – | task.* | إعادة استخدام | – |
| Projects Admin | A | إدارة مشاريع | project.admin | – | – | project.* | نطاق بالصلاحية | خلط |
| Notifications Admin | A | قوالب/قنوات | notif.manage | القنوات | – | notif.* | تسليم مدقَّق | إزعاج |
| App Store Management | A | نشر/إتاحة تطبيقات | store.manage | الإتاحة | – | app.* | يرى المسموح فقط | وصول واسع |
| MCP/API Connectors | A/SA | تسجيل/اختبار/تفعيل | connector.manage | الموصلات | endpoints/secrets → **Ops** | connector.added/disabled | اختبار اتصال يعمل | ربط ضار |
| Model/Provider Management | A/SA | نموذج لكل capability | model.manage | خريطة capability→model | provider endpoints البنيوية → **Ops** | model.changed/provider.changed | تغيير من الواجهة يعمل | نموذج غير آمن |
| Media/OCR Settings | A | نماذج/حدود وسائط | media.manage | capability flags/حدود | عُقد GPU → **Ops** | media.* | تبديل نموذج نوع وسائط | عتاد |
| RAG Settings | A | chunking/rerank/فهرسة | rag.manage | معاملات RAG | – | rag.* | استرجاع محسّن | جودة |
| Feature Flags | A/SA | تفعيل/تعطيل قدرة | flag.manage | الأعلام (غير المحميّة) | الأساسية محميّة | feature_flag.changed | تعطيل قدرة لا خدمة | تعطيل خاطئ |
| Profiles | SA | اختيار/تعريف profile | profile.manage | defaults الـ profile | تبديل بيئة/lifecycle → **Ops** | profile.changed | تبديل بالإعداد | انقطاع |
| Configuration Registry | SA | قيم إعداد | config.manage | القيم (dynamic) | static/secrets → **Ops** | config.changed | versioning/rollback | كسر إقلاع |
| Service Health | A/SA/Ops | عرض صحة | health.view | – (قراءة فقط) | lifecycle → **Ops** | service.health_alert | حالة/تبعيات صحيحة | إنذار كاذب |
| Audit Logs | A/SA | عرض/بحث/تصدير | audit.view | – | – | export.requested | بحث دقيق | كشف حسّاس |
| Reports Admin | A | قوالب/جدولة | report.admin | القوالب | – | report.* | تقرير من الحقيقة | قديم |
| Backup/Restore | Ops | نسخ/استعادة | ops.backup | – | كامل → **Ops** | backup.created/restore.executed | متحقَّق | فقد |
| About/Licenses | A/U | عرض تراخيص | – | – | – | – | attribution صحيح | خرق |
| Security Policies | SA | سياسات أمن/بوابات | security.manage | السياسات | – | security.* | تُنفَّذ | سوء ضبط |

---

## 7. User Screens Catalog

> أعمدة: الشاشة · المستخدم · العمليات · صلاحيات · مصادر البيانات · LLM؟ · RAG؟ · Store؟ · Audit؟ · القبول.

| الشاشة | المستخدم | العمليات | صلاحيات | المصادر | LLM | RAG | Store | Audit | القبول |
|---|---|---|---|---|---|---|---|---|---|
| User Home | U | تصفح/اختصارات | user.view | platform/apps_db | لا | لا | لا | جزئي | يعرض المسموح فقط |
| Chat | U | سؤال/أمر طبيعي | chat.use | DB/docs/APIs | نعم | نعم | نعم | نعم | مسنود بمصدر + No-Guessing |
| Projects | U | إنشاء/تجميع | project.use | apps_db,MinIO | اختياري | اختياري | لا | نعم | نطاق بالصلاحية |
| Tasks | U | إنشاء/تنفيذ | task.use | DB | نعم | اختياري | نعم | نعم | تنفيذ مصرّح |
| Notifications | U | قراءة/تفاعل/دردشة | notif.use | DB | اختياري | لا | لا | نعم | إشعار مدقَّق |
| App Store | U | تصفح/طلب ربط | store.use | integration_db | لا | لا | نعم | نعم | المسموح فقط |
| My Connected Apps | U | ربط/فصل/تفويض | app.link | integration_db | لا | لا | نعم | نعم | ربط ضمن الصلاحية |
| Screens/Applications | U | استخدام الشاشات المولّدة | screen.use | apps_db | اختياري | اختياري | حسب التطبيق | نعم | RLS/FLS مطبّق |
| Records | U | CRUD ضمن الصلاحية | record.use | apps_db | لا | لا | لا | نعم | عزل صفوف/حقول |
| Entity Profile | U | عرض كيان مجمّع | entity.view | DB,RAG | اختياري | نعم | لا | نعم | تجميع بالصلاحية |
| Files | U | رفع/عرض | file.use | MinIO | لا | لا | لا | نعم | رفع مدقَّق |
| Reports | U | توليد/تصدير | report.use | DB,RAG | نعم | نعم | لا | نعم | من مصادر الحقيقة |
| Workflow Inbox | U | متابعة workflows | workflow.use | platform_db | لا | لا | لا | نعم | حالة صحيحة |
| Approvals | Manager/U | اعتماد/رفض | workflow.approve | platform_db | لا | لا | لا | نعم | SoD مطبّق |
| Search | U | بحث موحّد | search.use | DB,Vec,Srch | اختياري | نعم | لا | نعم | نتائج مصفّاة بالصلاحية |
| Settings | U | تفضيلات/لغة/كلمة مرور | self.manage | platform_db | لا | لا | لا | نعم | تغيير آمن (لا الرقم الوظيفي) |

---

## 8. Configuration &amp; Profiles Matrix

**Environment Profiles (واحد نشط):**
| Profile | يتغيّر | لا يتغيّر | خدمات مفعّلة | lightweight | نموذج افتراضي | resources | logging | monitoring | يغيّره | restart؟ | approval؟ |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Local | endpoints محلية، بلا TLS، replica=1 | الكود/المعمارية | كلها (demo) | كلها | خفيف (Ollama) | منخفض | debug | أساسي | Ops/SA | نعم (static) | لا |
| Demo | بيانات عرض، مستخدم/اثنان | الكود | كلها | معظمها | خفيف | منخفض-متوسط | info | أساسي | Ops/SA | نعم | لا |
| Staging | إعدادات أكبر، اختبار شامل | الكود | كلها | جزئي | متوسط | متوسط | info | متوسط | Ops/SA | نعم | نعم |
| Production | عناقيد، TLS، replicas=N، عُقد GPU | الكود | كلها | لا | vLLM موزّع | عالٍ | warn/audit | كامل | Ops | نعم | نعم |

**Capability Bundles (قابلة للتركيب فوق البيئة):**
| Bundle | يفعّل | يعطّل | ملاحظات | يغيّره | restart؟ | approval؟ |
|---|---|---|---|---|---|---|
| Low-resource | نماذج خفيفة، pgvector/FTS بدل عناقيد | vision/video الثقيلة | لـ dev/MSI Titan | SA | جزئي | لا |
| Full-stack | كل القدرات | – | staging/prod | SA | جزئي | نعم |
| Media-enabled | OCR/vision/audio/video pipeline | (نماذج ثقيلة حسب العتاد) | معماري متاح دائماً | A/SA | لا (flags) | حسب السياسة |
| Security-enabled | سياسات/بوابات مشدّدة، أدوات أمن | – | فرق الأمن/CERT | SA | لا | نعم |
| Graph-enabled | Neo4j/Apache AGE | – | علاقات معقدة | SA | نعم (تشغيل الخدمة) | نعم |
| Integration-enabled | موصلات/متجر واسع | – | حسب الأنظمة الداخلية | A/SA | لا | نعم |

**قاعدة:** static config → restart (Ops)؛ dynamic flags → live (Registry). الأساسية محميّة لا تُعطَّل من الواجهة. كل تغيير مدقَّق + versioned + قابل للـ rollback.

---

## 9. Capability-to-Model Mapping

> النظام مربوط بـ **capabilities** لا بأسماء نماذج؛ الأمثلة توضيحية فقط.
| Capability | نوع النموذج | GPU؟ | يعمل على dev؟ | يُغيَّر من الأدمن؟ | C/O | Fallback | Audit؟ | مخاطر |
|---|---|---|---|---|---|---|---|---|
| chat | LLM عام | مفضّل | نعم (خفيف) | نعم | Core | نموذج أصغر | نعم | هلوسة |
| reasoning | LLM قوي | نعم | محدود | نعم | Core | chat model | نعم | تكلفة |
| summarization | LLM متوسط | مفضّل | نعم | نعم | Core | chat | نعم | فقد دقة |
| long report | LLM + سياق طويل | نعم | محدود | نعم | Core | تقسيم أدق | نعم | تكلفة |
| SQL generation | LLM/coder | مفضّل | نعم | نعم | Core | قوالب SQL | نعم | حقن |
| code generation | coder | نعم | محدود | نعم | Opt | – | نعم | كود ضار |
| embedding | embedder | مفضّل | نعم | نعم | Core | نموذج embed أصغر | نعم | جودة استرجاع |
| reranking | reranker | مفضّل | نعم | نعم | Core | بلا rerank | نعم | ترتيب أضعف |
| OCR | OCR engine | لا/مفضّل | نعم | نعم | Core | Tesseract | نعم | جودة عربي |
| document understanding | multimodal/LLM | نعم | محدود | نعم | Opt | استخراج نصي | نعم | عتاد |
| image understanding | vision | نعم | محدود | نعم | Opt | OCR فقط | نعم | عتاد |
| audio transcription | ASR (Whisper) | مفضّل | نعم | نعم | Core | نموذج أصغر | نعم | لهجات |
| video understanding | video/multimodal | نعم (ثقيل) | لا (لاحقاً) | نعم | Opt | صوت+keyframes | نعم | عتاد جداً |
| classification | LLM/مصنّف | مفضّل | نعم | نعم | Core | قواعد | نعم | خطأ تصنيف |
| validation | LLM تحقق | مفضّل | نعم | نعم | Core | قواعد/citations | نعم | fail-open ممنوع |
| translation | LLM/مترجم | مفضّل | نعم | نعم | Opt | بلا ترجمة | نعم | دقة |
| Arabic enhancement | LLM عربي | مفضّل | نعم | نعم | Opt | نموذج عام | نعم | أسلوب |

**Hardware-aware selection:** الـ Gateway + Hardware/Runtime Manager يمنعان تحميلاً يتجاوز العتاد؛ الـ fallback يُضبط في Registry. **default-deny للتحقق** (validation لا تفشل مفتوحة).

---

## 10. Data Flow Scenarios

> لكل سيناريو: الخطوات · الخدمات · الصلاحية · مصدر الحقيقة · Audit · التعامل مع الفشل.

1. **سؤال عن بيانات داخلية** — UI→API(auth)→Orchestrator(تصنيف+سياق+**Permission Gate**)→Retrieval/SQL ضمن الصلاحية→Validation→Reasoning→إجابة+provenance. الخدمات: API/Orchestrator/RAG/SQL/Gateway. الصلاحية: قبل الاسترجاع. الحقيقة: DB/docs/APIs. Audit: rag/sql query + record.viewed. الفشل: نقص أدلة→No-Guessing.
2. **سؤال غامض** — Orchestrator يكتشف الغموض→**طلب توضيح** (لا تخمين). Audit: chat. الفشل: يبقى في طلب التوضيح.
3. **رفض بسبب صلاحية** — Permission Gate=deny→رسالة «لا صلاحية»؛ لا استرجاع. Audit: **permission_denied**. الفشل: default-deny.
4. **الأدمن ينشئ شاشة** — Admin→Screen Builder→ميتاداتا في platform_db. الصلاحية: screen.manage. Audit: **screen.created/field.added**.
5. **توليد migration** — من الميتاداتا→ملف migration + فحص تعارض/مخاطر (لا DDL من نموذج). Audit: **migration.generated**. الفشل: يبقى draft.
6. **اعتماد migration** — Approver يعتمد→تطبيق داخل schema + versioning. الصلاحية: migration.approve (SoD). Audit: **migration.approved/applied**. الفشل: rollback نسخة.
7. **إدخال بيانات في شاشة** — Record Service مع RLS/FLS + ownership. الصلاحية: record.use. الحقيقة: apps_db. Audit: **record.created/updated**.
8. **إنشاء workflow (مستخدم)** — Draft→Validation→Permission→Risk. Audit: **workflow.created**. الفشل: لا تفعيل.
9. **اعتماد workflow (Manager)** — approve (SoD)→Activation. Audit: **workflow.approved/activated**. الفشل: rejected + سبب.
10. **استخدام App Store** — يرى المسموح فقط→يفتح تطبيقاً. الصلاحية: store.use. Audit: app view. الفشل: يُخفى غير المسموح.
11. **ربط حساب بتطبيق داخلي** — تفويض/ربط عبر Integration. الصلاحية: app.link. الحقيقة: integration_db (رموز مُعمّاة). Audit: **app.connected**. الفشل: يُلغى الربط.
12. **رفع PDF** — رفع→MinIO→Media pipeline (Tika/OCR إن مسحوب)→chunk→embed→index. Audit: **file.uploaded/ocr.completed/media.processed**. الفشل: يُعلَّم فشل المعالجة.
13. **رفع صورة** — MinIO→vision (إن مفعّل) أو OCR→نتيجة مربوطة بالمصدر. Audit: media.processed. الفشل: fallback إلى OCR.
14. **رفع فيديو** — MinIO→استخراج صوت(ffmpeg)+transcription+keyframes→(فهم فيديو كامل إن توفّر العتاد). Audit: media.processed. الفشل: يكتفي بالصوت/keyframes.
15. **طلب تقرير طويل** — Report Agent يبني قسماً قسماً من المصادر مع استشهاد. الحقيقة: DB/docs. Audit: **report.generated**. الفشل: قسم بلا دليل→يُعلَّم.
16. **تغيير نموذج في Registry** — Admin يبدّل capability→model→Gateway يحلّه وقت التشغيل. الصلاحية: model.manage. Audit: **model.changed/provider.changed**. الفشل: fallback المعرّف.
17. **تغيير feature flag** — Admin يعطّل/يفعّل **قدرة** (لا خدمة). الأساسية محميّة. Audit: **feature_flag.changed**. الفشل: منع تعطيل أساسي.
18. **Operations يغيّر profile/config** — Ops عبر سطح العمليات؛ static→restart. Audit: **profile.changed/config.changed**. الفشل: fail-fast عند إعداد ناقص + rollback.
19. **فشل خدمة + health alert** — Service Registry/health يكتشف→تنبيه في Monitoring؛ الأدمن يرى (قراءة)، Ops يتصرّف. Audit: **service.health_alert**. الفشل: تدهور رشيق (degrade).
20. **إبطال كاش** — تغيّر نسخة مستند/فهرس/سكيم/صلاحية→مفتاح الكاش يبطل + إعادة تحقق live قبل الحرِج. Audit: **cache.invalidated**. الفشل: يُعاد الجلب من المصدر.

---

## 11. Audit Events Catalog

> أعمدة: الحدث · الفاعل · الهدف · الخطورة · حقول لازمة · الاحتفاظ · موافقة؟ · يظهر للأدمن؟ (retention أمثلة قابلة للضبط).
| الحدث | الفاعل | الهدف | خطورة | حقول لازمة | احتفاظ | موافقة؟ | للأدمن؟ |
|---|---|---|---|---|---|---|---|
| login | user | session | Info | user,ip,ts | 1y | لا | نعم |
| logout | user | session | Info | user,ts | 1y | لا | نعم |
| failed_login | user? | auth | Warn | attempt,ip,ts | 1–2y | لا | نعم |
| permission_denied | user | resource | Warn | user,resource,policy,ts | 2y | لا | نعم |
| role_assigned | admin | user/role | High | actor,target,role | 3y | حسب السياسة | نعم |
| role_removed | admin | user/role | High | actor,target,role | 3y | حسب السياسة | نعم |
| user_disabled | admin | user | High | actor,target,reason | 3y | حسب السياسة | نعم |
| screen_created | admin | screen | Info | actor,screen | 2y | لا | نعم |
| field_added | admin | field | Info | actor,field | 2y | لا | نعم |
| migration_generated | system/admin | migration | Info | migration,diff | 3y | لا | نعم |
| migration_approved | approver | migration | High | approver,migration | 3y | نعم | نعم |
| migration_rejected | approver | migration | Med | approver,reason | 3y | نعم | نعم |
| migration_applied | system | schema | High | migration,version | 3y | (بعد اعتماد) | نعم |
| record_viewed | user | record | Info | user,record,class | 6–12m | لا | نعم |
| record_created | user | record | Info | user,record | 2y | حسب workflow | نعم |
| record_updated | user | record | Info | user,record,diff | 2y | حسب workflow | نعم |
| record_deleted | user/admin | record | High | actor,record | 3y | غالباً | نعم |
| export_requested | user | dataset | High | user,scope,class | 3y | حسب السياسة | نعم |
| workflow_created | user | workflow | Info | user,wf | 2y | لا | نعم |
| workflow_approved | approver | workflow | High | approver,wf | 3y | نعم | نعم |
| workflow_rejected | approver | workflow | Med | approver,reason | 3y | نعم | نعم |
| workflow_activated | system | workflow | High | wf,version | 3y | (بعد اعتماد) | نعم |
| connector_added | admin | connector | High | actor,connector | 3y | نعم | نعم |
| connector_disabled | admin | connector | Med | actor,connector | 3y | حسب السياسة | نعم |
| app_connected | user | app | Med | user,app | 2y | حسب التطبيق | نعم |
| app_disconnected | user | app | Info | user,app | 2y | لا | نعم |
| model_changed | admin | capability | High | actor,cap,old,new | 3y | حسب السياسة | نعم |
| provider_changed | admin/ops | provider | High | actor,old,new | 3y | حسب السياسة | نعم |
| feature_flag_changed | admin | flag | High | actor,flag,old,new | 3y | حسب العلم | نعم |
| profile_changed | ops/sa | profile | Critical | actor,old,new | 5y | نعم | نعم |
| config_changed | ops/sa | config key | High | actor,key,old,new | 5y | نعم | نعم |
| file_uploaded | user | file | Info | user,file,class | 2y | لا | نعم |
| media_processed | system | media | Info | media,type,model | 1–2y | لا | نعم |
| ocr_completed | system | doc | Info | doc,engine | 1y | لا | نعم |
| rag_query_executed | user | query | Info | user,scope | 6–12m | لا | نعم |
| sql_query_generated | system | query | Info | user,query | 1y | لا | نعم |
| sql_query_executed | system | db(read) | Med | user,query,rows | 1y | لا | نعم |
| report_generated | user | report | Info | user,report | 2y | لا | نعم |
| cache_invalidated | system | cache key | Info | key,reason | 3–6m | لا | جزئي |
| service_health_alert | system | service | Warn/High | service,state | 1y | لا | نعم |
| backup_created | ops | backup | High | actor,target | 3y | نعم | Ops |
| restore_executed | ops | system | Critical | actor,source | 5y | نعم | Ops |

---

## 12. Risks and Trade-offs

- **Modular Monolith مقابل Microservices:** المونوليث المعياري أبسط تشغيلاً وأخف على جهاز واحد وأسرع تطويراً؛ ثمنه انضباط الحدود بين الـ modules. *Trade-off محسوم لصالح المونوليث المعياري*، مع تصميم يسمح باستخراج module لخدمة لاحقاً.
- **سهولة مقابل أمان:** تشغيل/إيقاف الخدمات من الواجهة أسهل لكنه خطر؛ *الحسم: capability toggles للأدمن، وlifecycle للعمليات فقط*، مع خدمات محميّة + Safe Mode + رسم تبعيات.
- **Ollama (dev) مقابل vLLM (prod):** سهولة مقابل تزامن؛ يُحلّ بالـ Gateway على عقد OpenAI-compatible وتبديل بالإعداد.
- **تراخيص AGPL (MinIO/Grafana/Loki/PyMuPDF) وإعادة ترخيص Redis:** *استخدام داخلي عادةً مقبول* لكن يجب مراجعة قانونية وتجنّب توزيع نسخ معدّلة كخدمة؛ بدائل: Valkey/SeaweedFS/pdfplumber/VictoriaMetrics.
- **OpenSearch/Qdrant ذاكرة عالية على dev:** يُخفَّف بـ Low-resource bundle (Postgres FTS/pgvector) مع الإبقاء المعماري.
- **الوسائط الثقيلة على MSI Titan:** المعمارية جاهزة، والتشغيل الفعلي للنماذج الثقيلة يُضبط عبر Registry حسب العتاد (fallback: صوت+keyframes).
- **هلوسة الـ LLM:** *الحسم:* No-Guessing + Validation (citations) + الحقيقة من المصادر فقط + validation لا تفشل مفتوحة.
- **تعقيد metadata-driven + التوليد:** يُضبط بخط ترحيل صارم (review/approval/versioning/audit) وشاشة توثيق.
- **قابلية النقل:** خطر انحراف dev/prod؛ *الحسم:* صورة واحدة، فرق إعداد فقط، اختبارات تكامل لكل profile، منع كود خاص ببيئة.

---

## 13. Open Decisions (تحتاج قراراً منك)

1. **مراجعة/اعتماد بدائل التراخيص:** Valkey بدل Redis؟ SeaweedFS بدل MinIO أم قبول AGPL داخلياً؟ Apache AGE بدل Neo4j؟ pdfplumber بدل PyMuPDF؟ (أستطيع التحقق من التراخيص الحالية بالبحث إن رغبت.)
2. **محرك OCR الأساسي للعربية:** PaddleOCR أم docTR أم Tesseract؟
3. **مزوّد الخدمة في dev:** Ollama فقط، أم Ollama + vLLM مبكراً؟
4. **نطاق Graph:** نؤجّله (off) أم نعتمد Apache AGE من البداية؟
5. **مستوى المراقبة في dev:** أساسي أم كامل (Prometheus/Grafana/Loki) منذ Local؟
6. **النماذج الفعلية لكل capability + سياسة تشغيل الثقيل** حسب العتاد.
7. **العدد المتزامن، عتاد الإنتاج، الأحجام، جرد الأنظمة، الـ IdP، مصفوفات الاعتماد/SoD** (نواقص سابقة تُحسم كإعدادات/قياسات).
8. **تأكيد Modular Monolith** كأسلوب معماري قبل الانتقال إلى Spec-driven development.

---

## 14. Expanded Roadmap (feature-based · بدون برومبتات تنفيذ)

> الترتيب مقترح بعد دراسة Feature Catalog؛ المبدأ: **الحوكمة قبل القدرة**، وde-risk أعلى مجهولية مبكراً، والوسائط جاهزة معمارياً من البداية. لكل مرحلة: الهدف · مميزات داخلة/خارجة · خدمات · مخرجات · قبول · مخاطر · لماذا قبل التالية.

**Phase 0 — Foundation &amp; Full-Stack Skeleton**
الهدف: كل الطبقات حاضرة وتقلع end-to-end، config-driven وportable. داخلة: Config/Profiles، Feature Flags، Service Registry، Monitoring، License/About، interfaces (LLM/Identity/Storage/DB-Router/Media)، كل الخدمات بإعداد demo. خارجة: أي منطق أعمال/صلاحيات/شاشات فعلية. خدمات: كلها (خفيفة). مخرجات: إقلاع كامل + /health أخضر + تبديل profile. قبول: تبديل Local→Prod بالإعداد؛ لا منطق أعمال. مخاطر: انحراف البيئات (يُضبط مبكراً). **قبل التالية:** لا شيء يُبنى بلا أساس قابل للنقل.

**Phase 1 — Governed Core + Screen Builder (Walking Skeleton)**
الهدف: إثبات التوليد المحكوم تحت الحوكمة end-to-end. داخلة: Auth(+IdP-adapter)، Organization، Permission spine، Metadata، Audit spine، Screen/Field Builder + Migration Review/Approval، Records أساسي. خارجة: RAG/Media/وكلاء/workflow كامل/متجر. خدمات: Auth/Org/Permission/Metadata/Record/Migration/Audit/Config/Flags. مخرجات: دورة توليد شاشة محكومة + CRUD مدقَّق. قبول: كل خطوة عبر Permission+Audit؛ لا DDL من نموذج؛ RTL. مخاطر: تعقيد الحوكمة. **قبل التالية:** الحوكمة والميتاداتا أساس كل ما بعدها.

**Phase 2 — Full Screen/Field Builder + Records + RLS/FLS**
الهدف: نضج البناء وإنفاذ العزل. داخلة: كل أنواع الحقول/التحققات، Row/Field-Level، Entity Profile مبدئي، شاشة توثيق كاملة. خارجة: وكلاء/وسائط/تكاملات. خدمات: Record/Metadata/Permission. مخرجات: شاشات معقّدة بعزل مدقَّق. قبول: RLS/FLS يعملان. مخاطر: أداء الاستعلام. **قبل التالية:** بيانات محكومة قبل بناء الـ workflows فوقها.

**Phase 3 — Workflows + Actions + Notifications**
الهدف: دورة حياة الـ workflows (نوعان). داخلة: Draft→Validation→Permission→Risk→Approval→Activation→Versioning→Rollback→Audit، Action/CTA، Notifications، Tasks/Projects. خارجة: RAG/وسائط. خدمات: Workflow/Task/Project/Notification. مخرجات: workflow مستخدم لا يتفعّل قبل اعتماد + rollback. قبول: SoD مطبّق؛ كل انتقال مدقَّق. مخاطر: تعارض/حلقات. **قبل التالية:** العمليات والحوكمة قبل إدخال الذكاء/الوسائط.

**Phase 4 — Full Authorization + Admin Feature Management**
الهدف: الصلاحيات الكاملة + حوكمة المزايا. داخلة: RBAC+ABAC+ReBAC، field/row-level، SoD، Need-to-know، Feature/Module Management (flags)، Safe Mode، رسم تبعيات، Security Policies. خارجة: وسائط ثقيلة. خدمات: Permission/Config/Flags/Security. مخرجات: سياسات مركّبة تُنفَّذ؛ تعذّر تعطيل خدمة أساسية من الواجهة. قبول: default-deny شامل. مخاطر: تصعيد صلاحية. **قبل التالية:** ضبط الوصول قبل فتح المعرفة/التكاملات.

**Phase 5 — Knowledge &amp; Media (RAG + Multimodal)**
الهدف: المعرفة والوسائط مفعّلة (نماذج خفيفة). داخلة: RAG/Retrieval، Document/OCR، **Media pipeline (صوت/صور/فيديو-keyframes)**، OKF، Model/Provider Registry UI، LLM Gateway، وكلاء (Retrieval/Validation/Reasoning/Media)، No-Guessing. خارجة: نماذج ثقيلة إن لم يناسب العتاد (قابلة للتوصيل). خدمات: RAG/Media/File/Gateway/Registry. مخرجات: رفع مستند/صوت/صورة→معالجة→فهرسة→استرجاع مصفّى بالصلاحية + provenance. قبول: تبديل نموذج نوع وسائط من الواجهة؛ الصلاحية قبل الاسترجاع. مخاطر: عتاد/جودة عربي/تسريب كاش. **قبل التالية:** المعرفة قبل الاستعلام المتقدّم والتقارير.

**Phase 6 — Data Query &amp; Reasoning + Chat + Reports**
الهدف: استعلام آمن وتقارير ودردشة مؤسسية. داخلة: Safe SQL Agent، Reasoning/Report، Long Reports، Chat في Enterprise UI. خارجة: تكاملات خارجية. خدمات: SQL/Report/Gateway. مخرجات: إجابات مسنودة؛ SQL قراءة فقط ضمن الصلاحية؛ تقرير طويل مُستشهَد. قبول: لا SQL خارج allow-list/RLS. مخاطر: حقن/هلوسة. **قبل التالية:** إتقان الاستعلام قبل ربط الأنظمة الخارجية.

**Phase 7 — Integration &amp; App Store**
الهدف: الربط الداخلي والمتجر. داخلة: Integration Management (MCP/API/Webhook/DB)، Enterprise App Store، ربط حسابات، استخدام التطبيقات في Chat/Tasks/Workflows/Reports/Notifications، بوابات اعتماد. خارجة: SaaS خارجي (اختياري لاحقاً). خدمات: Integration/AppStore/MCP. مخرجات: المستخدم يرى المسموح فقط ويستخدم تطبيقاً داخل الدردشة ضمن الصلاحية مع تدقيق. قبول: كل استدعاء ضمن صلاحية الحساب المربوط + مدقَّق. مخاطر: تنفيذ خطير/ربط ضار. **قبل التالية:** التكامل بعد نضج الحوكمة والمعرفة.

**Phase 8 — Operations, Scale &amp; Hardening**
الهدف: جاهزية الإنتاج والتوسع. داخلة: Monitoring/observability كامل، Deployment/Operations Controller، offline bundle/backup/restore، HA/تحمّل، Graph module (اختياري)، أدوات أمن (اختياري، نمط PentAGI/RedAmon في المتجر). خارجة: — . خدمات: Ops/Monitoring/Backup. مخرجات: ترقية Local→Production بالإعداد فقط؛ نسخ/استعادة متحقَّقة؛ lifecycle عبر طبقة العمليات. قبول: config-only promotion مُثبَت. مخاطر: تعقيد تشغيلي. **قبل التالية:** التصليب والتوسع بعد اكتمال الوظائف.

---

## 15. Final Recommendation

اعتمد **Modular Monolith** (backend واحد قابل للنشر، modules واضحة الحدود + workers للوكلاء/الوسائط + datastores منفصلة) مُدار بـ **Spec-driven development** (Spec Kit: constitution ثم spec/plan/tasks لكل module/مرحلة). هذا الأسلوب يحقّق في آنٍ: **كل الطبقات حاضرة**، **يعمل خفيفاً على MSI Titan**، **قابل للنقل بالإعداد فقط**، و**قابل للتوسع** (استخراج module إلى خدمة لاحقاً دون إعادة كتابة). ثبّت مبكراً: **Config Registry + Feature Flags + Service Registry** و**LLM Gateway على عقد OpenAI-compatible** و**Model/Provider Registry مربوط بالـ capabilities** و**Media Pipeline جاهز معمارياً**، مع **الحوكمة قبل القدرة** (الصلاحية قبل الاسترجاع، default-deny، Audit شامل)، و**فصل ثلاث طبقات تحكّم** (Capability=أدمن، Configuration=Super Admin، Operations=عمليات) وحماية الخدمات الأساسية.

**قبل الانتقال:** احسم بنود «Open Decisions» (خاصة بدائل التراخيص ومحرك OCR العربي وتأكيد Modular Monolith). بعدها نصمّم **المرحلة الأولى وحدها** في محادثة مستقلة.
