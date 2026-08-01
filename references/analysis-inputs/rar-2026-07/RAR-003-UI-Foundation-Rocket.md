# RAR-003 — أساس الواجهة وتقنين مخرجات Rocket
## UI Foundation, Rocket Canonicalization & Open WebUI Exit

> **نوع الوثيقة:** Request for Architectural Review (RAR)  
> **المشروع:** AQL / AQLORA Enterprise AI Platform  
> **الحالة الأولية:** Architecturally Accepted in Principle — Foundation Not Yet Fully Canonicalized  
> **الغرض:** تحديد ما أصبح Canonical وما بقي Candidate وما يجب توثيقه قبل التنفيذ  
> **قاعدة السلطة:** المواصفات والعقود المعتمدة تتقدم على كود Rocket التجريبي  
> **قاعدة التنفيذ:** لا إعادة تصميم ولا تعديل Repo قبل دراسة Claude واعتماد المالك

---

## 1. ملخص تنفيذي

الفهم الحالي أن Rocket هو مسار بناء واجهة AQL النهائية، وأن الواجهة الأساسية المستهدفة تعتمد Next.js client-only، بينما FastAPI والخادم يظلان مصدر منطق الأعمال والصلاحيات. Open WebUI جسر مؤقت قابل للإزالة، وليس الواجهة النهائية ولا مصدر حقيقة وظيفي. توجد UI Governance وScreen Governance وComponent States وعقود أولية، ويوجد مستودع Rocket يحتوي Candidate Components وشاشات قابلة للاستخراج.

المشكلة ليست غياب التصميم، بل عدم ثبوت أن الـFoundation أصبح كاملاً وقانونياً بما يسمح لـCoding Agent بتنفيذ شاشة جديدة من المستودع وحده، دون الرجوع إلى صور أو ذاكرة محادثات ودون اختراع أسماء أو Actions أو Routes.

المطلوب من Claude:

- فحص actual `HEAD` في مستودع المواصفات ومستودع Rocket ومستودع المنصة.
- مقارنة الوثائق بالكود الفعلي.
- تصنيف كل أصل: Canonical / Code-only / Spec-only / Proposed / Obsolete.
- تحديد الحد الأدنى لإغلاق Foundation Gate.
- توضيح خطة إزالة Open WebUI وشروطها.
- عدم إعادة تصميم الواجهة أو فرض Figma.

---

## 2. نية المنتج

نريد واجهة AQL:

- مؤسسية ومحايدة.
- عربية/إنجليزية.
- RTL/LTR.
- Light/Dark.
- Responsive للهاتف والكمبيوتر.
- Offline/Air-Gapped.
- قابلة للصيانة والتوسع.
- موحدة عبر الشاشات.
- مبنية بمكونات Canonical.
- لا تعتمد على أصول خارجية وقت التشغيل.
- لا تخزن أسراراً في العميل.
- لا تنفذ الصلاحيات في UI فقط.
- قادرة على استبدال Open WebUI دون تغيير AI/RAG runtimes.
- تسمح لـRocket بحرية UX في التفاصيل غير الوظيفية.

---

## 3. طبقات الحقيقة المطلوبة

على Claude فحص واعتماد فصل واضح بين:

| الطبقة | مسؤوليتها |
|---|---|
| Constitution | القواعد الثابتة العابرة للمراحل وحدود السلطة |
| ADRs | القرارات التقنية الكبيرة والبدائل والأسباب |
| UI Governance | المبادئ، Tokens، Accessibility، Responsive، States |
| Screen/Route/Action Contracts | حقيقة كل شاشة وسلوكها وعلاقاتها |
| Rocket Repository | Design/Implementation Candidate |
| Feature Package | سياق محدود لدفعة تنفيذ |
| Code/Tests | دليل التنفيذ الفعلي |
| Handoff/Receipt | ما تم وما لم يتم والأدلة |

Rocket لا يصبح Source of Truth لمجرد أن الشاشة أفضل بصرياً، والمواصفات لا يجب أن تتحول إلى وصف Pixel-by-Pixel يقتل حرية التصميم.

---

