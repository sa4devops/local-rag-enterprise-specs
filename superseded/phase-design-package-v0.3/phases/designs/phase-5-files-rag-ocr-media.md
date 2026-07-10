# Phase 5 — Knowledge Foundation: Files, RAG, OCR &amp; Media Pipeline

> **Version:** 1.0 — Proposed (Accepted باعتماد v0.3) · **Date:** 2026-07-06 · **Authority عند الاعتماد:** المرتبة 6
> **Inherits:** Common Phase Baseline — PHASE_MASTER_PLAN §4. **Predecessor:** Phase 4 بكامل DoD. بطاقات المهام عند التفعيل.
> **بوابات دخول إلزامية (فئة 2/3):** صفوف تراخيص: محرك OCR المختار · PDF tooling (الافتراضي pdfplumber/pypdf/Tika؛ PyMuPDF=Legal) · ffmpeg (بناء LGPL موثَّق) · **أوزان كل نموذج قبل تشغيله (بوابة 1)** · مزوّد Object Storage **فقط عند تفعيل حاوية** (وإلا يبقى fs).

## 1. Purpose
تفعيل الطبقة المعرفية: ملفات محكومة، معالجة مستندات/OCR ووسائط (صوت/صورة/فيديو-keyframes)، فهرسة **هجينة** (Qdrant+OpenSearch) مرشّحة بالصلاحية، واسترجاع بـ provenance وNo-Guessing — مع Model/Provider Registry UI و**الحد الأدنى من LLM Gateway** (توجيه embedding/rerank/ASR/OCR/vision-caption فقط، لا chat).

## 2. Scope
File Service: رفع/تنزيل/نسخ عبر **ObjectStorageProvider (fs افتراضاً)** + ميتاداتا (نوع/مالك/وحدة/تصنيف موروث من السياق) + ربط attachment fields من P2 · Ingestion pipeline (workers): extract → normalize → chunk (defaults قابلة للضبط) → embed (EmbeddingProvider) → index مزدوج (Qdrant vectors + OpenSearch BM25) مع **وسم كل chunk بنطاق الصلاحية/التصنيف والمصدر والنسخة** · OCR للصور وPDF الممسوح (OCRProvider) · Docs parsing (PDF نصّي/Office) · Media: صوت→ASR (SpeechProvider عبر faster-whisper المرشّح) · صورة→OCR+وصف (VisionProvider خفيف) · فيديو→**استخراج الصوت + keyframes** (MediaProcessingProvider/ffmpeg) — فهم الفيديو الكامل Backlog · **RAG Retrieval API**: hybrid + RerankerProvider + **ترشيح الصلاحية قبل الإرجاع** + provenance إلزامي + **No-Guessing** (نقص أدلة ⇒ رفض صريح) · **RAG-over-media** (نتائج الوسائط بنفس الفهرس المحكوم) · OKF: حِزم معرفة محلية (md+yaml) كمساعد سياق **ليست مصدر حقيقة** · **Model/Provider Registry UI**: capability→model/provider، تفعيل/تعطيل، fallback، **بلا كشف endpoints/secrets (D9)** · Gateway-min: المسار الوحيد لهذه القدرات · إبطال كاش بالمفاتيح (doc-version/index-version/schema/permission-scope) + إعادة تحقق live قبل الأفعال الرسمية.

## 3. Out of Scope
Chat/تقارير/SQL-Agent/Reasoning (P6) · فهم فيديو كامل (Backlog) · نماذج ثقيلة فوق العتاد (تبقى قابلة للتوصيل بالإعداد) · تكاملات (P7) · تفعيل MinIO/SeaweedFS ما لم تُفتح بوابته.

## 4. Required Inputs
P4 DoD · هذا التصميم Accepted · بوابات الترخيص أعلاه مقفلة لكل عنصر يُشغَّل فعلاً · نماذج خفيفة معتمدة في license-review (embedding/rerank/ASR/OCR).

## 5. Expected Outputs
رفع مستند/صوت/صورة → معالجة وفهرسة محكومة → استرجاع هجين مرشّح بالصلاحية مع مصدر واستشهاد، وتبديل نموذج أي capability من الواجهة دون كود.

