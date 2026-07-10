# ADR-0019 — تخزين الكائنات: filesystem محلياً · SeaweedFS افتراضي الإنتاج · MinIO مشروط

> **ملاحظة زرع وتحديث:** الرقم قائم في السجل الكنسي منذ 2026-07-04 (D5: افتراضي filesystem وحسم المزوّد بمرحلة الملفات). يُزرع ملفه هنا **مع إغلاق تكميلي بتفويض SA (2026-07-10 — D8 في حزمة خط الأساس v1.0):** حسم افتراضي الإنتاج الموزَّع = SeaweedFS.

**السياق (Context):** الملفات والوسائط تحتاج تخزين كائنات قابلاً للنقل بين جهاز التطوير والشبكة المغلقة، مع بوابة تراخيص صارمة (constitution م7) وحساسية خاصة لتراخيص AGPL عند التوزيع.

**الوضع السابق (Previous state):** ADR-0013 (تجريد Object Storage — مبدأ) وADR-0019 (صف السجل: filesystem افتراضاً والمزوّد يُحسم بمرحلة الملفات)؛ license-review يحمل MinIO بوصفه Needs Legal Review وSeaweedFS بوصفه «بديل».

**القرار (Decision):**
1. **المحلي/التجريبي (Local/Demo):** filesystem عبر **ObjectStorageProvider** (fs|s3) — كما هو.
2. **افتراضي الإنتاج عند الحاجة لتخزين كائنات موزَّع: SeaweedFS (Apache-2.0)**.
3. **MinIO يبقى adapter اختيارياً فقط** — لا يُستخدم إلا إذا اجتاز License Review القانوني (AGPLv3).
4. أي مزوّد S3-compatible آخر يمر عبر نفس التجريد وبوابة الترخيص.
5. **كود الأعمال لا يسمّي مزوّداً أبداً** — الأسماء داخل تنفيذ الـ Provider في backend/shared حصراً.

**البدائل (Alternatives):** MinIO افتراضاً (مرفوض كافتراضي — AGPLv3 يفرض مراجعة قانونية لكل سيناريو توزيع) · S3 سحابي (غير قابل — شبكة مغلقة) · filesystem في الإنتاج الموزَّع (مرفوض — لا يفي بالتوسع/التوافر عند تعدد العقد؛ يبقى صالحاً للنشر المفرد).

**السبب (Rationale):** SeaweedFS يوفر S3-compatibility بترخيص Apache-2.0 الآمن توزيعياً، فيزيل بوابة قانونية كاملة من مسار الإنتاج؛ والتجريد يحفظ حرية التبديل بلا كلفة كود.

**العواقب (Consequences):** صف SeaweedFS في license-review يصبح المفضل/الافتراضي الإنتاجي؛ صف MinIO يبقى Needs Legal Review كخيار مشروط؛ بوابة الفئة 3 تنطبق عند تفعيل أي صورة تخزين؛ Provider Equivalence tests (fs ↔ s3) قبل اعتماد التنفيذ الثاني.

**خطة الانتقال (Migration plan):** التفعيل بمرحلة الملفات (P5): تعريف الصورة موجود مطفأً من Phase 0؛ التفعيل = صف ترخيص + إعداد + اختبارات تكافؤ — دون تغيير كود أعمال.

**الحالة (Status):** Accepted
**التاريخ (Date):** 2026-07-10 (الأصل: D5 بتاريخ 2026-07-04؛ الإغلاق التكميلي D8-baseline بتاريخ 2026-07-10)
**الوثائق المرتبطة (Related documents):** ../open-decisions.md (صف Object Storage C2) · ../license-review.md (صفوف SeaweedFS/MinIO) · ../../methodology/coding-standards.md (§2/§3) · ../../methodology/testing-strategy.md (Provider Equivalence) · ADR-0013 (السجل الكنسي) · ../../phases/phase-0-foundation-full-stack-skeleton.md (FR-0.4/FR-0.9)