## 4. القرارات التي نعتقد أنها محسومة — تحتاج تحققاً

1. Primary UI Client هو Next.js client-only.
2. Rocket مسار توليد/تحسين الواجهة.
3. FastAPI والخادم مصدر منطق الأعمال.
4. Supabase ممنوع.
5. لا External Runtime Assets.
6. Open WebUI مؤقت ومعزول.
7. Route Registry أفضل من مسارات مبعثرة، إن كان قد اعتمد.
8. Design Tokens بدل قيم اعتباطية.
9. Fonts محلية.
10. العمل عبر Pull Requests، وعدم دفع Rocket مباشرة إلى `main`.
11. Feature Package وFeature Handoff جزء من التشغيل.
12. Rocket يقترح UX لكنه لا يخترع Contracts.
13. Figma اختياري للتنقيح وليس Source of Truth إلزامياً.
14. Permission enforcement وAudit في الخادم.

على Claude تصنيف كل بند: Accepted / Proposed / Code-only / Spec-only / Superseded.

---

## 5. نطاق UI Foundation المطلوب تقييمه

### 5.1 Design Foundations

- Brand primitives.
- Typography.
- Font loading.
- Spacing scale.
- Radius.
- Elevation.
- Color roles.
- Light/Dark themes.
- Accent policy.
- Motion policy.
- Icon policy.
- Density.
- Breakpoints.
- RTL mirroring rules.
- Focus indicators.
- Content width.
- Data density for enterprise tables.

### 5.2 Component Foundations

- Button.
- Input.
- Textarea.
- Select/Combobox.
- Checkbox/Switch/Radio.
- Date/Time.
- Card.
- Table/Data Grid.
- Form and validation.
- Dialog/Drawer/Popover.
- Toast/Alert/Banner.
- Tabs.
- Breadcrumb.
- Sidebar/Topbar.
- Search/filter/pagination.
- Empty/Loading/Error/Forbidden/Read-only states.
- Permission-aware action presentation.
- Evidence/Citation component.
- Status badges.
- Record reference/LinkedRecord.
- Audit timeline.
- Workflow step/state components.
- File/attachment presentation.
- Offline/degraded status.

لا نفرض أن يكون لكل عنصر ملف منفصل؛ المطلوب معرفة الحد الأدنى القابل للاختبار.

### 5.3 Behavioral Foundations

- Keyboard navigation.
- Focus management.
- Form validation.
- Async loading.
- Optimistic update policy.
- Confirmation for side effects.
- Unsaved changes.
- Session expiry.
- Unauthorized vs Forbidden.
- Sensitive field masking.
- Long Arabic content.
- Mobile adaptations.
- Retry and degraded behavior.
- Error correlation/reference.
- Read-only and disabled semantics.

### 5.4 Governance Foundations

- Naming.
- Component ownership.
- Proposed → Candidate → Approved lifecycle.
- Dependency allowlist.
- CI/lint/type/test gates.
- Accessibility tests.
- Offline asset checks.
- License checks.
- Design-to-code traceability.
- Versioning and changelog.

---

## 6. Core UI Foundation Candidate في Rocket

تقارير سابقة وصفت مستودع `aql` بأنه يحتوي على:

- Next.js وReact وTailwind.
- Zustand وZod وReact Flow وTanStack.
- Routes مثل Record List وRecord Type Builder وWorkflow Canvas وAction Registry وUI Showcase.
- Route Registry مستخدم في الكود.
- نقص محتمل في CI والاختبارات وLICENSE وi18n.
- فرع `rocket-update` وPR غير مدموج وقت التقرير.

هذه ليست حقائق حالية مضمونة. Claude يجب أن:

1. يفحص branches وHEAD وPRs.
2. يبني Inventory للمكونات والTokens والRoutes.
3. يقيس إعادة الاستخدام.
4. يكتشف Hard-coded values والنصوص.
5. يفحص External assets وSecrets.
6. يفحص Dependencies وLicenses.
7. يقارن code مع contracts.
8. يحدد ما يقبل وما يحتاج refactor وما يرفض.
9. يتحقق من عدم وجود Backend logic داخل UI.
10. يحدد ما إذا كان UI Showcase صالحاً كمرجع داخلي.

