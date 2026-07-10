# testing-strategy.md — استراتيجية الاختبار

> **Version:** 1.1 (+Provider-Equivalence وLogging-Contract) · **Status:** Current / Accepted · **Date:** 2026-07-04
> **Authority:** النسخة المرجعية الموسّعة لـ Methodology §10؛ عند التعارض داخل مستواها تحكم هذه الوثيقة.
> **مبادئ حاكمة:** default-deny يُختبر لا يُفترض · **deny test لكل endpoint** · **Validation لا تفشل مفتوحة (fail-closed)** · لا نداء خارجي (مُختبر آلياً) · الحدود تُختبر في CI · كل feature بلا اختبار = غير مكتمل (Quality Gates).

| النوع | الهدف | أين يُطبَّق | مثال Acceptance Criteria | مطلوب من |
|---|---|---|---|---|
| Unit | صحة منطق module داخلياً | داخل كل module (`tests/`) | دالة قرار الصلاحية تُرجع deny افتراضاً عند غياب سياسة | Phase 0 |
| Integration | تفاعل modules عبر واجهاتها فقط | `tests/integration` | screen→migration→approve→apply يعمل وكل خطوة تولّد audit | Phase 1 |
| E2E | مسار مستخدم كامل عبر UI | `tests/e2e` | دخول admin → إنشاء شاشة → CRUD على الكيان المولّد | Phase 1 |
| Permission | إنفاذ الصلاحية | `tests/permission` | لكل endpoint: **deny test** + التحقق من RLS (صف غير مملوك لا يظهر) وFLS (حقل محجوب لا يعود) | Phase 1 |
| Audit | تسجيل الأحداث | مع كل feature | كل حدث في كتالوج الأحداث يُنشأ بحقوله الإلزامية (actor/target/old/new/ts) | Phase 0 (أحداث الإعداد) ثم شامل من Phase 1 |
| Migration | سلامة الترحيل والتراجع | `tests/migration` | apply ثم rollback بلا فقد؛ ورفض تطبيق migration غير معتمد في خط التوليد المحكوم | Phase 0 (baseline) / Phase 1 (المحكوم) |
| Configuration Profile | صحة البروفايلات والحِزم | `tests/` | ملفات local/demo/staging/production + bundles تجتاز الـ validation؛ مفتاح حرج ناقص ⇒ fail-fast برسالة تذكر المفتاح | Phase 0 |
| Feature Flag | تفعيل/تعطيل القدرات | `tests/` | تعطيل قدرة يخفيها دون كسر خدمة؛ **الأعلام المحميّة ترفض التعطيل**؛ الحدث يُسجَّل | Phase 0 |
| Boundary (CI) | منع كسر الحدود | CI | استيراد صاعد/دوري/عابر مُتعمَّد ⇒ فشل CI | Phase 0 |
| Offline / No-external-call | لا اتصال خارجي وقت التشغيل | `tests/offline` + CI | إدخال نداء خارجي تجريبي ⇒ فشل الاختبار | Phase 0 |
| Smoke / Health | الإقلاع والصحة | CI + بيئة التشغيل | compose up كامل ⇒ `/health` أخضر لكل التبعيات؛ إسقاط خدمة ⇒ تحديد المتعطل + service.health_alert | Phase 0 |
| RAG | استرجاع محكوم الصلاحية | `tests/` | مستند خارج صلاحية المستخدم لا تظهر مقاطعه إطلاقاً؛ كل إجابة تحمل provenance؛ نقص أدلة ⇒ No-Guessing | Phase 5 |
| SQL-Agent Safety | أمان الاستعلام | `tests/security` | رفض DDL/DML/جداول خارج allow-list/تجاوز RLS؛ الاستعلام المنفّذ يُسجَّل | Phase 6 |
| Media Pipeline | معالجة الوسائط | `tests/` | PDF/صورة/صوت ⇒ معالجة+فهرسة+ربط بالمصدر+audit؛ فشل نموذج ⇒ fallback المعرّف (فيديو ⇒ صوت+keyframes) | Phase 5 |
| Cache Invalidation | منع التسريب عبر الكاش | `tests/` | تغيّر نسخة مستند/سكيم/**نطاق صلاحية** ⇒ إبطال المفتاح؛ العمليات الحرجة تعيد التحقق live | Phase 5 |
| Connector | سلامة التكامل | `tests/` | الاستدعاء ضمن صلاحية الحساب المربوط؛ إجراء يغيّر حالة ⇒ بوابة human-in-the-loop | Phase 7 |
| Backup/Restore | التعافي | `tests/` + تمرين تشغيلي | نسخ ثم استعادة متحقَّقة من bundle موقّعة | Phase 8 |
| RTL/i18n | سلامة العربية | snapshot/بصري | تبديل ar/en يقلب الاتجاه صحيحاً في الشاشات المعنية | Phase 0 (القشرة) ثم مستمر |
| Reproducibility | إعادة البناء مغلقاً | CI | lockfiles محدّثة؛ الصور بـ digest pinning؛ بناء من الحزمة الـ offline ينجح (لاحقاً) | Phase 0 (السياسة) / Phase 8 (التمرين الكامل) |
| Provider Equivalence | تكافؤ تنفيذات العقود (memory/Postgres ↔ Valkey؛ fs ↔ S3) | tests | نفس حزمة حالات القبول تجتاز على التنفيذين قبل اعتماد الثاني | عند إدخال أي تنفيذ ثانٍ |
| Logging/Error Contract | التزام JSON schema + Error Code Catalog + correlation IDs | tests + CI | كل خطأ يحمل error_code + request_id؛ لا أسرار في السجلات (فحص قناع) | Phase 0 |

**قاعدة إدارة:** يوسَّع هذا الجدول عند تصميم كل مرحلة بحالات القبول التفصيلية لمهامها؛ ولا يُدمج أي feature قبل اجتياز الأنواع المنطبقة عليه (Quality Gates — Methodology §11).
**قاعدة الاستخراج (v1.0-baseline):** اختبارات العقود (contract tests) **شرط مسبق إلزامي** لأي استخراج module إلى خدمة مستقلة — انظر ADR سياسة الحدود والاستخراج.
