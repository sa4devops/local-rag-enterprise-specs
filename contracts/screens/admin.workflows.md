# عقد الشاشة — `admin.workflows` (تعريفات الـ Workflows)

```contract
id: screens.admin.workflows
version: 0.1
status: Candidate
owner: Specification Architect (SA-delegated)
since: 2026-07-19 (G1) — بذرة مشتقة
relates: screens.template · enums.dictionary (workflow_*) · بطاقة السلوك 13 · OD-P3-2 · FR-3.11/3.12
```

## §1 التعريف والتموضع (جدول A)
تعريفات الـ Workflows · ‏route: ‏`/admin/workflows` · ‏phase: ‏3 · ‏audience: أدمن · ‏type: ‏admin-config ‏(G8) · ‏end_user: ✖ · ‏priority: ‏High · **archetype: ‏Builder** · التفصيل في شاشة شقيقة `admin.workflow_detail`.

## §2 الربط الحوكمي (جدول B)
حوكمة التعريفات · **البيانات:** ‏workflow_definitions · **الأفعال:** ‏`wf.define`/`wf.validate`/`wf.submit` · **الصلاحية:** ‏`admin.workflows.manage`؛ **الاعتماد لـ`wf.approve` بمعتمِد غير المعرِّف (SoD)** · **التدقيق:** ‏`WORKFLOW_DEFINED`/`WORKFLOW_VALIDATED`.

## §3 السلوك الملزم (بطاقة 13)
**افتراضياً:** قائمة الـ workflows (اسم · كيان · حالة · نسخة) + زر «تعريف جديد». **مطويّ:** التفصيل صفحة `admin.workflow_detail`. **drawer:** ‏Validation report (دورات، حالات ميتة) · ‏diff نُسخ. **modal:** «اعتماد» typed · «تفعيل» typed لمعالجة الـ instances الجارية (**grandfathering**). **page:** فتح workflow ⇒ ‏`admin.workflow_detail` (**جدول حالات/انتقالات مُهيكل + tab مصفوفة الاعتماد — بلا canvas في v1**). **إلى Renderer:** ‏N/A — الـ workflow يعمل على سجلات الـ Renderer. **الإرجاع الموجَّه:** يدعم `workflow.return_route` وحدث `WORKFLOW_ITEM_RETURNED` ‏(FR-3.11/3.12).

## §4 الحالات
من البطاقة: ‏default · loading · empty · error (**دورة مكتشفة**) · disabled (تفعيل قبل اعتماد) · confirmation · approval · success · failed · audit-visible. ‏**+S16–S20:** ‏S18/S19/S20.

## §5 معايير القبول
حزمة **Builder** §5 **+** خاص: (أ) ‏Validation يكشف الدورات والحالات الميتة قبل السماح بالتقديم؛ (ب) التفعيل مع instances جارية يُظهر خيار grandfathering صراحة؛ (ج) SoD مفروض (المعرِّف لا يعتمد)؛ (د) عرض التعريف **جدولاً مهيكلاً** هو المرجع في v1.

## §6 الانحرافات وCorrection candidates `[حقيقة — aql@eab9f99 مقابل بطاقة 13]`
**CC-WF-1 (الأبرز):** بطاقة 13 تنص حرفياً: «canvas مرئي معقد بـ nodes وwires **مؤجَّل — OD-P3-2**»، بينما بنت التجربة `workflow-canvas-builder` بعُقد ووصلات (‏`WorkflowNode`/`WorkflowEdge`) — **الـ canvas التجريبي استكشاف غير معتمد**؛ عقد v1 يبقى على الجدول المهيكل، ومصير الـ canvas يُحسم حصراً بفتح **OD-P3-2** بقرار مالك (خيارات بوابة G4: إبقاؤه خلف علم تجريبي admin-only، أو تجميده، أو اعتماده بفتح القرار) — **لا حسم صامتاً هنا**. **CC-WF-2:** ‏`workflow_status` الثنائية (‏draft/published) لا تكفي دورة SoD (تحتاج حالة تقديم/اعتماد وسيطة) — تُواءم مع القاموس. **CC-WF-3:** المسار.

## §7 التبعيات
‏`enums.dictionary` (‏workflow_node_type/workflow_status) · عقد `admin.actions` (عُقد action تستهلك أفعالاً معرَّفة) · ‏`identity.record` (السجلات المعالجَة) · تصميم P3 عند تفعيله (‏FR-3.x).

## §8 الاختبارات
تعريف → ‏validate بدورة مزروعة يفشل مفسَّراً → إصلاح → ‏submit → اعتماد بشخص مختلف → تفعيل مع instances جارية يعرض grandfathering · لقطتا RTL.