---

## 7. Canonicalization لا تعني نسخ الكود إلى Specs

نريد تصنيفاً واضحاً:

- **Rule/Decision:** يوثق في Constitution أو ADR أو Governance.
- **Contract:** يوثق السلوك والغرض والحقول والإجراءات والحالات.
- **Token Catalogue:** قد يكون مصدره code أو structured file أو generated artifact.
- **Component API:** قد يحتاج توثيقاً داخل repo التنفيذي.
- **Implementation Detail:** يبقى في الكود.
- **Visual Example:** مرجع بصري لا قانون وظيفي.
- **Candidate:** لا يصبح معتمداً قبل Gate.
- **Historical Artifact:** لا يقرأه Agent افتراضياً.

يجب منع تضخم المواصفات بنسخ JSX/CSS أو تفاصيل تتغير مع كل Refactor.

---

## 8. حرية Rocket وحدودها

### Rocket حر في

- ترتيب بصري لا يغير العقد.
- تجميع Actions في Menu.
- اختيار Layout ضمن Tokens وResponsive وAccessibility.
- تحسين Hierarchy والفراغات.
- اقتراح Component Composition.
- تحسين UX للحالات الفارغة والأخطاء.
- دمج أزرار متشابهة إذا بقيت Actions واضحة ومسموحاً بها.

### Rocket غير حر في

- تغيير Business Rule.
- إضافة Action أو Field أو Route غير معتمد.
- تجاوز Permission.
- إضافة خدمة خارجية.
- تخزين Secrets.
- تغيير Identity semantics.
- تحويل Mock إلى سلوك Production ظاهري.
- دفع مباشر إلى Main خارج السياسة.
- تغيير Contract IDs أو API endpoints من عنده.
- إضافة Dependency غير مسموح.

Claude يقرر كيف توثق هذه الحدود دون تقييد الإبداع البصري.

---

## 9. Foundation Gate

السؤال الحاسم:

> هل يستطيع Coding Agent، اعتماداً على Specs وFeature Package فقط، تنفيذ شاشة AQL جديدة متسقة ومتصلة بالعقود دون صور أو ذاكرة محادثات أو اختراع أسماء؟

محاور البوابة:

1. Tokens كافية.
2. Component states واضحة.
3. Screen Contract Template كافٍ.
4. Route/Action/Permission Contracts متاحة.
5. Responsive/RTL/Accessibility موثقة.
6. Dependency policy واضحة.
7. Code organization واضحة.
8. Mock/Real API boundaries واضحة.
9. Foundation components موجودة أو خطة اعتمادها واضحة.
10. CI/Test gates موجودة.
11. Rocket Operating Model واضح.
12. Traceability بين Spec وCode.
13. Error/Loading/Forbidden/Read-only states موحدة.
14. Offline asset verification موجود.
15. Security and secret guards موجودة.

إذا كانت الإجابة «لا»، يجب أن يحدد Claude **أقل مجموعة أعمال** لسد الفجوة قبل FP-0001.

---

## 10. الشاشات العينة لاختبار Foundation

يجب فحص قدرة الـFoundation على تمثيل شاشات مختلفة ومعقدة:

- Workflow Builder.
- Declarative Agent Builder.
- Dynamic Screen/Record Type Builder.
- Integrations/Connectors.
- Chat/AI Workspace.
- Record List/Profile.
- Action Registry.
- UI Showcase.

لا نطلب تنفيذها. يمكن لـClaude اختيار عينتين أو ثلاثاً كاختبار Representative.

---

## 11. UI Design Constitution التاريخي

توجد وثيقة UI Constitution تاريخية تحتوي مبادئ مفيدة، لكن بعض نسخها قد تشير إلى React/Vite أو قواعد مطلقة لم تعد مناسبة.

المطلوب:

