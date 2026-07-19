# تصنيف القرارات المفتوحة — Open Decisions Classification

> **Document Title:** Open Decisions Classification · **Version:** 2.4 — (Δ 2026-07-19: +فهرس دفعة G1 — Governance Foundation Baseline) (2.3: D1–D9 مدمجة؛ C1–C5 مُغلقة؛ +فهرس v0.8؛ +قسم إغلاق خط الأساس v1.0) · **Status:** Current / Accepted · **Date:** 2026-07-10
> **Supersedes:** v2.0 + قسم Open Decisions في الكتالوج (§13) والمنهجية (§19) — هذه الوثيقة هي **المرجع المُلزم الوحيد** للقرارات المفتوحة.
> **Authority Order:** المرتبة **4**. · **Related:** license-review.md · phase-roadmap.md · adr/README.md · coding-standards.md
> **Purpose:** تصنيف كل قرار إلى فئة توقيت واضحة حتى لا يوقف أي قرارٍ التصميمَ بلا داعٍ، ولا يدخل أي شيء التنفيذَ بلا حسم.

## الفئات الخمس (القاعدة المعتمدة)
| الفئة | المعنى | الأثر |
|---|---|---|
| **1 — Blockers قبل التصميم** | يمنع تصميم المراحل | **فارغة** — لا شيء يوقف التصميم |
| **2 — Blockers قبل التنفيذ** | يُحسم قبل كتابة أول كود للمرحلة المعنية | بوابة لكل مرحلة عند تنفيذها |
| **3 — Blockers قبل Docker Compose** | يُحسم قبل سحب/تفعيل الصورة المعنية | **بوابة متكررة** لكل صورة جديدة/مفعَّلة في أي مرحلة |
| **4 — Blockers قبل التوزيع النهائي** | يُحسم قبل أول release خارج الفريق | لا يوقف التطوير الداخلي |
| **5 — Configurable** | يبقى مفتاح إعداد/سياسة | لا يوقف شيئاً |

## المحسوم حديثاً — قرارات ما قبل التنفيذ D1–D9 (2026-07-04)
| # | القرار المحسوم | المرجع |
|---|---|---|
| D1 | **Frontend = React + Vite + TypeScript + Tailwind + shadcn/ui-style** (SPA مستقلة تستهلك OpenAPI/SDK؛ لا Next.js — لا SSR/SEO داخلياً؛ SvelteKit رُفض) | ADR-0017 |
| D2 | **Backend مؤكَّد** = Python + FastAPI + Pydantic + SQLAlchemy + Alembic + PostgreSQL + workers | ADR-0001/0003 |
| D3 | **C5 محسوم:** uv + pnpm + lockfiles + pinned + reproducible + offline caches + install/verify scripts | coding-standards §7 |
| D4 | **Cache/Queue/Lock:** ثلاث واجهات بافتراضي **memory/PostgreSQL**؛ Valkey **optional-ready** (ليس إلزامياً في P0/P1) | ADR-0018 |
| D5 | **ObjectStorageProvider** بافتراضي **local filesystem**؛ المزوّد (MinIO/SeaweedFS/S3) كان يُحسم بمرحلة الملفات — **حُسم افتراضي الإنتاج الموزَّع في v1.0-baseline: SeaweedFS؛ MinIO مشروط Legal** | ADR-0019 |
| D6 | **Observability Baseline:** Audit-PG + JSON logs خارج PG + Log Viewer + Health + Error Catalog + IDs + /metrics اختياري؛ لا Grafana/Loki/Graylog الآن | ADR-0020 |
| D7 | **GitHub الآن** + قناة نقل مغلقة موقّعة؛ Git داخلي (Gitea/GitLab) = **Backlog** | ADR-0022 |
| D8 | **Reference-aware clean implementation** — سياسة مُغلقة مُلزمة (ليست قراراً مفتوحاً) | ADR-0021 + coding-standards §9 |
| D9 | **حدود Admin UI** مؤكدة (capabilities من الواجهة؛ البنية الحساسة config/Ops؛ audit + approval حسب السياسة) | ADR-0008 |

