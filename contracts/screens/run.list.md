# عقد الشاشة — `run.list` (Renderer — قائمة كيان)

```contract
id: screens.run.list
version: 0.1
status: Candidate
owner: Specification Architect (SA-delegated)
since: 2026-07-19 (G1) — بذرة مشتقة، لا تأليف جديد
relates: screens.template · identity.record · enums.dictionary · بطاقة السلوك 2 · جدول الجرد A/B (run.list)
```

## §1 التعريف والتموضع (جدول A)
‏Renderer — قائمة كيان · ‏route: ‏`/app/{entity}` · ‏phase: ‏1→2 · ‏audience: مستخدم حسب الصلاحية · ‏type: ‏**renderer** (قالب G13) · ‏end_user: ✔ · ‏priority: ‏High · **archetype: ‏List** — هذه الشاشة **قالب**: تتجسد لكل كيان من تعريف نوعه (لا شاشة لكل كيان).

## §2 الربط الحوكمي (جدول B)
قائمة أي كيان (حتمي) · **البيانات:** صفوف الكيان RLS-مرشّحة · **الأفعال:** ‏`record.create` (زر) · ‏`record.search`/`filter`/`export`† · **الصلاحيات:** ‏`records.{entity}.read` (+‏export بسياسة P4†) · **التدقيق:** ‏`RECORD_EXPORTED`† · †التصدير يظهر من P4 · **المكافئ المحادثي:** بطاقة بحث/إنشاء في ws ‏(P6+) بنفس `action_id`.

## §3 السلوك الملزم (بطاقة 2)
**افتراضياً:** ‏header بعنوان الكيان + زر إنشاء (إن مسموحاً) · بحث سريع · 5–7 أعمدة · صف مختار · ترقيم أسفل. **مطويّ:** الفلاتر المتقدمة (drawer end) · ‏column picker · أفعال الصف الإضافية تحت ⋯. **حسب الصلاحية:** أزرار الأفعال HIDDEN-SERVER لغير المخوّل · صفوف خارج RLS **لا تظهر ولا تُعدّ** · حقول FLS خلايا مقنَّعة «•••». **drawer:** معاينة الصف · الفلاتر المتقدمة. **modal:** التصدير المحكوم (نطاق ثم تأكيد بوسم) ثم صفحة حالة. **page:** «فتح كامل» ⇒ ‏`run.detail` · التحرير ⇒ ‏`run.form`. **إلى Renderer:** هذه الشاشة **هي** الـ Renderer — تغذي `run.detail`/`run.form`.

## §4 الحالات
من البطاقة: ‏default · loading (skeleton صفوف) · empty (إرشاد بلا مبالغة) · error · permission-denied (403 مفسَّرة) · masked (خلية) · audit-visible (زر «سلسلة تدقيق الصف» للمخوّل). ‏**+S16–S20:** تنطبق كاملة (شاشة بيانات حية) — وفق `UI_COMPONENT_STATES` v1.1 §S16.

## §5 معايير القبول
حزمة **List** كاملة في `ui/UI_SCREEN_GOVERNANCE_STANDARD.md` §5 (بما فيها تمييز «فارغ» عن «فارغ بفلتر» والترقيم وسقف الـ bulk) **+** خاص بالشاشة: (أ) الأعمدة/الأفعال تُبنى من تعريف النوع لا من كود الشاشة (قالبية G13)؛ (ب) خلية مقنَّعة واحدة على الأقل وشارة workflow state في العرض المرجعي؛ (ج) `reference_number` ظاهر في كل صف (‏identity.record §2).

## §6 الانحرافات وCorrection candidates `[حقيقة — aql@eab9f99]`
التجربة بنت `records-list` ضمن مسارات لا تطابق `/app/{entity}` وبأسماء حقول camelCase (‏`RecordInstance`) — **CC-RL-1:** مواءمة المسار للجرد؛ **CC-RL-2:** مواءمة أسماء الحقول لـ snake_case عبر طبقة الأنواع؛ كلاهما يُحسم في **FP لاحقة لمسار Renderer** (ليس FP-0001/0002) — مسجل هنا لمنع الحسم الصامت.

## §7 التبعيات
‏`identity.record` (الرباعية في كل صف/معاينة) · ‏`enums.dictionary` (‏status/classification للشارات) · عقد الفعل `record.create` (تبعي عند اعتماد `admin.actions`).

## §8 الاختبارات
جدول بحالتي بيانات/فارغ · drawer معاينة بثلاثة أفعال رأسية كحد أقصى · 403 مفسَّرة · صفوف RLS لا تُعدّ (عدّاد الترقيم يطابق المرئي) · لقطتا RTL ‏Light/Dark.
