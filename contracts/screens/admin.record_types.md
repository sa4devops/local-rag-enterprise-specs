# عقد الشاشة — `admin.record_types` (Screen/Record-Type Builder)

```contract
id: screens.admin.record_types
version: 0.1
status: Candidate
owner: Specification Architect (SA-delegated)
since: 2026-07-19 (G1) — بذرة مشتقة؛ هدف FP-0001 (Retrofit)
relates: screens.template · identity.record · enums.dictionary · بطاقة السلوك 11 · OD-BLD-1 · ADR-0032
```

## §1 التعريف والتموضع (جدول A)
‏Screen/Record-Type Builder · ‏route: ‏`/admin/metadata/screens` · ‏phase: ‏1→2 · ‏audience: أدمن · ‏type: ‏admin-config ‏(G7) · ‏end_user: ✖ · ‏priority: ‏High · **archetype: ‏Builder** — الشاشة التي أنتجت نسختها التجريبية في `aql` وهي **هدف FP-0001** (‏Retrofit عقدي — قرار DR-2).

## §2 الربط الحوكمي (جدول B)
بناء الأنواع والشاشات · **البيانات:** ‏screen_definitions + versions · **الأفعال:** ‏`screen.define`/`screen.version` · ‏`policy.set` ‏(RLS/FLS) · **الصلاحية:** ‏`admin.metadata.manage` · **التدقيق:** ‏`SCREEN_DEFINED`/`SCREEN_VERSIONED` · ‏`SCREEN_POLICY_CHANGED` · **مصدر schema للسطحين معاً** (Renderer + ws).

## §3 السلوك الملزم (بطاقة 11)
**افتراضياً:** قائمة الأنواع (اسم · حالة دورة الحياة · النسخة) + زر «تعريف جديد». **مطويّ:** الـ Builder صفحة مستقلة عند فتح تعريف. **حسب الصلاحية:** الشاشة لـ`admin.metadata.manage`؛ محاكاة «مَن سيرى؟» لمخوّلي `admin.policies`. **drawer:** ‏diff بين نسختين · المحاكاة. **modal:** «اعتماد النسخة» typed **بشخص مختلف (SoD ظاهر)**. **page:** «فتح Builder» ⇒ صفحة بشريط دورة حياة + تبويبات (الحقول · السياسات · التنقل · التوثيق). **إلى Renderer:** ‏N/A مباشرة — التعريف **يولّد** شاشات الـ Renderer. **أنماط التأليف الثلاثة (OD-BLD-1 — مقفل):** تقليدي · محادثي · هجين — الـ LLM يكتب **metadata فقط** فوق خط الإنتاج المحكوم غير المتغير.

## §4 الحالات
من البطاقة: ‏default · loading · empty · error (‏Validation فاشل بدورات) · disabled (تفعيل قبل اعتماد) · confirmation (اعتماد) · approval (بانتظار المعتمِد) · success · failed · audit-visible (drawer «سلسلة تعريف»). ‏**+S16–S20:** تنطبق S18 ‏(partial) وS19 ‏(saving) وS20 ‏(conflict — تحرير نسخة متزامن) — وفق مصفوفة v1.1.

## §5 معايير القبول
حزمة **Builder** في `ui/UI_SCREEN_GOVERNANCE_STANDARD.md` §5 **+** خاص: (أ) شريط دورة الحياة يعرض حالة التعريف من `enums.dictionary` بعد مواءمة FP-0001؛ (ب) الاعتماد يفرض SoD فعلياً (المعرِّف لا يعتمد نسخته)؛ (ج) لا WYSIWYG بأسلوب low-code استهلاكي (بطاقة 11 — «يجب ألا يُرى»)؛ (د) كل تفعيل قبل اعتماد ⇒ ‏disabled بتفسير.

## §6 الانحرافات وCorrection candidates `[حقيقة — aql@eab9f99]`
التجربة (‏screen-builder) بأنماطها الثلاثة مطابقة اتجاهاً لـ OD-BLD-1؛ الفروق المسجلة: **CC-RT-1** مسار التجربة ≠ ‏`/admin/metadata/screens`؛ **CC-RT-2** حالات `status_value` التجريبية تحتاج مواءمة شريط دورة الحياة (انظر قاموس التعدادات)؛ **CC-RT-3** حقول `RecordInstance` ‏camelCase. **حسم الثلاثة = نطاق FP-0001 نفسه.**

## §7 التبعيات
‏`identity.record` · ‏`enums.dictionary` (‏status_value/field_type) · عقد `admin.actions` (الأفعال المعروضة أزراراً) · مسار م10 للترحيلات المولَّدة (‏ADR-0032 §5).

## §8 الاختبارات
تعريف جديد → نسخة → اعتماد بشخص مختلف (رفض اعتماد الذات) · ‏Validation بدورة فاشلة يظهر error مفسَّراً · محاكاة «مَن سيرى؟» تعكس السياسات · لقطتا RTL ‏Light/Dark.