---

## الجدول التفصيلي — القرارات المفتوحة والمُغلقة

> الأعمدة: القرار · الفئة · لماذا · يوقف التصميم؟ · يوقف التنفيذ؟ · متى يُحسم · الخيارات · التوصية/الحالة · License Review؟ · Configurable؟

| القرار | الفئة | لماذا | يوقف التصميم؟ | يوقف التنفيذ؟ | متى يُحسم | الخيارات | التوصية/الحالة | License Review؟ | Configurable؟ |
|---|---|---|---|---|---|---|---|---|---|
| **Frontend stack** | **مُغلق (D1)** | قرار لا-رجعة عملياً | لا | لا | مُغلق 2026-07-04 | — | **React + Vite + TS + Tailwind + shadcn-style**؛ Next.js غير معتمد؛ SvelteKit مرفوض | نعم (صفوف شكلية قبل أول كود) | — |
| **Backend stack** | **مؤكَّد (D2)** | AI/RAG ecosystem | لا | لا | مُغلق | — | Python + FastAPI + Pydantic + SQLAlchemy + Alembic + PostgreSQL | نعم (شكلية) | — |
| مراجعة تراخيص ستاك الكود المعتمد | 2 (لمرحلة 0) | قاعدة «لا dependency بلا صف» | لا | **تنفيذ Phase 0** | قبل أول كود | — | تعبئة/إقرار صفوف: React/Vite/TS/Tailwind/shadcn/FastAPI/Pydantic/SQLAlchemy/Alembic/uv/pnpm | **نعم (شكلية متوقعة)** | — |
| **Git host (C4)** | **مُغلق (D7)** | التطوير online أولاً | لا | لا | مُغلق | GitHub / Gitea / GitLab | **GitHub الآن**؛ Git داخلي = **Backlog** (فقط عند نشوء تطوير داخل الشبكة)؛ قناة نقل كود موقّعة ضمن offline bundle | نعم (لأداة Git الداخلية إن فُعّلت) | — |
| **معايير الأدوات (C5)** | **مُغلق (D3)** | تثبيت قبل أول كود | لا | لا | مُغلق | uv/poetry · pnpm/npm | **uv + pnpm**؛ الإصدارات تُثبَّت عند التنفيذ في coding-standards | لا | تُوثَّق كمعيار |
| **Redis vs Valkey (C1)** | **مُغلق نهائياً (D4 + D9c/ADR-0018 — v1.0-baseline)**؛ التفعيل = فئة 3 | لا حاجة فعلية في P0/P1 | لا | لا (يوقف فقط تفعيل الصورة) | مُغلق؛ التفعيل عند بلوغ محفزات ADR-0018 | Redis (RSAL/SSPL) / **Valkey (BSD)** | الافتراضي **memory/PostgreSQL** عبر CacheProvider/QueueProvider/LockProvider؛ **Valkey افتراضي بروفايل التوسع — مسألة Redis مقفلة لا تُطرح مجدداً** | **نعم قبل تفعيل الصورة** | نعم — تبديل بالإعداد |
| **Object Storage (C2): MinIO / SeaweedFS / S3** | **مُغلق (D5 + D8/ADR-0019 — v1.0-baseline)**؛ التفعيل = فئة 3 (+4 للتوزيع) | التخزين ≠ OCR/استخراج؛ لا ملفات كبيرة قبل P5 | لا | لا (يوقف تفعيل الصورة فقط) | مُغلق؛ التفعيل قبل compose مرحلة الملفات | MinIO (AGPL) / SeaweedFS (Apache-2) / S3-compatible آخر | الافتراضي **local filesystem**؛ **الإنتاج الموزَّع: SeaweedFS افتراضاً؛ MinIO adapter مشروط باعتماد قانوني**؛ لا ربط بالكود باسم أداة | **نعم (MinIO = Legal)** | نعم |
| **Monitoring stack (C3)** | **مُغلق (D6)** — baseline | enterprise-auditability بلا وزن مبكر | لا | لا | مُغلق؛ التوسعة P8 | baseline / Grafana+Loki / VictoriaMetrics | **الخط الأساسي**: Audit-PG + JSON logs + Log Viewer + Health + Error Catalog + IDs + /metrics اختياري؛ OTel adapter مستقبلاً | **نعم عند التوسعة (Grafana/Loki = Legal)** | نعم |
| محرك OCR العربي | 5 (+2 لترخيص المحرك عند P5) | capability في الـ Registry | لا | صف مراجعة عند تنفيذ P5 | اختيار افتراضي بتصميم/تنفيذ P5 | Tesseract / **PaddleOCR** / docTR | قياس جودة عربي ثم الاختيار | نعم (شكلية Apache-2) | **نعم** — يبدَّل من الأدمن |
| PDF tooling (PyMuPDF؟) | 2 (لمرحلة 5) | dependency كود عند تنفيذ media | لا | تنفيذ Phase 5 | قبل تنفيذ P5 | PyMuPDF (AGPL) / **pdfplumber+pypdf** / Tika | الافتراضي pdfplumber/pypdf + Tika؛ PyMuPDF بعد Legal فقط | **نعم (Legal لـ PyMuPDF)** | نعم — parser قابل للتبديل |
| ffmpeg (بناء الصورة) | 2 (لمرحلة 5) + 3 عند دخوله | الترخيص حسب خيارات البناء | لا | تنفيذ Phase 5 | قبل تنفيذ P5 | بناء LGPL-only / GPL | بناء LGPL-only مفضّل + توثيق الخيارات | **نعم** | جزئياً |
| تراخيص أوزان النماذج | **2 (P5) + 4** — بوابة مزدوجة | تشغيل = dependency؛ تضمين = توزيع | لا | تنفيذ P5 (تشغيل)؛ release (تضمين) | قبل تشغيل كل نموذج + قبل أول release | حسب النموذج | صف مستقل لكل نموذج | **نعم** | اختيار النموذج: نعم (Registry) |
| Graph: Neo4j / Apache AGE / تأجيل | 5 | Optional-off | لا | لا | عند الحاجة الفعلية | تأجيل / **AGE** / Neo4j (GPLv3) | يبقى off؛ إن لزم: Apache AGE | نعم (عند التفعيل) | **نعم** |
| Open WebUI usage status | محسوم (مرجع فقط) | Enterprise UI هي الواجهة | لا | لا | مُغلق | مرجع / طبقة داخلية (مشروط Legal) | **مرجع دراسة فقط** خاضع لسياسة Reference-aware (D8)؛ v0.6.6+ ممنوع white-label | نعم (إن استُخدم فعلياً) | — |
| Qdrant + OpenSearch | محسوم + مراجعة شكلية | **حاضران في Local Demo** (constitution م12) | لا | لا (صف شكلي) | مُغلق (ADR-0004) | — | pgvector/PG-FTS **fallback ضمن low-resource bundle فقط** | نعم (شكلية Apache-2) | إعدادات الحجم فقط |
| IdP (LDAP/AD/Keycloak/OIDC/SAML) | 5 | Local Auth + IdP-adapter | لا | لا | عند ربط المؤسسة (بعد P1) | LDAP / AD / Keycloak / OIDC / SAML | Local الآن؛ الربط لاحقاً adapter بلا تعديل جوهر | نعم (لمكوّن الربط) | **نعم** |
| Production sizing | 5 | قياسات وإعدادات | لا | لا | قبل نشر الإنتاج (P8) | حسب المؤسسة | افتراض تزامن 2–5% من 20–30k للتحقق؛ الأحجام config | لا | **نعم** |
| Compose الآن / K8s-OpenShift لاحقاً | محسوم الآن + 5 مستقبلاً | Compose يكفي dev/staging | لا | لا | عند الحاجة (P8+) | Compose / K8s / OpenShift | Compose الآن؛ K8s لاحقاً **manifests فقط دون كود** | لا | **نعم** |
| بنية Postgres في Local (C6) | 5 | DatabaseRouter يجعلها إعداداً | لا | لا | افتراض معتمد | 1×4 / 4×1 | **instance واحد ×4 قواعد** في Local؛ الفصل بالإعداد في الإنتاج | لا | **نعم** |
| Ollama/vLLM في compose مبكراً (C7) | 5 | تعريف مطفأ لا تشغيل | لا | لا | مع P0.4 | تعريف مطفأ / تأجيل | تعريفهما بعلم مطفأ (حضور معماري) | نعم (شكلية) | **نعم** |
| TLS/PKI + توقيع حزمة النقل | 4 (تُقدَّم إلى «قبل أول Staging شبكي» إن وُجد) | تشغيلي/أمني قبل النشر | لا | لا | قبل أول بيئة شبكية أو release | PKI داخلي / شهادات مؤسسة | يُحسم مع فريق العمليات | لا | جزئياً |
| موقف AGPL النهائي عند التوزيع | 4 | استخدام داخلي ≠ توزيع | لا | لا | قبل أول release | رأي قانوني / بدائل Apache-2 | رأي قانوني قبل أي توزيع (يشمل MinIO/Grafana/Loki إن اعتُمدت) | **نعم (Legal)** | — |
| اكتمال Attribution/About | 4 | شرط إغلاق للتوزيع | لا | لا | قبل أول release | — | تُبنى تدريجياً من license-review | — | — |
| مصفوفات الاعتماد + SoD التفصيلية | 5 | سياسات في platform_db | لا | لا | مع P3/P4 كإعدادات | حسب المؤسسة | قابلة للضبط من الأدمن | لا | **نعم** |
| جرد الأنظمة الداخلية + عقودها | 2 (لمرحلة 7) | لا تكامل بلا جرد | لا | تنفيذ Phase 7 | قبل تنفيذ P7 | حسب المؤسسة | يبدأ حصره مبكراً | نعم (لكل connector) | — |

