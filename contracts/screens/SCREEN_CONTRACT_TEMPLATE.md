# SCREEN_CONTRACT_TEMPLATE.md — قالب عقد الشاشة

```contract
id: screens.template
version: 1.0
status: Proposed
owner: Specification Architect (SA-delegated)
since: 2026-07-19 (G1)
relates: contracts.standard · ui/UI_SCREEN_GOVERNANCE_STANDARD.md · ui/UI_SCREEN_INVENTORY.md · ui/UI_SCREEN_BEHAVIOR_CARDS.md
```

> **Purpose:** الشكل الإلزامي لعقد أي شاشة. **قاعدة الاشتقاق — لا التأليف الموازي:** أقسام §1 و§2 و§3 **تُشتق نصاً** من صف الشاشة في جدولي الجرد A/B ومن بطاقة سلوكها — العقد يكوّدها ويضيف طبقات القبول والانحراف، ولا يعيد تقرير ما قررته؛ أي تعارض بين العقد ومصدره = عيب في العقد يُصحَّح فوراً (‏EC-11).

## البنية الإلزامية (ثمانية أقسام)
1. **§1 التعريف والتموضع** — من صف الجدول A حرفياً: ‏screen_name · route · phase · audience · type · end_user · priority + **archetype** (من عمود v1.4) وأي وسم قالب.
2. **§2 الربط الحوكمي** — من صف الجدول B حرفياً: البيانات المعروضة (نطاق RLS/FLS) · ‏action_ids · ‏permissions · ‏audit_events · ملاحظات السطحين.
3. **§3 السلوك الملزم** — حقول بطاقة السلوك: افتراضياً يظهر · مطويّ · حسب الصلاحية · drawer · modal · page · متى إلى Renderer.
4. **§4 الحالات** — قائمة حالات البطاقة (من S1–S15) + انطباق S16–S20 حسب مصفوفة `UI_COMPONENT_STATES` v1.1.
5. **§5 معايير القبول** — بالإحالة إلى حزمة معايير الـ archetype في `ui/UI_SCREEN_GOVERNANCE_STANDARD.md` §5 **+** البنود الخاصة بالشاشة فقط.
6. **§6 الانحرافات وCorrection candidates** — كل فرق موثق بين العقد وأي تنفيذ قائم (‏aql) مع بوابة حسمه؛ **لا حسم صامتاً**.
7. **§7 التبعيات** — العقود/التعدادات/الهوية التي تستهلكها الشاشة.
8. **§8 الاختبارات** — ما يُثبت به القبول (بنود قابلة للأتمتة ما أمكن؛ لقطتا RTL ‏Light/Dark ضمن الحد الأدنى).

**دورة الاعتماد:** البذرة تُودَع **Candidate**؛ ترقيتها Approved عبر بوابة FP الخاصة بشاشتها (‏retrofit أو بناء) بتوقيع SA — عندها تكتسب المرتبة 5 (‏AUTHORITY).
