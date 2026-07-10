# EXECUTION_REPORT.md — تقرير تنفيذ دفعة v0.8 (Conversational & Workflow)

> **Version:** 1.0 · **Date:** 2026-07-10 · **المنفِّذ:** وكيل تنفيذ مفوَّض من SA (تفويض كامل — جلسة 2026-07-10)
> **النطاق:** SPECS = `local-rag-enterprise-specs` (هذه الدفعة) + PLATFORM = `local-rag-enterprise-platform` (تحديث `docs/SPEC_SOURCE.md` فقط)
> **المرجع الحاكم للدفعة:** تعليمات SA المؤرخة 2026-07-10 (جرد 100% → تدقيق → إصلاحات → دفعة التعديلات المعتمدة → إصدار v0.8 وفق Option B → تحديث PLATFORM → هذا التقرير)
> **الثوابت غير الممسوسة:** D9 · runs.list/runs.detail · حالات النموذج الست · PROVIDER_CONFIG_APPLIED_BY_OPS · «لا DDL من LLM» · superseded/ · decisions/adr/ · constitution.md · ترتيب المراحل

---

## §1 الجرد (PHASE 0)

قُرئت ملفات المستودع بنسبة 100%: **55 ملف Markdown + 5 ملفات أخرى (SVG/أصول) = 60 ملفاً**، على قاعدة `main` عند `b03c9e3`. التوزيع: 20 ملف `ui/` · 6 `methodology/` · 4 `decisions/` (+adr) · 12 `superseded/` (تاريخية موسومة — لم تُمس) · 2 `architecture/` (+diagrams) · `phases/` (README + roadmap + phase-0) · الجذر (README · vision · constitution · PACKAGE_CHECKLIST · github-docs-structure) · `handoff/` · `references/`. الحالة المعلنة لكل ملف قورنت بمحتواه الفعلي وبالفهارس الثلاثة (PACKAGE_CHECKLIST · github-docs-structure · handoff) — الانحرافات المكتشفة في §2.

## §2 التدقيق — Findings (PHASE 1)

| # | الوصف | الحالة |
|---|---|---|
| **F-1** | وسم `v0.7.1-responsive-ui` موجود على commit `c6dc18f` لكنه **lightweight** بلا ZIP asset وبلا SHA-256 وبلا إدخال handoff — انحراف عن نمط **Option B** المعمول به منذ v0.5 (وسوم v0.5/v0.6/v0.7 annotated) | **معالَج جزئياً:** H-0008 توثيق بأثر رجعي (FIX-12) + توثيق الحزمة في PACKAGE_CHECKLIST (ضمن FIX-10) · **المتبقي بقرار SA:** تسوية الوسوم lightweight القديمة (v0.1/v0.2/v0.2.1/v0.4/v0.7.1) — لم تُمس |
| **F-2** | `github-docs-structure.md` (v1.5) لا يُدرج ملفات `ui/` لحزمتَي v0.5/v0.6 (11 ملفاً) + اسم جذر الشجرة قديم (`local-rag-enterprise-docs` بدل `-specs`) + نطاق handoff قديم (H-0001..H-0004) — بند (b) من تعليمات SA | **مُصلح** — FIX-9 |
| **F-3** | ملفات حزمة v0.3 المُحالة من كل الفهارس **غير موجودة في الريبو**: `phases/PHASE_MASTER_PLAN.md` · `phases/designs/phase-1..8-*.md` (8 ملفات) · `phases/BACKLOG_DEFERRED_SCOPE.md` — **ولا يوجد tag v0.3 أصلاً** (الموجود: v0.1 · v0.2 · v0.2.1 · v0.4..v0.7.1) | **موسوم لا مُصلح:** أُدرجت تحذيرات ⚠️ في الفهرسين (FIX-13)؛ **استعادة/تأليف الملفات بقرار SA** — ولهذا حُملت FR الجديدة في ملف دلتا مستقل (§4-B) |
| **F-4** | انحرافات PACKAGE_CHECKLIST: صف github-docs-structure يقول v1.0 والملف فعلياً v1.5 · حزمة v0.7.1 غير موثقة إطلاقاً · صفا handoff وarchitecture/README قديمان | **مُصلح** — FIX-10 (استُكمل أثناء الدفعة بتحديث صفوف open-decisions/handoff/architecture بعد تعديلها) |
| **F-5** | `architecture/README.md` يُحيل إلى الكتالوج والمنهجية **v2.0** والفعلي **v2.1** | **مُصلح** — FIX-11 |
| **F-6** | commit `b03c9e3` (تصحيح 2.0→2.1 في phases/README) واقع **بعد** وسم v0.7.1 وغير مُصدَر | **يُحل تلقائياً** — يدخل ضمن إصدار v0.8 |
| **F-7** | دفعة SA تعرّف قرار وضعَي العرض بالمعرّف **OD-WS-2**، وهو **محجوز** في `UI_AI_WORKSPACE_MODEL.md` لقرار مدة احتفاظ الجلسات | **مُعالَج بتوثيق:** اعتُمد الترقيم **OD-WS-4** مع ملاحظة تتبّع صريحة في جدول ODs بالملف وفي H-0009 |
| **F-8** | ملفات PLATFORM (`README.md` · `AGENTS.md`) تُحيل إلى إصدارات specs سابقة — خارج نطاق التفويض (PHASE 5 = `docs/SPEC_SOURCE.md` فقط) | **غير معالَج عمداً** — يقرّره SA |

