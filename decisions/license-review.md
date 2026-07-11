# license-review.md — سجل مراجعة التراخيص (بوابة إلزامية)

> **Version:** 1.2 (v1.0-architecture-baseline: صفوف SeaweedFS/MinIO/Valkey/Redis مُحدَّثة وفق ADR-0018/0019 + إصدارات P0 تُثبَّت في lockfiles + فقرة السياسة وفق D12) · **Status:** Current / Accepted · **Date:** 2026-07-10 (الأصل 2026-07-04) · **Authority:** ينفّذ constitution م7 وMethodology §15.
> **القاعدة:** لا يدخل أي **tool / package / container image / model weights** إلى المنتج قبل صف معتمد هنا **للإصدار/الصورة المحددة**. الترقية تعيد المراجعة. البوابة **متكررة** لكل إضافة جديدة (فئة 2 قبل تنفيذ المرحلة، فئة 3 قبل دخول compose).
> **قيم القرار:** Approved · Conditional (بشروط مثل attribution أو داخلي-فقط) · Rejected · **Needs Review** (متساهلة متوقعة، تحتاج تثبيت الإصدار) · **Needs Legal Review** (AGPL/SSPL/RSAL/قيود branding أو توزيع).

| tool/package/image/model | version | official source | license | usage type | modification? | redistribution? | white-label risk? | offline compatible? | attribution required? | legal risk | decision | notes |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| PostgreSQL | تُثبَّت في lockfiles عند تنفيذ Phase 0 | postgresql.org | PostgreSQL | container image | لا | نعم | لا | نعم | لا | منخفض | Needs Review | قواعد ×4 بمستخدم least-privilege لكل قاعدة |
| Qdrant | تُثبَّت في lockfiles عند تنفيذ Phase 0 | qdrant.tech | Apache-2.0 | container image | لا | نعم | لا | نعم | نعم (NOTICE) | منخفض | Needs Review | حاضر في Local Demo (ADR-0004) |
| OpenSearch | تُثبَّت في lockfiles عند تنفيذ Phase 0 | opensearch.org | Apache-2.0 | container image | لا | نعم | لا | نعم | نعم | منخفض | Needs Review | حاضر في Local بإعداد heap خفيف |
| Redis | — (لا يُستخدم) | redis.io | RSAL/SSPL (متغيّر) | container image | لا | مقيّد | لا | نعم | — | **مرتفع** | **مقفل — لا يُستخدم (D9c/ADR-0018)** | مسألة Redis أُغلقت نهائياً في v1.0-baseline؛ البديل المعتمد Valkey |
| Valkey | تُثبَّت عند التفعيل (فئة 3) | valkey.io | BSD-3 | container image | لا | نعم | لا | نعم | لا | منخفض | Needs Review | **افتراضي بروفايل التوسع (D9c/ADR-0018)** — كاش/أقفال/جلسات/طابور موزَّعة؛ يُفعَّل عند بلوغ محفزات ADR-0018 بعد المراجعة؛ الافتراضي الحالي memory/PostgreSQL |
| MinIO | تُثبَّت عند الاعتماد (إن اعتُمد) | min.io | AGPL-3.0 | container image | لا | AGPL شروط | لا | نعم | نعم | **مرتفع عند التوزيع** | **Needs Legal Review** | **adapter اختياري فقط — لا يُستخدم إلا بعد اجتياز المراجعة القانونية (D8/ADR-0019)**؛ الموقف النهائي قبل أي release (فئة 4) |
| SeaweedFS | تُثبَّت عند التفعيل (فئة 3) | seaweedfs | Apache-2.0 | container image | لا | نعم | لا | نعم | نعم | منخفض | **Needs Review (آمن — مفضَّل)** | **افتراضي الإنتاج الموزَّع لتخزين الكائنات (D8/ADR-0019)**؛ S3-compatible عبر ObjectStorageProvider |
| Neo4j Community | (حدِّد) | neo4j.com | GPL-3.0 | container image (optional-off) | لا | GPL شروط | لا | نعم | — | متوسط | **Needs Legal Review** | لا يدخل compose Local؛ البديل AGE |
| Apache AGE (بديل Graph) | (حدِّد) | age.apache.org | Apache-2.0 | Postgres extension | لا | نعم | لا | نعم | نعم | منخفض | Needs Review | يُفعَّل فقط مع Graph-enabled |
| SQLite | تُثبَّت في lockfiles عند تنفيذ Phase 0 | sqlite.org | Public Domain | dependency (tests) | لا | نعم | لا | نعم | لا | منخفض | Needs Review | اختبارات/محلي فقط |
| Alembic | تُثبَّت في lockfiles عند تنفيذ Phase 0 | sqlalchemy.org | MIT | dependency | لا | نعم | لا | نعم | لا | منخفض | Needs Review | أداة الترحيل داخل غلاف الحوكمة |
| FastAPI (+Starlette/Pydantic) | تُثبَّت في lockfiles عند تنفيذ Phase 0 | fastapi.tiangolo.com | MIT | dependency | لا | نعم | لا | نعم | لا | منخفض | Needs Review | Backend framework |
| React / Vite / TypeScript | تُثبَّت في lockfiles عند تنفيذ Phase 0 | react.dev / vitejs.dev / typescriptlang.org | MIT / Apache-2 | dependency + build tool | لا | نعم | لا | نعم | لا | منخفض | Needs Review | ستاك الواجهة المعتمد (D1/ADR-0017)؛ **Next.js غير معتمد** |
| Tailwind CSS | تُثبَّت في lockfiles عند تنفيذ Phase 0 | tailwindcss.com | MIT | dependency | لا | نعم | لا | نعم | لا | منخفض | Needs Review | RTL عبر logical properties |
| shadcn/ui | تُثبَّت في lockfiles عند تنفيذ Phase 0 | ui.shadcn.com | MIT | **copy-in** | نعم (ننسخ ونعدّل) | نعم | لا | نعم | لا | منخفض | Needs Review | مكوّنات تُنسخ للمستودع |
| uv | تُثبَّت في lockfiles عند تنفيذ Phase 0 | astral.sh/uv | MIT/Apache-2 | dev tool | لا | نعم | لا | نعم | لا | منخفض | Needs Review | مدير حزم Python المعتمد (D3) + offline cache |
| pnpm | تُثبَّت في lockfiles عند تنفيذ Phase 0 | pnpm.io | MIT | dev tool | لا | نعم | لا | نعم | لا | منخفض | Needs Review | مدير حزم الواجهة المعتمد (D3) + offline store |
| OpenWebUI | v0.6.5 للدراسة فقط | github.com/open-webui | BSD-3 حتى 0.6.5؛ 0.6.6+ قيود branding/مستخدمين | **reference only — ليس dependency** | – | – | نعم (0.6.6+) | – | – | متوسط | **Conditional (مرجع فقط)** | لا يُنسخ كوده؛ خاضع لسياسة Reference-aware (ADR-0021) |
| OpenWebUI (container image — interim chat client) | **v0.6.5 مثبَّت (لا latest)** — digest يُسجَّل إلزامياً عند أول سحب/اعتماد تشغيلي | ghcr.io/open-webui/open-webui | BSD-3 ‏(v0.6.5)؛ 0.6.6+ رخصة Open WebUI بقيود branding | container image (واجهة محادثة مؤقتة — ADR-0030) | لا (تشغيل كما هي — لا fork ولا نسخ كود) | لا (استخدام داخلي) | **نعم عند أي white-label — ممنوع** | نعم | نعم (إبقاء الهوية/الإشعارات) | متوسط | **Needs Legal Review** | بوابة تفعيل ADR-0030: لا تشغيل قبل اعتماد هذا الصف؛ ‏scaffold فقط حالياً؛ الترقية لإصدار 0.6.6+ تعيد المراجعة (قيود الرخصة الجديدة) |
| Ollama | (حدِّد) | ollama.com | MIT | container image (dev) | لا | نعم | لا | نعم | لا | منخفض | Needs Review | provider خلف الـ Gateway |
| vLLM | (حدِّد) | vllm.ai | Apache-2.0 | container image (prod) | لا | نعم | لا | نعم | نعم | منخفض | Needs Review | provider الإنتاج |
| SGLang / llama.cpp | (حدِّد) | — | Apache-2 / MIT | container/dep (اختياري) | لا | نعم | لا | نعم | — | منخفض | Needs Review | بدائل serving/CPU |
| Prometheus | (حدِّد) | prometheus.io | Apache-2.0 | container image | لا | نعم | لا | نعم | نعم | منخفض | Needs Review | مراقبة Local الأساسية |
| Grafana | (حدِّد) | grafana.com | AGPL-3.0 | container image | لا | AGPL شروط | لا | نعم | نعم | **مرتفع عند التوزيع** | **Needs Legal Review** | فئة 3/4؛ Observability قابلة للتبديل |
| Loki | (حدِّد) | grafana.com | AGPL-3.0 | container image | لا | AGPL شروط | لا | نعم | نعم | **مرتفع عند التوزيع** | **Needs Legal Review** | كما فوق |
| VictoriaMetrics (بديل) | (حدِّد) | victoriametrics.com | Apache-2.0 | container image | لا | نعم | لا | نعم | نعم | منخفض | Needs Review | بديل مقاييس |
| OpenTelemetry | (حدِّد) | opentelemetry.io | Apache-2.0 | dependency (لاحقاً) | لا | نعم | لا | نعم | نعم | منخفض | Needs Review | tracing مستقبلاً |
| Docker Engine / Compose | تُثبَّت في lockfiles عند تنفيذ Phase 0 | docker.com | Apache-2.0 | dev/ops tool | لا | نعم | لا | نعم | — | منخفض | Needs Review | أساس النشر |
| GitHub Spec Kit (`specify`) | (حدِّد) | github/spec-kit | MIT | dev tool (اختياري) | لا | نعم | لا | نعم | لا | منخفض | Needs Review | النمط مُعتمد؛ الأداة اختيارية |
| Gitea (إن اختير C4) | (حدِّد) | gitea.com | MIT | container image | لا | نعم | لا | نعم | لا | منخفض | Needs Review | استضافة Git داخلية |
| Tesseract / PaddleOCR / docTR | (حدِّد) | — | Apache-2.0 | dependency (P5) | لا | نعم | لا | نعم | نعم | منخفض | Needs Review | محرك OCR العربي يُختار بقياس (فئة 5 + مراجعة عند P5) |
| Apache Tika | (حدِّد) | tika.apache.org | Apache-2.0 | dependency/container (P5) | لا | نعم | لا | نعم | نعم | منخفض | Needs Review | استخراج PDF/Office |
| pdfplumber / pypdf | (حدِّد) | — | MIT / BSD | dependency (P5) | لا | نعم | لا | نعم | لا | منخفض | Needs Review | **الافتراضي** لمعالجة PDF |
| PyMuPDF | (حدِّد) | pymupdf.io | AGPL-3.0 / تجاري | dependency (P5) | لا | AGPL شروط | لا | نعم | نعم | **مرتفع** | **Needs Legal Review** | لا يُستخدم قبل رأي قانوني |
| python-docx / openpyxl | (حدِّد) | — | MIT | dependency (P5) | لا | نعم | لا | نعم | لا | منخفض | Needs Review | Office parsing |
| faster-whisper | (حدِّد) | github | MIT | dependency (P5) | لا | نعم | لا | نعم | لا | منخفض | Needs Review | ASR |
| ffmpeg | (حدِّد — build LGPL-only مفضّل) | ffmpeg.org | LGPL/GPL حسب البناء | dependency/system (P5) | لا | حسب البناء | لا | نعم | نعم | **متوسط–مرتفع** | **Needs Legal Review** | توثيق خيارات البناء إلزامي |
| Model weights — Qwen family (chat/coder/VL) | (حدِّد لكل نموذج) | المصدر الرسمي | حسب النموذج | **model weights** | لا | حسب الرخصة | لا | نعم | غالباً | متفاوت | **Needs Legal Review** | **بوابة مزدوجة:** قبل تشغيله (P5) وقبل تضمينه في bundle (فئة 4) |
| Model weights — Embedding/Reranker (nomic-embed, bge-reranker…) | (حدِّد) | — | حسب النموذج | model weights | لا | حسب الرخصة | لا | نعم | غالباً | متفاوت | **Needs Legal Review** | صف مستقل لكل نموذج |
| Model weights — Whisper / OCR models | (حدِّد) | — | MIT/Apache غالباً | model weights | لا | حسب الرخصة | لا | نعم | — | منخفض–متوسط | Needs Review | يُثبَّت الإصدار قبل التشغيل |

