# RAR-004 — متجر التكاملات والامتدادات المحكوم
## Governed Integration, Connector & Extension Store

> **نوع الوثيقة:** Request for Architectural Review (RAR)  
> **المشروع:** AQL / AQLORA Enterprise AI Platform  
> **الحالة الأولية:** Partially Covered — Prepare Architecture Now, Implement Store UI Later  
> **الغرض:** تقييم الحاجة والحدود والعقود ودورة الحياة دون بناء Store الآن  
> **قاعدة السلطة:** المستودع الحاكم الفعلي يتقدم على هذا التصور  
> **قاعدة التنفيذ:** لا Package Manager ولا Store UI ولا تعديل Repo قبل دراسة واعتماد

---

## 1. ملخص تنفيذي

نريد قدرة مؤسسية مركزية لإدارة Connectors وProviders وExtensions وWorkflow Templates وAutomation Recipes وحزم أخرى، مع توقيع وتحقق وتوافق وإدارة إصدار وتثبيت Offline وRollback وصلاحيات وتدقيق. لا نريد Marketplace عاماً، ولا نظام Plugins مفتوحاً يسمح بحقن كود غير موثوق داخل المنصة.

المواد السابقة تشير إلى وجود Provider/Capability Registry واتجاهات للConnectors وOffline Deployment، وإلى توصية بتوثيق Extension/Store Architecture الآن وتأجيل واجهة Store والتنزيل والترقية إلى مرحلة لاحقة. لكن لا نملك إثباتاً بأن الحدود بين Store وRegistries والعقود ودورة الحياة أصبحت مكتملة.

المطلوب من Claude تحديد:

- هل Store Bounded Context مستقل أم Facade فوق Registries؟
- ما الذي يملكه وما الذي لا يملكه؟
- ما أنواع الحزم؟
- كيف تعمل الثقة والتوقيع والتوافق والRollback؟
- ما الحد الأدنى المطلوب توثيقه الآن؟
- ما الذي يبقى Deferred بوضوح؟

---

## 2. نية المنتج

نريد كتالوجاً محكوماً يمكن أن يحتوي على:

- Connectors إلى أنظمة داخلية.
- Data ingestion adapters.
- AI provider/runtime adapters.
- Approved Actions.
- Workflow Templates.
- Automation Recipes.
- Dashboards أو visual modules ضمن حدود.
- Reports وExporters.
- OCR/Parsers.
- Model packages أو configuration profiles.
- Policy packs أو mappings.
- UI extensions إن سمحت المعمارية لاحقاً.

كل عنصر يجب أن يعرف:

- المصدر.
- الناشر.
- الإصدار.
- التوافق.
- التوقيع أو التحقق.
- الصلاحيات المطلوبة.
- الاعتماديات.
- الحالة التشغيلية.
- الإعدادات.
- Secret references.
- سجل التثبيت والترقية والتراجع.
- دعم Offline Bundle.

---

## 3. لماذا نحتاج Store محكوماً

1. منع التكاملات اليدوية غير القابلة للتدقيق.
2. توحيد دورة حياة Connectors وExtensions.
3. تسهيل النشر بين الجهات.
4. الفصل بين «متاح للمنصة» و«مفعّل لهذه الجهة».
5. دعم Upgrade وRollback.
6. إدارة Dependencies وCompatibility.
7. عرض قدرات معتمدة للمستخدمين وAgent Builder دون كشف أسرار.
8. توسيع المنصة دون تعديل Core لكل تكامل.
9. دعم الشبكات المغلقة والتحقق Offline.
10. إظهار أثر التعطيل أو الإزالة قبل التنفيذ.

---

## 4. مبدأ أساسي: Store ليس Runtime

التصور الوظيفي:

```text
Store / Catalog
→ Approved Package Metadata
→ Import / Verify / Approve
→ Install
→ Register capabilities/connectors/actions
→ Configure secret references and policies
→ Enable for scope
→ Runtime invokes through governed contracts
→ Health / Usage / Audit feedback
```

المتجر يدير Metadata والحزم والسياسات ودورة الحياة، ولا ينفذ منطق الأعمال بنفسه. على Claude منع تكرار Provider Registry وConnector Registry وAction Registry داخل Store.

---

## 5. أنواع الحزم المحتملة — للنقاش فقط