## §3 الإصلاحات (PHASE 2 — FIX-9..14)

| FIX | الملف | المضمون |
|---|---|---|
| FIX-9 | `github-docs-structure.md` → **v1.6** | إدراج ملفات ui لحزم v0.5/v0.6 (+شروح Δ v0.7.1/v0.8) · تصحيح اسم الجذر إلى `local-rag-enterprise-specs` · تحديث نطاق handoff إلى H-0001..H-0009 · إدراج ملفات v0.8 الجديدة |
| FIX-10 | `PACKAGE_CHECKLIST.md` → **v1.7** | توثيق Δ v0.7.1 لأول مرة · تصحيح صف github-docs-structure المنحرف · تحديث صفوف handoff/architecture/open-decisions · إضافة صفوف v0.8 |
| FIX-11 | `architecture/README.md` → **v1.2** | تصحيح مرجعَي الإصدار v2.0 → v2.1 (الكتالوج والمنهجية) |
| FIX-12 | `handoff/handoff.md` | إدخال **H-0008** توثيقاً بأثر رجعي لإصدار v0.7.1 (كان بلا إدخال) |
| FIX-13 | الفهرسان (checklist + structure) | وسم ملفات v0.3 الغائبة بتحذير ⚠️ + إحالة Finding F-3 (بدل ادعاء وجودها) |
| FIX-14 | `handoff/handoff.md` | إزالة وسم «(الإدخال الحالي)» الملتصق خطأً بـ H-0002 القديم (استمرارية السجل) |

## §4 دفعة تعديلات SA المطبقة (PHASE 3)

### A — الأسطح المحادثية
| البند | الموضع المعياري | الخلاصة |
|---|---|---|
| **OD-WS-4** وضعا عرض ws.main (ورد بمعرّف OD-WS-2 — F-7) | `ui/UI_AI_WORKSPACE_MODEL.md` **§14** + صف جدول ODs | وضعا «بطاقات/محادثة» كتفضيل مستخدم (`ws.view_mode`)؛ وضع المحادثة: عمود نظيف، رد كامل العرض، أفعال inline بنفس عقد الأزرار الـ13، مرفقات ورفع/تنزيل داخل الرسائل بنفس خط P5، مصادر مطوية افتراضياً — **عرضيّ صرف** بقائمة ثوابت قطعية |
| متغيّر «inline message action» | `ui/UI_ACTION_BUTTON_MODEL.md` **§2.1** | متغيّر عرض فقط: نفس العقد/الحقول/دورة الحياة/ترتيب التقييم؛ لا تنفيذ مباشر من النقر؛ ≤3 أزرار والباقي خلف «⋯»؛ أفعال surface=console مستثناة |
| **A-UX-17** صياغة الهوية | `ui/UI_UX_ASSUMPTIONS.md` (§1 + قسم A-UX-17) + ضبط القاعدة 5 في بطاقات السلوك | السطح المحادثي **مسموح ومحكوم**؛ المحظور حصراً: المحادثة غير المحكومة + استنساخ هوية منتجات قائمة؛ كل عبارات «ليست chatbot» تُقرأ بهذا الضبط |
| **OD-BLD-1** أوضاع الباني الثلاثة | `ui/UI_ADMIN_CONSOLE_MODEL.md` (ملاحظة §4-C + صف §7) | تقليدي/محادثي/مدمج كأساليب تأليف مسودة فقط؛ الخط draft→migration→checks→approval→apply **بلا تغيير**؛ **الـ LLM يكتب metadata فقط — لا DDL**؛ سطح أدمن لا يمس قاعدة «لا builder للمستخدم النهائي» |
| مشاعية الأنماط المحادثية | `ui/UI_REFERENCE_USAGE_POLICY.md` **§3.1** | الأنماط المحادثية العامة مشاعة صناعياً؛ القيد حصراً على الكود/الهوية/العلامة |