**سياسة المراجع مفتوحة المصدر (Reference-aware — D8/D12/ADR-0021):** قراءة/دراسة كود OSS للتعلم والفهم والمقارنة مسموحة دون قيد. **أي إعادة استخدام مباشرة لكود خارجي** — ملف كامل، **نسخ جوهري** (substantial copying)، أو بنية منسوخة بأسماء متغيّرات مُبدَّلة (بما فيه مخرَج «ذاكرة النموذج» المشابه جوهرياً لكود خارجي معروف) — تتطلب صفاً في هذا السجل وامتثال ترخيص صريحاً، مع **حفظ notices/attribution وعدم إزالتها**. **معايير الحكم (لا حد أسطر ثابتاً كمعيار وحيد):** التشابه الجوهري · التزامات الترخيص · المنشأ (provenance) · إعادة الاستخدام المباشرة مقابل النمط المُتعلَّم. حتى التراخيص المتساهلة (MIT/BSD/Apache) تحمل التزامات إشعار/إسناد. كود AGPL/SSPL/copyleft/commercial لا يدخل إلا بـ Legal Review. أوزان النماذج تُعامل كـ dependencies بهذا السجل. استخدام مرجع لأي مهمة يُذكر في handoff/سجل المراجع.

**قاعدة تشغيل السجل:** الاقتراح → تعبئة الصف → مراجعة (تقنية + قانونية عند اللزوم) → قرار → لا يدخل إلا Approved/Conditional (+attribution في About) → أي ترقية إصدار تعيد الصف إلى المراجعة. **CI (لاحقاً):** فشل عند dependency غير مدرجة.
