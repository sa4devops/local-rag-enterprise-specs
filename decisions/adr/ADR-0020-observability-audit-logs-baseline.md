# ADR-0020 — خط الأساس الرقابي: تدقيق PG محصَّن · سجلات JSON مهيكلة · عارض عبر LogRepository

> **ملاحظة زرع وتحديث:** الرقم قائم في السجل الكنسي منذ 2026-07-04 (D6 — Observability Baseline). يُزرع ملفه هنا ضمن إغلاق خط الأساس v1.0 **مع تفصيل تكميلي (D11):** مستخدم قاعدة التدقيق المخصص، ومصدر عارض السجلات، وموقف hash chaining.

**السياق (Context):** enterprise-auditability مطلوبة من اليوم الأول دون وزن مراقبة مبكر (Grafana/Loki)؛ ويلزم فصل صارم بين تدقيق الأعمال والتشخيص التقني، وضمانة تقنية ضد تعديل سجل التدقيق.

**الوضع السابق (Previous state):** ADR-0014 (طبقة Observability قابلة للتبديل — مبدأ) وADR-0020 (صف السجل: Audit-PG + JSON logs + Health + Error Catalog + IDs + /metrics اختياري)؛ FR-0.19 وcoding-standards §10 يفصّلان الحقول — دون نص على مستخدم التدقيق المخصص ولا مصدر العارض ولا موقف hash chaining.

**القرار (Decision):**
1. **التدقيق:** جداول PostgreSQL **append-only** بـ**مستخدم قاعدة بيانات مخصص**؛ دور التطبيق **لا يملك UPDATE/DELETE على جداول التدقيق** (INSERT فقط). العمليات الحساسة تسجّل: actor · action · entity · timestamp · request_id · result · before/after-metadata حيث يُسمح.
2. **hash chaining ليس الآن** — يُضاف فقط إذا فُرض مطلب امتثال tamper-evident صريح (يبقى موطؤه قابلاً للإضافة).
3. **سجلات التطبيق:** JSON مهيكلة إلى **stdout/stderr** (يدوّرها Docker) بحقول: request_id · correlation_id · module · endpoint · error_code · stack · duration · actor حيث ينطبق — **خارج PostgreSQL**.
4. **عارض السجلات الإداري لا يقرأ ملفات السجلات أبداً** — مصدره **LogRepository / مخزن أحداث تشغيلية مُهيكل** (تنفيذ v1: جدول **ops_events** صغير في PG)؛ الـ stack الكامل للمشغّلين المخوّلين فقط.
5. **المراقبة الآن:** health + **readiness/liveness** + `/metrics` اختياري بعلَم + **OpenTelemetry-ready** — **لا Grafana/Loki/Graylog/Elastic ابتداءً** (التوسعة P8 بمراجعة ترخيص).

**البدائل (Alternatives):** Grafana+Loki من البداية (مرفوض — وزن تشغيلي وبوابة AGPL قبل الحاجة) · التدقيق في محرك السجلات (مرفوض — التدقيق سجل أعمال قانوني في مصدر الحقيقة لا سجل تشخيص) · hash chaining الآن (مرفوض — كلفة بلا مطلب امتثال قائم) · قراءة العارض من الملفات (مرفوضة — هشّة وتكسر القناع والصلاحيات).

**السبب (Rationale):** الفصل تدقيق/تشخيص يحفظ لكلٍّ دلالته وصلاحياته؛ وقيد INSERT-only ضمانة بنيوية لا سياسية؛ وops_events يعطي عارضاً محكوم الصلاحية دون بنية سجلات مركزية.

**العواقب (Consequences):** baseline migrations تُنشئ مستخدم التدقيق وقيود المنح (Phase 0 — إضافات v1.0)؛ اختبار Logging/Error Contract في CI (لا أسرار، error_code+request_id لكل خطأ)؛ Error Code Catalog يتحدث مع كل feature.

**خطة الانتقال (Migration plan):** عند التوسعة (P8): OTel adapter ثم أي مكدس مراقبة بعد بوابة ترخيص — دون تغيير عقود التسجيل.

**الحالة (Status):** Accepted
**التاريخ (Date):** 2026-07-10 (الأصل: D6 بتاريخ 2026-07-04؛ التفصيل التكميلي D11 بتاريخ 2026-07-10)
**الوثائق المرتبطة (Related documents):** ../../methodology/coding-standards.md (§10) · ../../methodology/testing-strategy.md (Audit · Logging/Error Contract) · ../../phases/phase-0-foundation-full-stack-skeleton.md (FR-0.14/FR-0.19 + إضافات v1.0 بنود 2–4) · ADR-0014 (السجل الكنسي) · ../../constitution.md (م3)