### B — سير العمل والتنظيم
| البند | الموضع المعياري | الخلاصة |
|---|---|---|
| **FR-3.11** وجهة الإرجاع الافتراضية | `phases/designs/DELTA_V08_FR_WORKFLOW_ORG.md` §1 | الافتراضي: معدّ المسودة · تعليق إلزامي · حدث `WORKFLOW_ITEM_RETURNED` (from/to_state · from/to_user · reason) · إشعار + history |
| **FR-3.12** الإرجاع الموجَّه | الملف نفسه §2 | لأي عضو مؤهل في الإدارة الأم للمستلم الأصلي · ترشيح إلزامي (صلاحية المرحلة + التصنيف/need-to-know + SoD) · صلاحية `workflow.return_route` للمكلَّف الحالي · سبب إلزامي + تدقيق + إشعار ثلاثي |
| **FR-1.Org-Ext** الشجرة المرنة | الملف نفسه §3 | `org_units` مرنة العمق (`parent_unit_id` · `unit_type` += section/unit) · عضوية على أي مستوى · توريث النطاق نزولاً |
| **OD-WF-1 · OD-WF-2 · OD-ORG-1** (مقفلة) | الملف نفسه §4 + فهرس open-decisions | رفض نهائي/إرجاع للمعالجة متمايزان · المكلَّف الحالي فقط · توجيه/تكليف فقط — لا RLS في v1 |
| التحديثات التبعية | بطاقتا السلوك 5/7 + **بطاقة 24 admin.org** · جرد الشاشات v1.3 · G6/G8 · UI_FIELD_NAMING §3 · فهرس OD v2.2 | زر «إرجاع إلى…» بقائمة مرشّحة + modal سبب · شاشة Org tree مرنة العمق · سلسلة التسمية الكاملة للإرجاع الموجَّه |

> **ملاحظة حمل الدلتا:** لغياب ملفَي تصميم Phase 1/Phase 3 (F-3)، حُملت FR الجديدة في `DELTA_V08_FR_WORKFLOW_ORG.md` — **تُدمج نصياً في الملفين الأم عند استعادتهما/تأليفهما** ويُوسم ملف الدلتا حينها superseded.

## §5 الملفات المتغيرة وبصماتها (SHA-256 عند لحظة الإصدار)