---

## خلاصة الفئات (بعد D1–D9)
- **فئة 1:** فارغة — لا شيء يوقف التصميم (بما فيه تصميم Phase 1).
- **فئة 2 (قبل أول كود لكل مرحلة):** P0 = صفوف ترخيص الستاك المعتمد فقط · P5 = PDF-tooling + ffmpeg + ترخيص محرك OCR + أوزان النماذج (بوابة 1) · P7 = جرد الأنظمة وعقودها.
- **فئة 3 (بوابة تفعيل متكررة — قبل Docker Compose للصورة):** Valkey · MinIO أو SeaweedFS · أي خادم مراقبة · أي صورة جديدة مستقبلاً. **لا بوابة فئة 3 على P0.4** (الصور الفعّالة Postgres/Qdrant/OpenSearch تمرّ بصف شكلي).
- **فئة 4 (قبل التوزيع/الإنتاج):** موقف AGPL · أوزان النماذج (بوابة 2) · TLS/PKI + توقيع الحزمة · اكتمال Attribution.
- **فئة 5 (Configurable):** OCR engine · Graph · النماذج لكل capability · IdP · sizing · بنية Postgres · SoD/مصفوفات الاعتماد · K8s لاحقاً.

**ملاحظات حاكمة:** «Reference-aware clean implementation» **سياسة مُغلقة** (ADR-0021) وليست قراراً مفتوحاً · بنود الفئتين 2/3 تُحسم عبر License Review Workflow داخل نافذتها · بنود 5 تُوثَّق في configuration.md.

