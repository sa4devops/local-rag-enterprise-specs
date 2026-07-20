# RECORD_IDENTITY.md — عقد هوية السجل (Record Identity Contract)

```contract
id: identity.record
version: 1.0
status: Proposed
owner: Specification Architect (SA-delegated)
since: 2026-07-19 (G1)
relates: ADR-0032 · constitution م17 · contracts.standard · ui/UI_SCREEN_INVENTORY.md (مسارات /app/{entity})
```

> **Purpose:** الهوية الموحدة لكل سجل ديناميكي عبر الشاشات والوصلات والتدقيق — رباعية إلزامية لا يكتمل عرض/ربط سجل بدونها.

## §1 الرباعية الإلزامية
| الحقل | النوع/الصيغة | القاعدة الملزمة |
|---|---|---|
| `internal_id` | **UUIDv7** | المفتاح التقني الوحيد للربط والمسارات العميقة؛ **آلية التوليد في التطبيق أو قاعدة البيانات — غير مربوطة بدالة إصدار PostgreSQL معيّن** (قرار مالك، ‏ADR-0032 بند 3؛ الموضع يُحسم قرارَ تنفيذٍ في P1)؛ لا يُعرض كقيمة أعمال |
| `reference_number` | نص ASCII بنمط يعرّفه تعريف النوع | **المعرف الظاهر للمستخدم — ‏immutable مدى الحياة (م17)**؛ يظهر في كل سياق سجل (رأس التفاصيل · صف القائمة · بطاقة ws · الإشعارات) وهو مفتاح البحث البشري |
| `record_type_id` | معرف نوع السجل | يحدد الـ schema والسياسات والمسار `/app/{entity}` |
| `display_title` | حقل عرض يشتقه schema النوع | العنوان القرائي؛ لا يُستخدم للربط أبداً |

## §2 قواعد الاستهلاك
1. ‏**Deep-Link العام:** ‏`/app/{entity}/{id}` حيث `{id}` = ‏`internal_id` (اصطلاح الجرد)؛ البحث بالـ`reference_number` يحلّه الخادم إلى `internal_id`.
2. أي **إشارة سجل مضمّنة** (حقل reference · بطاقة محادثة · صف workflow) تنقل الرباعية كاملة — لا عناوين بلا مرجع ولا معرفات تقنية عارية.
3. أحداث التدقيق تسجّل `internal_id` + ‏`reference_number` معاً (تتبّع بشري وتقني).
4. **RLS/FLS** تعمل على النواة (‏ADR-0032) — الهوية لا تكشف ما تحجبه السياسات: السجل خارج النطاق لا يظهر ولا يُعدّ (بطاقة السلوك 2).

## §3 مواءمة التجربة `[حقيقة — aql src/mocks/types.ts]`
واجهة `RecordInstance` في التجربة تحمل الحقول `id · referenceNumber · typeId · title` (ضمن حقول أخرى) — التطابق البنيوي مع الرباعية قائم، والمواءمة **الاسمية** إلى snake_case القياسي (‏`internal_id` · ‏`reference_number` · ‏`record_type_id` · ‏`display_title`) تُنفَّذ في طبقة أنواع العميل ضمن **FP-0001** (‏Correction candidate مسجل — لا حسم صامتاً).

**Related:** `../../decisions/adr/ADR-0032-dynamic-records-hybrid-storage-uuidv7.md` · `../../constitution.md` (م17) · `../NAMING_AND_CONTRACTS_STANDARD.md` · `../../ui/UI_SCREEN_BEHAVIOR_CARDS.md` (بطاقة 2)
