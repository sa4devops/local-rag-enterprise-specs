# عقد الشاشة — `admin.actions` (Action Registry)

```contract
id: screens.admin.actions
version: 0.1
status: Candidate
owner: Specification Architect (SA-delegated)
since: 2026-07-19 (G1) — بذرة مشتقة
relates: screens.template · enums.dictionary (risk_level) · بطاقة السلوك 12 · UI_ACTION_BUTTON_MODEL · UI_FIELD_NAMING §2/§5
```

## §1 التعريف والتموضع (جدول A)
‏Action Registry · ‏route: ‏`/admin/metadata/actions` · ‏phase: ‏3 · ‏audience: أدمن · ‏type: ‏admin-config ‏(G7) · ‏end_user: ✖ · ‏priority: ‏High · **archetype: ‏Builder**.

## §2 الربط الحوكمي (جدول B)
تعريف الأزرار/الأفعال · **البيانات:** ‏action_buttons registry · **الأفعال:** ‏`action.define`/`action.edit` (**أثر معلن فقط** — من كتالوج، لا كود حر) · **الصلاحية:** ‏`admin.actions.manage` · **التدقيق:** ‏`ACTION_DEFINED`/`ACTION_CHANGED` · **قلب الـ Dual-Surface** — الزر المعرَّف يُعرض على السطحين (Renderer + ws).

## §3 السلوك الملزم (بطاقة 12)
**افتراضياً:** قائمة الأفعال (‏action_id · label · risk · حالة) + فلتر target/entity + زر «تعريف فعل جديد». **مطويّ:** محرر عقد الفعل صفحة مستقلة. **حسب الصلاحية:** الشاشة لـ`admin.actions.manage`. **drawer:** محاكاة «مَن سيرى هذا الزر؟». **modal:** «اعتماد الفعل» typed. **page:** محرر العقد بحقول العقد الثلاثة عشر في تبويبات (تعريف · صلاحية · تحقق · مخاطر/تأكيد · أثر · تدقيق). **إلى Renderer:** ‏N/A مباشرة — العقد يُظهر أزراراً في Renderer وبطاقات في ws. **قيد بنيوي:** ‏`action_id` بفعل من الكتالوج المغلق (‏UI_FIELD_NAMING §5) والفعل الواحد يستدعي عملية واحدة (‏§2).

## §4 الحالات
من البطاقة: ‏default · loading · empty · error · disabled (تفعيل قبل اعتماد) · confirmation · approval · success · failed · audit-visible. ‏**+S16–S20:** ‏S18/S19/S20 (محرر تعريف).

## §5 معايير القبول
حزمة **Builder** §5 **+** خاص: (أ) مصفوفة المخاطر تستهلك `risk_level` من القاموس حصراً؛ (ب) لوحة محاكاة الرؤية تعرض نتيجة الخادم لا منطق عميل؛ (ج) لا محرر تعبيرات/‏scripting IDE ولا سحب-إفلات للأثر (بطاقة 12)؛ (د) عرض `action_id` ‏ASCII الحرفي بجانب الـ label دائماً في المحرر.

## §6 الانحرافات وCorrection candidates `[حقيقة — aql@eab9f99]`
تجربة `action-registry` تحمل عقد فعل بمدخلات/مخرجات/أخطاء/صلاحيات/نسخ (‏`Action` في types.ts) — أوسع اسمياً من حقول العقد الـ13 المرجعية: **CC-AC-1** مطابقة حقول التجربة على الحقول الـ13 حقلاً-حقلاً (فائض التجربة يُعلَّم أو يُسقط)؛ **CC-AC-2** ‏`ActionPermission` بأدوار `user_role` الثابتة ⇒ تُستبدل بربط `permission` القياسي؛ **CC-AC-3** المسار. **الحسم:** ‏FP مسار الأفعال (بعد FP-0002) — مسجل لمنع الحسم الصامت.

## §7 التبعيات
‏`enums.dictionary` (‏risk_level/status) · كتالوج الأفعال المغلق (‏UI_FIELD_NAMING §5) · عقد `run.list` (حيث تظهر الأزرار) · نموذج `UI_ACTION_BUTTON_MODEL`.

## §8 الاختبارات
تعريف فعل جديد بكل تبويبات العقد · محاولة فعل بأثر خارج الكتالوج تُرفض بـ error مفسَّر · محاكاة الرؤية لدورين مختلفين · اعتماد typed · لقطتا RTL.