## فهرس القرارات المفتوحة لحزم v0.5–v0.7 (Δ ما-بعد الدمج 2026-07-08)
> هذه القرارات تُدار **نصاً داخل ملفاتها الحاضنة** (المصدر المعياري)؛ هذا الجدول فهرس تصنيفي بفئة التوقيت فقط، على نسق هذا السجل.
| OD | الملف الحاضن | فئة التوقيت | خلاصة سطرية |
|---|---|---|---|
| OD-IX-1..3 | ui/UI_INTERACTION_MODEL.md | عند تفعيل P1 (Clarify) | حفظ حالة drawer/فتح تلقائي للتبويبات/زر «فتح كامل» |
| OD-VZ-1..3 | ui/UI_VISIBILITY_RULES.md | عند تفعيل P1 (Clarify) | كتالوج أسباب disabled/عتبة مرجع التدقيق/استثناء عدّاد admin.audit |
| OD-PD-1..3 | ui/UI_PROGRESSIVE_DISCLOSURE.md | عند تفعيل P1 (Clarify) | مؤشر الحقول المطوية/تذكّر التبويب/سقف أزرار البطاقات |
| OD-MX-1 | ui/UI_PROVIDER_MODEL_MANAGEMENT.md | عند تفعيل P6 (Clarify) | إظهار محدد Model Profiles للمستخدم (التوصية: مخفي افتراضياً) |
| OD-MX-3 | ui/UI_PROVIDER_MODEL_MANAGEMENT.md | Ops/config لاحقاً | تحكم يدوي warm/unload — قراءة فقط في v1 |
| OD-MX-4 | ui/UI_PROVIDER_MODEL_MANAGEMENT.md | Ops/config (P5/P6) | مفتاح عتبة slow |
| OD-RUN-1 | ui/UI_RUN_EXECUTION_MODEL.md | Ops/config (P6) | عتبة auto-offload لحجم المخرجات |
| OD-RUN-2 | ui/UI_RUN_EXECUTION_MODEL.md | عند تفعيل P6 (Clarify) | إقرار typed-ack لاعتماد تقرير جزئي |
| OD-RUN-3 | ui/UI_RUN_EXECUTION_MODEL.md | Ops/config | مدة احتفاظ/أرشفة قائمة التشغيلات |
| OD-TPL-1 | ui/UI_RUN_EXECUTION_MODEL.md | **مؤجل بقرار المالك (غير معتمد)** | template.create — لا يدخل إلا بقرار صريح |
| OD-AB-4 | ui/UI_ACTION_BUTTON_MODEL.md | مرآة OD-TPL-1 | نفس الحكم على مستوى كتالوج الأفعال |
| OD-NM-1 (المعدَّل) | ui/UI_FIELD_NAMING.md | محسوم جزئياً + Clarify P3 | run/escalate/compare معتمدة (2026-07-08)؛ بقية الكتالوج تُثبَّت في P3 |
| OD-PSC-1 | architecture/PROVIDER_MODEL_SECRET_CONFIG_SPEC.md | عند تفعيل P5/P6 (Clarify) | مخزن الأسرار لأول تنفيذ (التوصية: env + ملفات محلية) |
| OD-PSC-2 | architecture/PROVIDER_MODEL_SECRET_CONFIG_SPEC.md | عند تفعيل P5/P6 (Clarify) | حساسية endpoint_ref (التوصية: حساس افتراضياً) |
| OD-PSC-3 | architecture/PROVIDER_MODEL_SECRET_CONFIG_SPEC.md | Ops/config (P5/P6) | مدة كاش الاكتشاف |