| الملف | التغيير | SHA-256 |
|---|---|---|
| PACKAGE_CHECKLIST.md | v1.6→**v1.7** (FIX-10 + صفوف v0.8) | `84460914adf6544bf3af92310d11aab9140c9c4d916f4c5c8989ab6042926091` |
| github-docs-structure.md | v1.5→**v1.6** (FIX-9 + FIX-13) | `f2e2a34c98f5c07f28d4338ab8565583fdd853b424916f37d7c1a86c7de61523` |
| architecture/README.md | v1.1→**v1.2** (FIX-11) | `4cf968bde9af3828f3919bf6ede995db372f33c7727a572a1ebd043efb756ab0` |
| handoff/handoff.md | +H-0008 (FIX-12) · +H-0009 · FIX-14 | `de2c6fe4a0ed5518a266f32732c2faaa7743148fa39395de8eff280cd95b9433` |
| decisions/open-decisions.md | v2.1→**v2.2** (+فهرس قرارات v0.8) | `4076a683f9d4032e96fe3db2878ffb44fb524f58a9a42ef12976941745092f4e` |
| ui/UI_UX_ASSUMPTIONS.md | v1.0→**v1.1** (+A-UX-17 + ضبط §1) | `0c4eb77ebcbf2fc6720dd0e2b44725a8043d91059291f52ce0b2ac7a76cfc445` |
| ui/UI_AI_WORKSPACE_MODEL.md | v1.0→**v1.1** (+§14 OD-WS-4) | `c1681922f3fe051dfbf8ad9aa5909bfda77e27a773d5f5bb7254cb9c9bddb8dc` |
| ui/UI_ACTION_BUTTON_MODEL.md | v1.0→**v1.1** (+§2.1 inline message action) | `5b398df1a0739ea1001819394c177dbd8fe3aa743e9c55397ee02f428e87d0f3` |
| ui/UI_ADMIN_CONSOLE_MODEL.md | v1.0→**v1.1** (+OD-BLD-1 + org مرنة) | `531cd60ad02f0473d825ee9ff3ab9f6181a7f7274974fc5a18750a32208afbbf` |
| ui/UI_REFERENCE_USAGE_POLICY.md | v1.0→**v1.1** (+§3.1 المشاعية) | `d5674bd2f611a9ddadfe4d9558dd0affb9b2e8152fd9a7b7fc8921fadb30f11e` |
| ui/UI_SCREEN_BEHAVIOR_CARDS.md | v1.0→**v1.1** (بطاقتا 5/7 + بطاقة 24 + قاعدة 5) | `3c2bb49d1180fb554dc331c80203af97b4fb3a7cd4e2661acbb216b155c5be65` |
| ui/UI_SCREEN_INVENTORY.md | v1.2→**v1.3** (صفوف الإرجاع/org/ws) | `655f7aaa817dd074394040fd45202d05ed8d50824261ae7af532b9f4d17e3a07` |
| ui/UI_FIELD_NAMING.md | v1.0→**v1.1** (+سلسلة الإرجاع الموجَّه §3) | `8176dac6e31fa527eddd58bc3bf615c7d1b97ac7c2ee381236017e050c4f72a2` |
| ui/UI_STITCH_PROMPTS_BY_PHASE.md | v1.0→**v1.1** (G6 + G8) | `6220ce61e67d0f181356ded31073c7fc5a66853e4c80e8a9c4bef234aac1fbd2` |
| phases/designs/DELTA_V08_FR_WORKFLOW_ORG.md | **جديد v1.0** (حامل FR/OD) | `4194b692dd0b7f93f59374830e169536e325da7c0c3629fb4a7d853171c02198` |
| EXECUTION_REPORT.md | **جديد v1.0** (هذا الملف) | — (بصمته ضمن بصمة ZIP الإصدار المعلنة في notes) |

**ملفات لم تُمس عمداً:** constitution.md · vision.md · superseded/* · decisions/adr/* · references/* · كل تصاميم المراحل المعتمدة وترتيبها.

## §6 القرارات المطبقة والمقفلة بهذه الدفعة (بقرار SA — 2026-07-10)

**OD-WS-4** (وضعا العرض — عرضيّ صرف) · **OD-BLD-1** (أوضاع الباني الثلاثة — LLM metadata فقط) · **OD-WF-1** (رفض نهائي ≠ إرجاع للمعالجة) · **OD-WF-2** (المكلَّف الحالي فقط) · **OD-ORG-1** (توجيه/تكليف فقط — لا RLS في v1) · اعتماد A-UX-17 · اعتماد FR-3.11/FR-3.12/FR-1.Org-Ext.

## §7 Findings غير المحلولة (تنتظر قرار SA — لم يجتهد الوكيل)

1. **F-3:** استعادة/تأليف حزمة v0.3 (PHASE_MASTER_PLAN + designs 1–8 + BACKLOG) ثم دمج ملف الدلتا فيها — **الأولوية قبل تصميم Phase 1**.
2. **F-1 (المتبقي):** تسوية الوسوم lightweight القديمة (v0.1 · v0.2 · v0.2.1 · v0.4 · v0.7.1) على نمط Option B من عدمه.
3. **F-8:** تحديث ملفات PLATFORM غير `docs/SPEC_SOURCE.md` (README/AGENTS تُحيلان لإصدارات أقدم).

## §8 فحوص النقاء

على كل الملفات المتغيرة: **لا كود منصة** (الوثائق تخطيطية؛ المعرّفات والمسارات API أمثلة تسموية قائمة أصلاً في اصطلاح UI_FIELD_NAMING) · **لا أوامر تشغيل** · **لا أسرار/endpoints حقيقية** (حدود D9 محفوظة نصاً) · لا حذف ملفات (لا supersession جديدة لزمت) · الالتزام بالعربية مع المصطلح الإنجليزي وقوالب Δ القائمة.

## §9 الإصدار (PHASE 4 — Option B)

commit واحد يضم كل ما سبق + **annotated tag `v0.8-conversational-and-workflow`** + ZIP asset للحزمة مع **SHA-256 معلن في notes الإصدار** + دفع إلى origin. PLATFORM: تحديث `docs/SPEC_SOURCE.md` إلى الوسم الجديد (PHASE 5). المرجع النافذ للمواصفات بعد هذا الإصدار: **tag `v0.8-conversational-and-workflow`**.