1. Connector Package.
2. Data Source Adapter.
3. Action Provider.
4. Model Runtime Adapter.
5. Embedding/Reranker Provider.
6. Workflow Template.
7. Automation Recipe.
8. UI Module.
9. Report/Exporter.
10. Parser/OCR.
11. Policy/Mapping Pack.
12. Composite Solution Bundle.

لا نريد اعتماد كلمة Plugin كنوع عام يخفي فروق الأمن ودورة الحياة. Claude يحدد Taxonomy أقل وأوضح إن أمكن.

---

## 6. Package Manifest — المتطلبات الوظيفية

كل حزمة قد تحتاج معلومات مثل:

- Stable package ID.
- Display name.
- Publisher/issuer.
- Version.
- Package type.
- Supported platform/spec versions.
- Dependencies.
- Required capabilities.
- Permissions/scopes.
- Network requirements.
- Artifact hashes.
- Signature/attestation.
- Allowed install hooks.
- Migrations.
- Rollback support.
- Configuration schema.
- Secret references.
- Health checks.
- License.
- SBOM reference.
- Offline availability.
- Deprecation/support dates.
- Documentation.
- Compatibility constraints.

هذا ليس Schema مفروضاً. Claude يقرر ما هو مشترك وما هو خاص بكل Package Type.

---

## 7. Trust and Supply Chain

بما أن المنصة مؤسسية وAir-Gapped، يجب تحليل:

- Trusted publisher model.
- Signing keys and rotation.
- Artifact hash verification.
- SBOM.
- License allow/deny policy.
- Vulnerability scanning في بيئة التحضير المتصلة.
- Import approval في الشبكة المغلقة.
- Quarantine قبل التثبيت.
- Immutable artifact storage.
- Provenance.
- Revoked package handling.
- Tamper evidence.
- Reproducible verification.
- Separation between package metadata and secrets.
- Emergency disable.
- Audit of every transition.

لا نريد فرض Sigstore أو أداة محددة. المتطلبات يجب أن تكون Tool-agnostic أولاً.

---

## 8. دورة الحياة المقترحة للمراجعة

```text
Discovered
→ Imported
→ Quarantined
→ Verified
→ Approved
→ Installed
→ Configured
→ Enabled
→ Disabled
→ Upgrading
→ Rolled Back
→ Deprecated
→ Removed
```

يجب الفصل بين:

- **Installed:** Artifact موجود.
- **Configured:** الإعدادات مكتملة.
- **Enabled:** مسموح بالاستخدام ضمن Scope.
- **Healthy:** Runtime يعمل.
- **Degraded / Unreachable / Misconfigured:** حالة تشغيلية.
- **Approved:** قرار حوكمة.
- **Available:** ظاهر للمستخدم أو Agent Builder.

هذا الفصل مهم خصوصاً في Connectors. Claude يقرر إن كان يعمم على جميع Package Types.

---

## 9. Online Preparation وOffline Transfer

### 9.1 Online Preparation

- تنزيل Artifacts.
- Resolve dependencies.
- Generate lockfiles/manifests.
- Verify licenses.
- Scan vulnerabilities.
- Generate hashes/signatures.
- Produce SBOM.
- Build offline bundle.

### 9.2 Offline Import

1. نقل الحزمة للشبكة المغلقة.
2. Import إلى Quarantine.
3. تحقق من Hash/Signature دون اتصال.
4. مراجعة Metadata وLicense وPermissions.
5. Approval من مسؤول مخول.
6. Install.
7. Configure secret references.
8. Health test.
9. Enable for scope.
10. Audit كل خطوة.

يجب تحديد العلاقة مع Desktop/Offline Deployment Bundle، ومنع خلط حزمة المنصة الأساسية بحزم الامتدادات.

---

## 10. الصلاحيات وفصل الواجبات

أدوار محتملة:

- Store Viewer.
- Package Importer.
- Security Reviewer.
- License Reviewer.
- Package Approver.
- Installer.
- Configurator.
- Secret Manager.
- Enable/Disable Operator.
- Auditor.
- Publisher.

المبادئ:

- من يستورد لا يعتمد أمنياً تلقائياً.
- من يثبت لا يرى Secret values بالضرورة.
- من يضبط لا يملك النشر في كل Scope.
- من يعطل يجب أن يرى Impact.
- كل صلاحية قابلة للتقييد بالمؤسسة والوحدة والنوع.
- Emergency actions مسجلة ومراجعة.

Claude يقرر الحد الأدنى الواقعي ولا يفرط في الأدوار.

---

## 11. Upgrade وRollback وCompatibility