## فهرس قرارات دفعة v0.8 — Conversational & Workflow (Δ 2026-07-10)
> **كلها مقفلة بقرار SA (2026-07-10)** — المصدر المعياري نصاً داخل ملفاتها الحاضنة؛ هذا فهرس تصنيفي فقط.
| OD | الملف الحاضن | الحالة | خلاصة سطرية |
|---|---|---|---|
| OD-WS-4 | ui/UI_AI_WORKSPACE_MODEL.md §14 | **مقفل** | وضعا عرض ws.main (بطاقات/محادثة) كتفضيل مستخدم — عرضيّ صرف، لا تغيير سلوكياً خادمياً (ورد في دفعة SA بمعرّف OD-WS-2؛ عُدِّل الترقيم لتفادي التصادم) |
| OD-BLD-1 | ui/UI_ADMIN_CONSOLE_MODEL.md §4-C | **مقفل** | أوضاع الباني الثلاثة (تقليدي/محادثي/مدمج) فوق خط draft→migration→checks→approval→apply بلا تغيير؛ الـ LLM يكتب metadata فقط |
| OD-WF-1 | phases/designs/DELTA_V08_FR_WORKFLOW_ORG.md §4 | **مقفل** | الرفض النهائي والإرجاع للمعالجة خياران متمايزان في سطح القرار |
| OD-WF-2 | phases/designs/DELTA_V08_FR_WORKFLOW_ORG.md §4 | **مقفل** | الإرجاع/التوجيه للمكلَّف الحالي فقط (`workflow.return_route`) |
| OD-ORG-1 | phases/designs/DELTA_V08_FR_WORKFLOW_ORG.md §4 | **مقفل** | الشجرة التنظيمية للتوجيه/التكليف فقط — لا RLS مشتقاً منها في v1 |