- مقارنة المبادئ مع ADR الحالي.
- حفظ القواعد المستقرة: Brand، Tokens، Accessibility، RTL، Responsive، Offline.
- فصل Brand عن Frontend Engineering إذا لزم.
- إزالة أو Supersede إشارات Stack قديمة.
- عدم وصف 44×44 بأنه شرط WCAG عالمي إن لم يكن كذلك.
- السماح باستثناءات موثقة للـInline Computed Styles عند React Flow أو التموضع الديناميكي.
- عدم فرض منع CSS داخل Screens بصورة مطلقة؛ الممنوع هو القيم الاعتباطية والهوية الخاصة بكل شاشة.
- تحديد Version Canonical واحدة.
- تحديد ما ينتقل إلى Code Standards وما يبقى Design Governance.

---

## 12. Open WebUI — الجسر المؤقت

الفهم الحالي:

- ليس الواجهة النهائية.
- معزول عن Domain Logic.
- لا يعرض API keys للمستخدم.
- يعتمد هوية/جلسة محكومة من المنصة وفق التصميم.
- Actions الحساسة تمر Server-side مع Confirmation.
- له Decommission Plan.
- توجد أو يفترض وجود اختبارات Replacement/Isolation/Upgrade.
- Multi-user/session/identity/license/scale لم تثبت تشغيلياً بعد.

المطلوب من Claude:

1. فحص ADR والخطة الحالية.
2. تحديد Exit Criteria قابلة للقياس.
3. تحديد الوظائف التي يجب أن توفرها AQL UI قبل الإزالة.
4. منع تسرب Contracts خاصة بـOpen WebUI إلى Domain.
5. تحديد Scale/Identity/License checks قبل أول تفعيل.
6. عدم تشغيل أو دمج Open WebUI في هذه الجولة.

### أمثلة Exit Criteria

- Chat workspace في AQL يغطي الاستخدامات المطلوبة.
- SSO/session يعمل.
- Evidence presentation يعمل.
- Approved actions تعمل عبر server-side bridge.
- Conversation history أو بديلها يعمل وفق السياسة.
- Export/attachments المطلوبة متاحة.
- No user-visible keys.
- Audit مكتمل.
- Replacement test ناجح.
- بيانات قابلة للنقل أو التصدير.

Claude يقرر القائمة النهائية.

---

## 13. i18n وRTL

على المراجعة تحديد:

- هل النصوص Hard-coded أم عبر translation catalog؟
- Direction per locale.
- Mirroring rules.
- عدم قلب الأيقونات ذات المعنى غير الاتجاهي.
- Arabic typography.
- Pluralization and numbers.
- Date/time locale.
- LTR content داخل RTL مثل IDs وEmails.
- Table behavior.
- Mobile navigation.
- Bidirectional testing.

لا يكفي أن تبدو الشاشة عربية في لقطة واحدة.

---

## 14. Accessibility

يجب التحقق من:

- Semantic HTML.
- Keyboard access.
- Focus order.
- Visible focus.
- Labels and descriptions.
- Error association.
- Dialog focus trapping.
- Contrast.
- Reduced motion.
- Screen reader announcements.
- Data table semantics.
- Accessible canvas alternatives.
- Touch target policy المعقولة.

Claude يحدد ما يدخل Governance وما يدخل Tests.

---

## 15. Offline/Air-Gapped UI

المراجعة يجب أن تفحص:

- Fonts محلية.
- Icons محلية أو bundled.
- لا CDN.
- لا telemetry خارجية.
- لا remote images.
- لا runtime package fetch.
- Build reproducibility.
- License manifests.
- Offline install cache.
- Failure behavior عند عدم توفر خدمة داخلية.
- تحديث الواجهة من bundle محكومة.

---

## 16. الحالة المتوقعة داخل المستودع — تحتاج إثباتاً

مواد التنفيذ تشير إلى وجود:

- ADR للواجهة الأساسية.
- ADR/Open WebUI update وخطط إزالة.
- UI Screen Governance.
- Component States.
- Screen Inventory.
- Screen Contract Template وبذور.
- Rocket Operating Model.
- Contracts Standard.
- Traceability Seed.
- UI Candidate Repo.

الفجوة المحتملة هي **عدم اكتمال Canonicalization والدليل التنفيذي**، لا غياب كل شيء.

---