على المراجعة معالجة:

- Version policy.
- Platform/API/spec compatibility.
- Database migrations.
- Maintenance windows.
- Backup before upgrade.
- Dependency conflicts.
- Downgrade restrictions.
- Configuration migration.
- Data ownership at uninstall.
- Rollback evidence.
- Orphaned workflows/actions.
- Impact preview before disable/remove.
- Pinning.
- LTS channels.
- End-of-support.
- Partial failure.
- Compatibility tests.

لا نريد افتراض SemVer إذا لم يكن مناسباً، لكن نحتاج قاعدة إصدار قابلة للتدقيق.

---

## 12. Impact Analysis

قبل Disable أو Upgrade أو Remove، يجب أن يستطيع النظام أو الأدمن معرفة ما يتأثر:

- Workflows.
- Agents.
- Actions.
- Schedules.
- Connectors.
- Screens.
- Reports.
- Data ingestion jobs.
- Permissions.
- Stored configuration.
- Active runs.

المطلوب تحديد هل نحتاج Dependency Graph قانونياً، وكيف يحافظ على Stable IDs.

---

## 13. UI Extensions — مستوى خطورة مرتفع

لا نريد السماح بحقن JavaScript اعتباطي داخل واجهة AQL. الخيارات التي يجب أن يقيمها Claude:

- رفض UI Extensions في MVP.
- Declarative widgets فقط.
- Approved component registry.
- Sandboxed modules لاحقاً.
- Micro-frontends ضمن Gate صارم.
- Server-rendered/report modules.

قد يكون القرار الصحيح هو تأجيل UI Extensions بالكامل. المطلوب توثيق السبب والحدود.

---

## 14. Code Execution Boundaries

إذا كانت بعض الحزم تحتوي كوداً، يجب تحديد:

- هل يعمل داخل Process؟
- داخل Container مستقل؟
- كخدمة خارجية داخل LAN؟
- كConfiguration فقط؟
- ما Network/File/System access؟
- ما Resource limits؟
- كيف تسجل Calls؟
- كيف تمنع package من تجاوز صلاحياتها؟
- كيف يختلف ذلك حسب Package Type؟

لا نطلب اختيار Runtime الآن، بل توثيق Invariants والخيارات المؤجلة.

---

## 15. العلاقة مع Registries القائمة

على Claude رسم الحدود مع:

- Provider Registry.
- Capability Registry.
- Connector Registry.
- Action Registry.
- Workflow Template Catalogue.
- Model Catalogue.
- Screen/Route Registry.
- Dependency/License Registry.
- Audit/Observability.

السؤال الحاسم:

> هل Store مجرد Presentation + Lifecycle فوق Registries، أم Bounded Context يملك Package وInstallation وApproval بينما تبقى القدرات التشغيلية لدى Registries؟

---

## 16. سيناريوهات الاستخدام

### UC-01 — استيراد Connector داخلي
حزمة HR Connector تأتي من ناشر موثوق، تتحقق، تثبت، تضبط Secret Reference، ثم تفعّل لوحدة محددة.

### UC-02 — ترقية Connector
يعرض النظام Dependencies وWorkflows المتأثرة وCompatibility وDowntime وRollback Plan قبل الاعتماد.

### UC-03 — تعطيل Package
يعرض أثر التعطيل على Runs وAgents وWorkflows، ويتطلب سبباً ويسجل Audit.

### UC-04 — Offline Import فاشل
Hash mismatch يبقي الحزمة Quarantined ولا يسمح بالتثبيت.

### UC-05 — Workflow Template
يظهر كقالب قابل للنسخ، لكنه لا يمنح المستخدم Skills أوPermissions غير موجودة.

### UC-06 — Revocation
اكتشاف ثغرة يؤدي إلى Revoked status، منع تثبيت جديد، تنبيه الجهات، وخطة Upgrade/Disable.

### UC-07 — Removal
لا يحذف بيانات الأعمال تلقائياً، ويحتاج Retention/Ownership plan.

### UC-08 — Dependency Conflict
حزمة جديدة تطلب إصداراً غير متوافق. النظام يرفض أو يقدم خياراً واضحاً دون كسر الحزم الحالية.

---

## 17. الحالة المتوقعة داخل المستودع — تحتاج إثباتاً

مواد المصالحة تشير إلى:

