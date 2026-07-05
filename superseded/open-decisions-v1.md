> ⚠️ SUPERSEDED — لا يُستخدم للتنفيذ. المرجع الحالي: حزمة v2.0 (انظر superseded/README.md). تاريخ الوسم: 2026-07-03.

# تصنيف القرارات المفتوحة — Open Decisions Classification
## ملحق رسمي يعدّل قسم Open Decisions في الوثيقتين المعتمدتين
> **القاعدة المعتمدة (بملاحظتك):** القرار المفتوح لا يوقف التصميم إلا إذا كان في **الفئة 1**. قرارات التراخيص تبقى **Needs License Review** ولا تمنع تصميم المرحلة الأولى، لكن **لا يدخل أي dependency فعلياً في التنفيذ قبل مراجعة ترخيصه** (License Review Workflow — قسم 15 من المنهجية).
> **حالة ADR-0001 (Spec-driven + Modular Monolith First): Accepted.**

---

## الفئة 1 — Blockers قبل التصميم (Design Blockers)
| البند | الحالة |
|---|---|
| — لا يوجد — | ✅ لا شيء يمنع تصميم المرحلة الأولى أو المراحل التالية. ADR-0001 معتمد، والمرجعان (Catalog + Methodology) معتمدان مبدئياً. |

*(بند تأكيدي غير مُعطِّل: تأكيد أن «المرحلة الأولى» = Phase 0 في ترقيم الـ Roadmap — انظر Clarify في حزمة التصميم. لا يوقف شيئاً لأن Phase 0 مطلوبة أولاً بأي تفسير.)*

## الفئة 2 — Blockers قبل التنفيذ (Implementation Blockers)
> تُحسم قبل كتابة أول كود للمرحلة المعنية — عبر License Review وقرارات معايير.

| البند | نطاق الحسم | ملاحظات |
|---|---|---|
| License Review لستاك الكود الأساسي (FastAPI، Next.js/React/TS، Tailwind/shadcn، Alembic، مكتبات Python/Node الأساسية) | قبل تنفيذ Phase 0 | تراخيص متساهلة متوقعة (MIT/BSD/Apache) لكن القاعدة تلزم صفاً في `license-review.md` لكل dependency قبل دخوله. |
| مضيف Git الداخلي (bare git محلي / Gitea / بديل) + سياسة الفروع | قبل أول commit | بيئة مغلقة تحتاج استضافة كود داخلية. |
| معايير الأدوات: نسخة Python + مدير حزم (uv/poetry)، نسخة Node LTS + (pnpm/npm) | قبل تنفيذ Phase 0 | قرار معايير يُوثَّق في `coding-standards.md`. |
| لكل مرحلة لاحقة: مراجعة تراخيص dependencies تلك المرحلة قبل تنفيذها (مثال: محرك OCR، بديل PyMuPDF، ffmpeg → قبل تنفيذ media في مرحلتها) | قبل تنفيذ المرحلة المعنية | لا يؤثر على Phase 0. |

## الفئة 3 — Blockers قبل Docker Compose (سحب/تشغيل الصور)
> تُحسم قبل مهمة بناء الـ Compose في Phase 0 (الحزمة P0.4) — لأن سحب الصورة = دخول dependency فعلياً.

| البند | الخيارات | ملاحظات |
|---|---|---|
| مزوّد cache/queue الافتراضي | **Redis** (ترخيص متغيّر RSAL/SSPL) أم **Valkey** (BSD) | الطبقة مجرّدة بالإعداد في الحالتين (ADR-0012)؛ المطلوب اختيار الصورة الافتراضية + مراجعة ترخيص الإصدار. |
| Object storage للـ demo | **MinIO** (AGPL — مقبول داخلياً غالباً) أم بديل S3-compatible (SeaweedFS…) | مجرّدة بالإعداد (ADR-0013)؛ القرار للصورة الافتراضية + مراجعة الإصدار. |
| مراقبة Local Demo | Prometheus + سجلات JSON فقط، أم Grafana/Loki كاملة (AGPL) | Observability قابلة للتبديل (ADR-0014)؛ يمكن البدء بالأبسط وإضافة Grafana/Loki لاحقاً بعد المراجعة دون تغيير كود. |
| مراجعة شكلية لصور: PostgreSQL، Qdrant، OpenSearch | — | تراخيص متساهلة متوقعة؛ تمرّ بنفس سير المراجعة. |
| Neo4j | **ليس blocker** | off by default ولا يدخل compose Local؛ حسمه ضمن الفئة 5. |

## الفئة 4 — Blockers قبل التوزيع النهائي (Distribution/Release Blockers)
| البند | ملاحظات |
|---|---|
| الموقف القانوني النهائي من AGPL عند توزيع الحزمة خارج فريقك (MinIO/Grafana/Loki إن اعتُمدت) | استخدام داخلي ≠ توزيع؛ يلزم رأي قانوني قبل أي release خارجي. |
| تراخيص أوزان النماذج (Qwen/Whisper/embedders/rerankers/OCR models) وشروط تضمينها في offline bundle | تُراجع لكل نموذج قبل تضمينه في حزمة النقل. |
| سياسة توقيع/تحقق حزمة النقل المغلق + نهج TLS/PKI للإنتاج | تشغيلية/أمنية قبل أول نشر إنتاجي. |
| اكتمال صفحة About/Attribution لكل مكوّن مفتوح | شرط إغلاق قبل التوزيع. |

## الفئة 5 — قرارات تبقى Configurable (لا توقف شيئاً)
| البند | آلية البقاء مفتوحاً |
|---|---|
| محرك OCR (Tesseract/PaddleOCR/docTR) | Capability في Model/Provider Registry — يُبدَّل من الأدمن. |
| نطاق Graph (off / Apache AGE / Neo4j) | Feature flag + Graph-enabled bundle. |
| النماذج الفعلية لكل capability + سياسة تشغيل الثقيل حسب العتاد | Registry + Hardware-aware selection. |
| مستوى المراقبة في dev بعد الحسم المبدئي | config. |
| مزوّد cache/queue وobject storage **بعد** حسم الافتراضي | abstraction تسمح بالتبديل بالإعداد. |
| بنية Postgres (instance واحد بأربع قواعد في Local ↔ فصل instances في الإنتاج) | Database Router + endpoints بالإعداد. |
| الـ IdP، مصفوفات الاعتماد/SoD، جرد الأنظمة الداخلية، الأحجام/التزامن/عتاد الإنتاج | إعدادات وسياسات تُحسم في مراحلها كقياسات/config. |

---

**قاعدة إدارة:** كل بند فئة 2/3 يُحسم داخل نافذة تنفيذ مرحلته عبر License Review Workflow (Approved/Conditional/Rejected/Needs Legal Review)؛ بنود الفئة 4 تُحسم قبل أول release/توزيع؛ بنود الفئة 5 تبقى مفاتيح إعداد موثّقة في `configuration.md`.
