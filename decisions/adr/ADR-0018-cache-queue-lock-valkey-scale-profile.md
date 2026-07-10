# ADR-0018 — Cache/Queue/Lock: الآن memory/PostgreSQL · بروفايل التوسع Valkey — مسألة Redis مقفلة

> **ملاحظة زرع وتحديث:** الرقم قائم في السجل الكنسي منذ 2026-07-04 (D4: افتراضي memory/PostgreSQL؛ Valkey optional-ready). يُزرع ملفه هنا **مع إغلاق تكميلي بتفويض SA (2026-07-10 — D9c في حزمة خط الأساس v1.0):** Valkey افتراضيُ بروفايل التوسع، ومسألة Redis **مقفلة نهائياً**، مع توثيق محفزات الانتقال.

**السياق (Context):** المنصة تحتاج كاشاً وطوابير وأقفالاً منذ Phase 0 بشكل خفيف، مع مسار توسع واضح لا يفتح جدل Redis/Valkey في كل مرحلة.

**الوضع السابق (Previous state):** ADR-0012 (تجريد Cache/Queue — مبدأ، Redis|Valkey بالإعداد) ثم ADR-0018 (صف السجل: افتراضي memory/PostgreSQL وValkey optional-ready)؛ Redis بقي يظهر كبديل قائم في بعض الجداول.

**القرار (Decision):**
1. **الآن (Local/Demo/النشر المفرد):** Cache = memory/none · Jobs = طوابير بسيطة على PostgreSQL بنمط **FOR UPDATE SKIP LOCKED** · Locks = **PG advisory locks**.
2. **بروفايل التوسع (scale profile) الافتراضي: Valkey (BSD-3)** للكاش الموزَّع والأقفال والجلسات والطابور.
3. **مسألة Redis مقفلة** — لا يُطرح كخيار في أي تصميم لاحق (ترخيص RSAL/SSPL متغيّر + وجود بديل مكافئ بترخيص آمن).
4. **محفزات الانتقال إلى Valkey (توثيق ملزم):** حجم مهام يقارب **مئات المهام/الثانية** أو الحاجة إلى **دلالات fan-out حقيقية** (بث لمستهلكين متعددين) أو أقفال/جلسات موزَّعة عبر أكثر من عقدة — عندها يُفعَّل Valkey بالإعداد بعد بوابة الفئة 3.

**البدائل (Alternatives):** Redis (مرفوض نهائياً — ترخيص متقلب وقيمة مطابقة لـ Valkey) · RabbitMQ/Kafka (مرفوضان الآن — أثقل من الحاجة؛ أي حاجة مستقبلية لبث أحداث مؤسسي = ADR جديد) · Valkey من اليوم الأول (مرفوض — حاوية إضافية بلا حاجة فعلية في P0/P1).

**السبب (Rationale):** PostgreSQL يغطي احتياج البداية بمكوّن واحد موثوق (أقل صور، أقل بوابات ترخيص)؛ وValkey يعطي مسار توسع بترخيص BSD آمن ومتوافق مع عقود Redis البرمجية.

**العواقب (Consequences):** عقود CacheProvider/QueueProvider/LockProvider في backend/shared منذ Phase 0 بتنفيذ memory/PG؛ Provider Equivalence tests (memory/PG ↔ Valkey) شرط اعتماد التنفيذ الثاني؛ مفاتيح الإعداد كما في coding-standards §3.

**خطة الانتقال (Migration plan):** عند بلوغ محفز: صف ترخيص Valkey (فئة 3) → تفعيل الصورة المعرّفة المطفأة → تبديل backends بالإعداد → اختبارات التكافؤ خضراء — دون تغيير كود أعمال.

**الحالة (Status):** Accepted
**التاريخ (Date):** 2026-07-10 (الأصل: D4 بتاريخ 2026-07-04؛ الإغلاق التكميلي D9c بتاريخ 2026-07-10)
**الوثائق المرتبطة (Related documents):** ../open-decisions.md (صف Redis vs Valkey C1) · ../license-review.md (صفا Valkey/Redis) · ../../methodology/coding-standards.md (§3) · ../../methodology/testing-strategy.md (Provider Equivalence) · ADR-0012 (السجل الكنسي) · ../../phases/phase-0-foundation-full-stack-skeleton.md (FR-0.4/FR-0.13)