---

## إغلاق خط الأساس المعماري v1.0-architecture-baseline (2026-07-10)

### (أ) قرارات أُغلقت عند خط الأساس (المرجع المعياري: ملف الـ ADR المذكور)
| القرار المُغلق | الخلاصة | ADR |
|---|---|---|
| افتراضي تخزين الكائنات | filesystem محلياً؛ **SeaweedFS افتراضي الإنتاج الموزَّع**؛ MinIO adapter مشروط باعتماد قانوني | ADR-0019 |
| Cache/Queue/Lock | الآن memory/PostgreSQL (SKIP LOCKED + advisory locks)؛ **بروفايل التوسع Valkey — مسألة Redis مقفلة** + محفزات انتقال موثقة | ADR-0018 |
| طوبولوجيا البحث | PG مصدر الحقيقة · Qdrant متجهي · OpenSearch نصي/هجين؛ pgvector/PG-FTS بروفايل low_resource اختياري فقط | ADR-0004 |
| عقد الواجهة/الخادم | REST أساسي + OpenAPI عقد رسمي + SSE للبث؛ types مولّدة + غلاف fetch رفيع؛ WebSocket بشرط ADR | ADR-0025 |
| موضع الواجهة | `/frontend` داخل مستودع المنصة (monorepo-lite)؛ الفصل لاحقاً عبر ADR | ADR-0017 |
| سياسة تغليف الوحدات | حدود منطقية لا عدد نهائياً؛ packaging map أثر تنفيذي يتغيّر دون ADR؛ ملكية الجداول لكل وحدة دائماً؛ شروط الاستخراج الخمسة | ADR-0026 |
| الهوية والتجميد | Enterprise AI Platform with Progressive Implementation + تجميد المعمارية عند الوسم (م21/م22) | ADR-0023 · ADR-0028 |

### (ب) قيم تشغيلية لا قرارات معمارية
تُضبط **بالقياس لكل نشر** ولا تُعامل قرارات معمارية مفتوحة ولا تدخل هذا السجل كبنود: أعداد النسخ (replicas) · أحجام النماذج · مدد الاحتفاظ النهائية · أحجام التخزين · حدود التزامن · تحجيم GPU للإنتاج. (المرجع: agent-execution-model §11 — توضيح القيم التشغيلية.)

### (ج) قرار مسجَّل — فهرس مواصفات قابل للقراءة الآلية
| OD | الموضوع | الفئة | الحالة |
|---|---|---|---|
| OD-IDX-1 | إنشاء manifest آلي للمواصفات (index.yaml) | — | **مرفوض الآن بقرار SA (2026-07-10)** — لا يُعاد فتحه إلا عند وجود مستهلك آلي فعلي (أداة/خط CI يقرأه)؛ حينها ADR/قرار جديد |

- F-3 (استعادة حزمة v0.3): مغلقة 2026-07-10 — الملفات العشرة مستعادة بمساراتها بلافتة حالة، والأصل الكامل مؤرشف في superseded/ ببصمته؛ نسخة agent-execution-model v0.3 متجاوَزة بخليفتها.