## 6. Functional Requirements
| # | المتطلب |
|---|---|
| FR-5.1 | File Service كامل عبر ObjectStorageProvider(fs) بميتاداتا وتصنيف وصلاحيات موروثة، وربط حقول attachment. |
| FR-5.2 | Pipeline ingestion غير متزامن (QueueProvider/Postgres) بحالات قابلة للتتبع وإعادة محاولة، وكل خطوة audit. |
| FR-5.3 | Chunking معلن الإعداد (حجم/تداخل/حدود) — defaults في config (OD-P5-1). |
| FR-5.4 | فهرسة مزدوجة: Qdrant (متجهات) + OpenSearch (نصي) بوسوم المصدر/النسخة/التصنيف/نطاق الوصول لكل chunk. |
| FR-5.5 | Retrieval API: hybrid merge + rerank + **فلترة الصلاحية على مستوى الاستعلام** (لا post-filter فقط) + إرجاع provenance (doc/page/segment). |
| FR-5.6 | No-Guessing: عتبة كفاية أدلة معلنة؛ دونها استجابة رفض مسنودة بالسبب. |
| FR-5.7 | OCR/Docs: PDF نصّي مباشر؛ الممسوح عبر OCRProvider؛ Office عبر أدوات معتمدة الصفوف. |
| FR-5.8 | Media: ASR للصوت؛ صورة=OCR+وصف؛ فيديو=صوت+keyframes تُعالَج كصور — النتائج في نفس الفهرس المحكوم. |
| FR-5.9 | Registry UI: ربط كل capability (embedding/rerank/asr/ocr/vision-caption) بمزوّد/نموذج + fallback + تعطيل، بتدقيق واعتماد حسب سياسة الإنتاج. |
| FR-5.10 | Gateway-min: كل استدعاءات القدرات أعلاه تمر به حصراً (منع أي SDK مباشر خارج Providers). |
| FR-5.11 | إبطال الكاش وإعادة الفهرسة عند نسخة جديدة للمستند أو تغيّر سياسة تمسّه (حذف/تحديث chunks المتأثرة). |
| FR-5.12 | OKF: تحميل حزم محلية وعرضها كمساعد سياق موسوم، دون اعتبارها مصدر حقيقة. |

## 7. NFRs (الخاصة)
حدود demo للموارد (heap/mem كما في P0) · زمن استرجاع baseline يُقاس · pipeline يتحمل فشل نموذج بـ fallback معلن (فيديو⇒صوت+إطارات دائماً).

## 8. User Stories
بصفتي موظفاً: أرفع PDF ممسوحاً فيصبح قابلاً للبحث ضمن صلاحيتي فقط · أبحث فأحصل على مقاطع بمصدرها وصفحتها · أسأل عمّا لا تغطيه المستندات فيرفض النظام صراحة بدل التخمين · أرفع تسجيلاً صوتياً فيُفهرس نصّه.

## 9. Admin Stories
بصفتي أدمن: أبدّل نموذج الـ embedding من الواجهة فيسري على الفهرسة الجديدة بخطة إعادة فهرسة واضحة · أعطّل OCR مؤقتاً فتتوقف مساراته بلطف · أرى حالة كل ملف في الـ pipeline وأعيد معالجة الفاشل · أراقب أن نتائج مستخدمٍ ما لا تتجاوز نطاقه (عبر المحاكاة من P4).

## 10. Main Modules + Epics
**Modules:** files · media · rag · search · okf · model-registry · provider-registry · llm-gateway(جزئي) (+workers).
**Epics:** E5.1 File Service → E5.2 Ingestion Pipeline+Queue → E5.3 Chunk/Embed/Dual-Index → E5.4 Retrieval+Rerank+PermFilter → E5.5 OCR/Docs → E5.6 Media(ASR/Image/Video-fallback) → E5.7 Registry UI+Gateway-min → E5.8 No-Guessing+Provenance → E5.9 Cache/Invalidation+Reindex → E5.10 OKF → E5.11 Hardening/Docs/Handoff.

## 11. Data Model Notes
files(+versions, classification, owner_scope) · ingestion_jobs(+steps,status,error_code) · chunks_meta (المرجع في PG؛ المتجهات في Qdrant والنص في OpenSearch) · capability_bindings (capability→provider/model+fallback) · okf_bundles — platform/apps حسب الملكية؛ لا تخزين ثنائي في PG.