## 17. الفجوات المحتملة — قائمة فحص

- Canonical Token Source.
- Approved Component Inventory.
- Component API/State docs.
- i18n/RTL architecture.
- CI and tests.
- Dependency/license checks.
- Asset offline verification.
- Story/Showcase أو بديل.
- Screen-to-Route-to-Action traceability.
- API client boundary.
- Auth/session handling.
- Permission-aware UI contract.
- Evidence display standard.
- Responsive complex builders.
- Open WebUI exit checklist.
- Superseding obsolete UI Constitution.
- Owner/version لكل UI artifact.
- Candidate promotion process.
- Proof of consistent new-screen delivery.
- Error taxonomy.
- Accessibility acceptance tests.
- Mobile behavior.

---

## 18. الأسئلة المعمارية المفتوحة

1. أين تعيش Tokens: Specs أم Code أم Generated Artifact؟
2. هل Component Library داخل repo نفسه أم Package داخلي؟
3. ما الحد الأدنى من Design Documentation داخل Specs؟
4. هل UI Showcase Production أم Dev-only؟
5. كيف يقاس Foundation Gate؟
6. من يملك Canonicalization؟
7. هل Open WebUI يحتاج Compatibility Contract؟
8. ما شروط الإزالة الدقيقة؟
9. كيف تمنع Rocket من إعادة تعريف Components؟
10. كيف تدار Bilingual Copy؟
11. ما قواعد Mobile للCanvas/Builders؟
12. هل Visual Regression ضروري الآن؟
13. ما الذي يجب إغلاقه قبل FP-0001؟
14. هل توجد Dependencies أو Licenses يجب رفضها؟
15. كيف تدار Generated Code ownership؟

---

## 19. خارج النطاق

- إعادة تصميم الواجهة.
- كتابة كود.
- دمج PR.
- فرض Figma.
- بناء كل الشاشات.
- تفعيل Open WebUI.
- فرض Exact Layout.
- نقل CSS إلى Specs.
- اعتماد Rocket repo بالكامل دفعة واحدة.

---

## 20. المطلوب من Claude Architecture

1. UI Foundation Coverage Report.
2. Design-to-Code Traceability Matrix.
3. Canonical / Code-only / Spec-only / Proposed / Obsolete Inventory.
4. Foundation Gate Verdict.
5. Minimal Canonicalization Plan.
6. Open WebUI Exit Readiness Matrix.
7. UI Constitution Reconciliation.
8. Repository Impact Map.
9. Owner Decisions.
10. Current / Prepare Now / Later split.
11. التوقف دون تعديل.
12. بعد الاعتماد فقط: Prompt لـClaude Code لتوثيق واعتماد التغييرات.

---

## 21. شكل مخرجات Claude

1. Executive Verdict.
2. Repository Evidence Baseline.
3. UI Coverage Matrix.
4. Design-to-Code Matrix.
5. Foundation Gate Result.
6. Open WebUI Exit Analysis.
7. Options and Trade-offs.
8. Recommended Minimal Delta.
9. Owner Decisions.
10. Deferred Items.
11. Acceptance Criteria.
12. Proposed Claude Code Prompt.
13. Stop Statement.

---

## 22. ما لا نريده

- لا اعتبار Rocket Source of Truth تلقائياً.
- لا تقييد Rocket بتفاصيل بصرية غير وظيفية.
- لا اعتماد وثيقة UI قديمة دون مقارنة.
- لا تنفيذ شاشة جديدة قبل إغلاق الحد الأدنى.
- لا نقل Implementation Details إلى الدستور.
- لا تشغيل Open WebUI.
- لا تعديل مستودع أثناء الدراسة.

---

## 23. معايير قبول المراجعة

تُرفض إذا:

- لم تفحص الكود الفعلي.
- لم تفرق بين UI Rule وImplementation Detail.
- أعلنت Foundation جاهزاً بلا اختبار.
- تجاهلت Open WebUI Exit.
- لم تعالج RTL/Accessibility/Offline.
- لم تحافظ على حرية Rocket ضمن العقود.
- لم تحدد Canonical Owner لكل أصل.