## فهرس قرارات دفعة «تنحية Flutter + جسر Open WebUI» (Δ 2026-07-11)
> المصدر المعياري نصاً في ملفَي الـ ADR؛ هذا فهرس تصنيفي فقط (قاعدة عدم التكرار).
| القرار | الملف الحاضن | الحالة | خلاصة سطرية |
|---|---|---|---|
| مبدأ العميل القابل للاستبدال | decisions/adr/ADR-0029-replaceable-client-principle.md | **مقفل — دُستر (م23، ‏2026-07-11)** | كل عميل يستهلك العقود فقط؛ لا حقيقة/صلاحيات/قواعد عمل/DB في أي عميل؛ الخادم يعيد التحقق ويملك القرار؛ اختبار الاستبدال معيار قبول مؤجل (سجل المؤجلات) |
| ‏Open WebUI واجهة مؤقتة | decisions/adr/ADR-0030-openwebui-temporary-chat-interface.md | **مقفل** (التفعيل خلف بوابات؛ الخروج بخطة) | ‏interim حصراً ضمن شرط م6؛ React خط الأساس بلا إعادة فتح؛ لا اعتماد على جداول Open WebUI الداخلية |


## فهرس قرارات دفعة G1 — Governance Foundation Baseline (Δ 2026-07-19)
> قرارات المالك في G0 (أمر 2026-07-19) قُنّنت كالتالي — **لا إعادة ترقيم لأي قرار قائم، ولا تغيير في حالة أي OD معلق** (التسعة Clarify لمرحلة P1 وبنود Ops-config تبقى كما هي بمواطنها في `methodology/PHASE_EXECUTION_STANDARD.md §2`).

| القرار | الحسم | التقنين |
|---|---|---|
| ‏Q1 عميل الواجهة | ‏Next.js client-only عبر Rocket بالحراس الأربعة | **ADR-0031** (‏ADR-0017 ‏Superseded-in-scope) |
| ‏Q2 تخزين السجلات الديناميكية | هجين: نواة + JSONB + ترويج مقنن؛ ‏UUIDv7 (توليد app/DB) | **ADR-0032** |
| ‏Q3 مستوى الأتمتة | ‏L1 لأول حزمتين ثم L2 افتراضي للمنخفض؛ مسارات محمية | **ADR-0033** |
| ‏Q4 ظهور المستودعات | عامة مؤقتاً؛ خصخصة = بوابة G6 | **ADR-0036** |
| ‏Q5 الهوية | ‏AQL Enterprise AI Platform — by AQLORA | ‏`knowledge/BUSINESS_GLOSSARY.md §1` |
| ‏DR-1 الترخيص | إشعار **Proprietary — All Rights Reserved © 2026 AQLORA**؛ لا Open Source؛ مراجعة قانونية قبل الإطلاق (مؤجلات) | **ADR-0036 بند 2** |
| ‏DR-2 أول حزمتين | ‏FP-0001 = ‏Retrofit ‏`admin.record_types` · ‏FP-0002 = بناء `admin.org` | **ADR-0033 بند 2** + عقود البذرة |
| مهارات التطوير | ‏subset مثبت من Superpowers ‏v6.1.1@d884ae0 | **ADR-0034** |
| طبقة العقود + المشتقات المولَّدة + ‏DGP | ‏contracts/ موطن التأليف؛ ‏BRD/FRD/… ‏GENERATED؛ المولد يُبنى في P2 | **ADR-0035** |
| ‏OD-IDX-1 | **محترم كما هو**: ‏`INDEX.md` بشري القراءة هو مصدر الفهرسة الحاكم — لا index.yaml/manifest في هذه الدفعة | ‏ADR-0035 بند 7 |
| ‏OD-P3-2 (canvas) | يبقى مؤجلاً كما هو؛ ‏canvas تجربة aql مؤشَّر **CC-WF-1** يُحسم ببوابته لا صمتاً | عقد `contracts/screens/admin.workflows.md §6` |