## 12. API Notes
/files/* · /ingestion/* (status/retry) · /rag/query (hybrid+cite) · /capabilities/* (registry) · /okf/* — خلف الـ Gate؛ /rag/query يتطلب سياق مستخدم كاملاً ويرفض الاستدعاء المجهول.

## 13. UI Notes
File manager بموروث التصنيف · Ingestion monitor · **Model/Provider Registry screens** (بلا endpoints/secrets) · Search/Retrieval tester للأدمن (يعرض provenance والقرار) · OKF viewer — RTL كاملة.

## 14. Security &amp; Permissions
الصلاحية **قبل** الاسترجاع (فلترة استعلامية بالوسوم + تحقق نهائي) · وراثة تصنيف الملف لمشتقاته (نص/chunks/إطارات) بقاعدة الأشد · Registry UI ضمن حدود D9 · لا استدعاء نموذج خارج Gateway-min (فحص CI).

## 15. Audit &amp; Logging
file.uploaded/version_added/deleted · ingestion.step_completed/failed/retried · index.updated/invalidated · rag.queried (مستخدم/نطاق/عدد النتائج/قرار الكفاية) · capability.binding_changed(+approval) · okf.bundle_loaded — مع request/correlation IDs عبر الـ pipeline.

## 16. Configuration / Environment Impact
STORAGE_BACKEND=fs (كما هو؛ تفعيل s3 ببوابة) · CHUNK_* defaults · RAG_TOPK/RERANK_* · EVIDENCE_THRESHOLD · MEDIA_* (تمكين لكل نوع) · نماذج القدرات تُدار من Registry (dynamic) لا env.

## 17. Provider Abstractions Impact
تفعيل فعلي: ObjectStorage(fs) · Embedding · Reranker · OCR · Vision(خفيف) · MediaProcessing(ffmpeg) · LLMProvider عبر Gateway-min · Queue(Postgres) للـ pipeline — SDKs داخل التنفيذات حصراً؛ **Provider-Equivalence tests** عند أي تنفيذ ثانٍ (fs↔s3).

## 18. Database / Migration Notes
Baseline migrations لجداول files/jobs/bindings · لا DDL على فهارس Qdrant/OpenSearch إلا عبر وحدة search بإجراء معلن ومدقَّق (index schema versioned) · إعادة الفهرسة عملية معلنة قابلة للاستئناف.

## 19. Testing Strategy (إضافات)
**تسريب-صفر:** مستند خارج الصلاحية لا يظهر أي chunk منه (اختبار سلبي إلزامي على المسارين vector/text) · provenance موجود بكل نتيجة · No-Guessing يرفض تحت العتبة · إبطال الكاش عند نسخة/سياسة (اختبار constitution م16) · فشل نموذج ⇒ fallback (فيديو⇒صوت+إطارات) · وراثة التصنيف للمشتقات · offline: كل الاستدعاءات محلية.

## 20. Acceptance Criteria
1) رفع→معالجة→فهرسة→استرجاع لمستند وصورة وصوت وفيديو(بالمسار الاحتياطي) يعمل بكامله. 2) إثبات اختباري لعدم تسريب أي محتوى خارج الصلاحية. 3) كل إجابة استرجاع تحمل مصدراً؛ ودون كفاية أدلة يرفض النظام صراحة. 4) تبديل نموذج capability من الواجهة يعمل بتدقيق (وباعتماد في وضع الإنتاج). 5) إعادة فهرسة عند نسخة جديدة تُبطل القديم. 6) لا SDK نموذج خارج Providers/Gateway (فحص CI أخضر). 7) بوابات التراخيص مقفلة لكل مكوّن مُشغَّل. 8) RTL سليم لشاشات المرحلة.

## 21. Risks
جودة العربية (OCR/ASR) — تخفيف: قياس مقارن قبل تثبيت الافتراضي (OD/فئة5) · حمل العتاد — نماذج خفيفة + حدود demo · تسريب عبر الكاش — مفاتيح النطاق + اختبار إلزامي · زحف نحو chat مبكراً — مقفول نطاقاً.

## 22. Open Decisions
| OD | الموضوع | التوصية | البوابة |
|---|---|---|---|
| OD-P5-1 | قيم chunking الافتراضية | حجم/تداخل معتدلان token-based موثّقان في config مع مبرر | Clarify التفعيل |
| OD-P5-2 | تفعيل حاوية تخزين (MinIO/SeaweedFS) | البقاء على fs في Local؛ التفعيل عند حاجة حجم/تعدد عقد ببوابة فئة 3 (SeaweedFS مرشّح ترخيصياً) | عند طلب التفعيل |
| OD-P5-3 | النموذج الافتراضي لكل capability | صف license-review + قياس عربي لكل مرشح قبل التثبيت في Registry | قبل تشغيل كل نموذج |

## 23. Definition of Done
Baseline المشترك + AC 1–8 خضراء + توثيق Registry/Pipeline + خطة إعادة فهرسة موثّقة + handoff بقائمة "لا يُلمس" (عقود Gateway-min وفلترة الاسترجاع) لوكيل P6.

## 24. Coding Agent Prompt
> القالب الموحّد §6 مع: **PHASE=5 · DESIGN=phases/designs/phase-5-files-rag-ocr-media.md · RELEASE=v0.3-phase-design-package** — لا تشغيل لأي نموذج/أداة قبل صف ترخيصه؛ التزم بأقسام 3/14/19/22.
