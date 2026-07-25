# SEMANTIC-MERGE-MAP — B1 (المرحلة 4: الدمج الدلالي العالمي)

> **مخرج traceability/تحليلي غير حاكم** — لا سلطة موازية ولا بديل عن الأصل الحاكم. الدمج **عبر الوثائق السبع كلها مرة واحدة** (P3 B1 §10) لإنتاج canonical universe ثابت. **قاعدة السكن:** الممثل تحت **أدنى رقم RAR** بين مصادر المجموعة. الدمج **فقط** عند تطابق: الالتزام الدلالي · النطاق · actor/component · الأثر · بلا qualifiers متعارضة · وصفٌ واحد يحفظ كل المصادر.

## مجموعات الدمج المعتمدة (اختبار تكافؤ دلالي مُثبت)
| MERGE-ID | atomic sources (RAR:line) | الالتزام الموحّد | الممثل يسكن | سبب الدمج + qualifiers محفوظة |
|---|---|---|---|---|
| **MERGE-G01** | RAR001-S14-014 (:299) ⊕ RAR002-S14-008 (:414) | منع Prompt Injection من محتوى غير موثوق (مستند/سجل/معرفة) | **RAR-001** (أدنى) | نفس الالتزام والأثر (سلامة المدخل)؛ المصدران محفوظان؛ لا qualifier متعارض |
| **MERGE-G02** | RAR002-S11-001..008 (:331–:338) | تدفق «طلب إنشاء Agent → مراجعة أدمن → قبول/تعديل/رفض → Draft مملوك» كالتزام حوكمي واحد | **RAR-002** | ثمان خطوات لتدفق واحد ذي قرار تغطية واحد (هل يوجد request/approval workflow محكوم؟)؛ الخطوات محفوظة تفصيلاً كسمة للصف |
| **MERGE-G03** | RAR001-S12-018 (:258) ⊕ RAR001-S14-013 (:298) | سلوك Fallback عند عدم توفر LLM (المطلب + سؤاله) | **RAR-001** | التزام واحد (fallback محدَّد لا fail-open)؛ qualifier «كيف تعمل» محفوظ كسؤال تنفيذ |
| **MERGE-G04** | RAR003-S12-003 (:316) ⊕ RAR003-S12-021 (:340) | لا مفاتيح/أسرار ظاهرة للمستخدم (No user-visible keys) | **RAR-003** | تكرار داخل RAR-003 لنفس الالتزام (D9/م) |

## بنود متشابهة **لم تُدمج** (تُبقى INDEPENDENT — سبب الاستقلال)
- **Audit**: RAR001-S12-015 (Audit Event Catalogue) · RAR002-S14-013 (Audit/non-repudiation) · RAR005 (Principal/Actor/On-Behalf-Of) · RAR006-S11-… — نطاقات وأغراض مختلفة (كتالوج أحداث ≠ خاصية عدم إنكار ≠ تدقيق تفويض ≠ تدقيق أحداث حية). مرساة دستورية مشتركة (م3) لا تكفي للدمج.
- **Permissions**: RAR001-S12-006 (Permission-per-stage) · RAR002-S14-004 (Least privilege) · RAR002-S14-006 (Row/Object/Field) — مبادئ متمايزة تحت م2؛ التزامات إنفاذ مختلفة.
- **Secrets**: RAR002-S14-007 (Secret handling — Agent) مقابل MERGE-G04 (No user-visible keys — UI) — سطحان و actor مختلفان رغم مرساة D9 المشتركة.
- **Idempotency**: RAR001-S12-010 (Task retry) مقابل RAR006 (Event idempotency/replay) — نطاقان مختلفان (تنفيذ مهمة ≠ استيعاب حدث)؛ RAR006 مؤجَّل إلى B2 أصلاً.
- **Versioning**: RAR001-S12-011 (Task/Automation versioning) مقابل RAR002-S14-… lifecycle — كائنات مختلفة.

## ثبات الخريطة
بعد Commit 1 تصبح هذه الخريطة + `CANONICAL-ITEM-UNIVERSE.md` = **B1 FROZEN CANONICALIZATION BASELINE**: لا يُعاد دمجها ولا يُنقل ممثل ولا تُغيَّر قاعدة أدنى RAR إلا بخطأ مثبت + تقرير + تجاوز SA + commit تصحيحي مستقل (B1 §10/§17). B2 يستهلكها كما هي.
