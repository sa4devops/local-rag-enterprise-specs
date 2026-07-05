# تصنيف القرارات المفتوحة — Open Decisions Classification

> **Document Title:** Open Decisions Classification · **Version:** 2.1 — Final (D1–D9 مدمجة؛ C1–C5 مُغلقة) · **Status:** Current / Accepted · **Date:** 2026-07-04
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
| D5 | **ObjectStorageProvider** بافتراضي **local filesystem**؛ المزوّد (MinIO/SeaweedFS/S3) يُحسم بمرحلة الملفات | ADR-0019 |
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
| **Redis vs Valkey (C1)** | **مُغلق هيكلياً (D4)**؛ التفعيل = فئة 3 | لا حاجة فعلية في P0/P1 | لا | لا (يوقف فقط تفعيل الصورة) | عند أول حاجة (غالباً P5/P6 أو P8) | Redis (RSAL/SSPL) / **Valkey (BSD)** | الافتراضي **memory/PostgreSQL** عبر CacheProvider/QueueProvider/LockProvider؛ Valkey optional-ready مفضَّل على Redis | **نعم قبل تفعيل الصورة** | نعم — تبديل بالإعداد |
| **Object Storage (C2): MinIO / SeaweedFS / S3** | **مؤجَّل لمرحلة الملفات (D5)**؛ التفعيل = فئة 3 (+4 للتوزيع) | التخزين ≠ OCR/استخراج؛ لا ملفات كبيرة قبل P5 | لا | لا (يوقف تفعيل الصورة فقط) | قبل compose مرحلة الملفات/الوسائط | MinIO (AGPL) / SeaweedFS (Apache-2) / S3-compatible آخر | الافتراضي **local filesystem** عبر ObjectStorageProvider؛ لا ربط بالكود باسم أداة | **نعم (MinIO = Legal)** | نعم |
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