- Store الكامل مؤجل.
- Extension/Store Architecture مطلوب الآن.
- Connector Contract وفصل Enabled/Health مطلوبان.
- Deferred Entry للواجهة والتنزيل والترقية.
- Provider/Capability Registry direction موجود.
- Offline Deployment requirements موجودة.
- لا UI Store كاملة.

Claude يجب أن يحدد:

- هل Architecture Doc موجود فعلياً؟
- هل يوجد Package Contract أو Manifest؟
- هل Deferred Register محدث؟
- هل Phase 7/8 تغطي التنفيذ؟
- هل توجد تعارضات بين Connector وExtension وProvider؟

---

## 18. الفجوات المحتملة — قائمة فحص

- Canonical definition of Package/Extension/Connector.
- Package taxonomy.
- Manifest Contract.
- Signature/Trust model.
- Installation Record.
- Approval Record.
- Compatibility Contract.
- Dependency Graph.
- License/Security metadata.
- Offline import/export contract.
- Lifecycle.
- Rollback.
- Enabled vs Health separation.
- Impact Analysis.
- Permission Matrix.
- Audit Events.
- UI Screen Contracts المؤجلة.
- Phase mapping.
- Acceptance tests.
- Uninstall semantics.
- Secret handling.
- Revocation.
- Emergency disable.

---

## 19. الأسئلة المعمارية المفتوحة

1. هل Store Bounded Context أم Facade؟
2. ما الذي يملكه Store وما الذي تملكه Registries؟
3. هل Core Modules تستخدم نفس Package Model؟
4. ما مستوى Extension المسموح في Modular Monolith؟
5. أين يعمل Package Code؟
6. كيف تفرض Compatibility دون ربط بأداة؟
7. ما الحد الأدنى المطلوب الآن؟
8. هل نحتاج ADR أم Architecture Contract؟
9. كيف تدار Vendor Packages في Air-Gap؟
10. هل يسمح للجهة بنشر Package خاصة؟
11. من يوقعها؟
12. كيف تمنع Network/File access غير المصرح؟
13. ما سياسة UI Extensions؟
14. كيف ترتبط Package Capabilities بـAgent Builder؟
15. ما الاختبارات قبل Enable؟
16. كيف تدار Migrations وRollback؟
17. هل Templates Packages أم Catalogue entries؟

---

## 20. خارج النطاق

- بناء Store UI.
- تنفيذ Package Manager.
- اختيار Signing Vendor.
- Public Marketplace.
- Arbitrary Plugins.
- تشغيل Third-party Code.
- اختيار Container Runtime.
- ترقية فعلية.
- كتابة Installer.
- دعم UI Extensions الآن.

---

## 21. المطلوب من Claude Architecture

1. Evidence Baseline.
2. Store/Registry Boundary Decision.
3. Package Taxonomy.
4. Trust and Lifecycle Model.
5. Offline Flow.
6. Permission/Separation-of-Duties Matrix.
7. Compatibility and Rollback Requirements.
8. UI Extension Policy.
9. Current / Prepare Now / Later map.
10. Minimal Repository Updates الآن.
11. Owner Decisions.
12. Deferred Items.
13. التوقف دون تعديل.
14. بعد الاعتماد فقط: Prompt لـClaude Code لتوثيق المعمارية والـDeferred state.

---

## 22. شكل مخرجات Claude

1. Executive Verdict.
2. Evidence Baseline.
3. Coverage Matrix.
4. Boundary Diagram.
5. Package and Lifecycle Model.
6. Trust/Supply-chain Model.
7. Offline Installation Flow.
8. Options and Trade-offs.
9. Recommended Minimal Delta.
10. Owner Decisions.
11. Deferred Items.
12. Acceptance Criteria.
13. Proposed Claude Code Prompt.
14. Stop Statement.

---

## 23. ما لا نريده

- لا Marketplace مفتوح.
- لا Arbitrary code execution.
- لا اختيار تقنية قبل تعريف المتطلبات.
- لا تكرار Registries.
- لا Store UI قبل العقود.
- لا خلط Enabled مع Healthy.
- لا إهمال Rollback وImpact.
- لا تعديل Repo أثناء الدراسة.

---

## 24. معايير قبول المراجعة

تُرفض إذا:

- لم تعالج Supply Chain وOffline Verification.
- لم تفصل Store عن Runtime.
- لم تحدد الحدود مع Registries.
- سمحت UI/Code Extensions بلا عزل.
- تجاهلت Compatibility وRollback.
- لم تحدد ما هو مؤجل.
- لم تقدم Evidence من المستودع.
