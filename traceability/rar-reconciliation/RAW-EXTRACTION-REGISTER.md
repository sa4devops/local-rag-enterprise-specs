# RAW-EXTRACTION-REGISTER — B1 (المرحلة 1: الاستخراج الخام)

> **مخرج traceability/تحليلي غير حاكم** — ليس داخل authority ladder، ليس مصدراً حاكماً مستقلاً، ولا ينشئ سلطة موازية، ولا يُعدّ بديلاً عن الأصل الحاكم الذي يستشهد به. مرحلة pipeline: **الاستخراج الخام** (P3 B1 §7). لا تصنيف §10.4 هنا.
> **الموضع:** `traceability/rar-reconciliation/RAW-EXTRACTION-REGISTER.md` · **المدخل:** `references/analysis-inputs/rar-2026-07/RAR-00X-*.md` (أقسام §11/§12/§14 حصراً).

## قاعدة العدّ (مطبّقة على كل بند)
كل **عنصر قائمة منفصل** (نقطة `-` أو بند مرقّم `N.`) داخل §11/§12/§14 يُعدّ **بنداً خاماً مستقلاً واحداً**. تُستثنى (سياق لا بنود): جُمل التمهيد («على المراجعة معالجة:»…) · جُمل توجيه المراجعة («على Claude تقرير…») · كتل الكود/المخططات (lifecycle diagram · chain block). أُعيد اشتقاق العدد بهذه القاعدة وطابق المرجع 257 لكل قسم ولكل ملف (التفصيل في §C من تقرير B1). **حالة pipeline** لكل بند: `EXTRACTED` (يُحمل إلى التطبيع في `NORMALIZATION-REGISTER.md`).

---

## RAR-001 — Conversational Tasks & Automation  (46: §11=13 · §12=18 · §14=15)
### §11 — الحالة المتوقعة داخل المستودع — تحتاج إثباتاً
| RAW-ID | سطر | النص الخام |
|---|---|---|
| RAW-RAR001-S11-001 | :220 | وجود Business Glossary أولي للمصطلحات الأربعة |
| RAW-RAR001-S11-002 | :221 | وجود Workflow وAction وPermission وAudit foundations |
| RAW-RAR001-S11-003 | :222 | وجود Agent-assisted Workflow Builder كفكرة مرتبطة |
| RAW-RAR001-S11-004 | :223 | وضع التنفيذ الفعلي لـConversational Automation في مرحلة لاحقة |
| RAW-RAR001-S11-005 | :224 | توصية بتجهيز العقود الآن |
| RAW-RAR001-S11-006 | :228 | هل توجد Contracts للأنواع الأربعة؟ |
| RAW-RAR001-S11-007 | :229 | هل توجد Lifecycles رسمية؟ |
| RAW-RAR001-S11-008 | :230 | هل توجد API Operation Contracts؟ |
| RAW-RAR001-S11-009 | :231 | هل توجد Screen/Route Contracts لنقاط الدخول؟ |
| RAW-RAR001-S11-010 | :232 | هل توجد Permission Verbs واضحة؟ |
| RAW-RAR001-S11-011 | :233 | هل توجد Traceability إلى Phase واختبارات؟ |
| RAW-RAR001-S11-012 | :234 | هل توجد Deferred Entries؟ |
| RAW-RAR001-S11-013 | :235 | هل توجد تعارضات تسمية بين الوثائق؟ |
### §12 — الفجوات المحتملة — قائمة فحص لا حكم
| RAW-ID | سطر | النص الخام |
|---|---|---|
| RAW-RAR001-S12-001 | :241 | نموذج موارد موحد أو فصل واضح بين الأنواع |
| RAW-RAR001-S12-002 | :242 | Draft / Preview / Confirm semantics |
| RAW-RAR001-S12-003 | :243 | Intent Interpretation Contract |
| RAW-RAR001-S12-004 | :244 | Resolution Contract للأشخاص والسجلات والوحدات |
| RAW-RAR001-S12-005 | :245 | Ambiguity handling |
| RAW-RAR001-S12-006 | :246 | Permission evaluation في كل مرحلة |
| RAW-RAR001-S12-007 | :247 | Approval thresholds |
| RAW-RAR001-S12-008 | :248 | Recurrence/Timezone/Business Calendar |
| RAW-RAR001-S12-009 | :249 | Event Trigger abstraction |
| RAW-RAR001-S12-010 | :250 | Idempotency وإعادة المحاولة |
| RAW-RAR001-S12-011 | :251 | Versioning والتعديل والإلغاء |
| RAW-RAR001-S12-012 | :252 | Run history وExecution Evidence |
| RAW-RAR001-S12-013 | :253 | Notifications |
| RAW-RAR001-S12-014 | :254 | ربط Work Queue وInbox |
| RAW-RAR001-S12-015 | :255 | Audit Event Catalogue |
| RAW-RAR001-S12-016 | :256 | UI states: parsing/needs_input/preview_ready/approval_required/failed |
| RAW-RAR001-S12-017 | :257 | Acceptance tests لمنع تجاوز الصلاحيات وكشف البيانات |
| RAW-RAR001-S12-018 | :258 | Fallback عند عدم توفر LLM |
### §14 — الأسئلة المعمارية المفتوحة
| RAW-ID | سطر | النص الخام |
|---|---|---|
| RAW-RAR001-S14-001 | :286 | هل Task مورد مستقل أم تجسيد مبسط لـWorkflow؟ |
| RAW-RAR001-S14-002 | :287 | ما الحد بين Schedule وAutomation Trigger؟ |
| RAW-RAR001-S14-003 | :288 | أين تخزن صياغة المستخدم الأصلية؟ |
| RAW-RAR001-S14-004 | :289 | هل تحفظ خطة LLM الوسيطة؟ وكيف تمنع اعتبارها حقيقة؟ |
| RAW-RAR001-S14-005 | :290 | ما نموذج التحقق Deterministic؟ |
| RAW-RAR001-S14-006 | :291 | كيف تربط Preview بنسخة العقود التي تحققت عليها؟ |
| RAW-RAR001-S14-007 | :292 | هل كل تعديل ينتج Version جديداً؟ |
| RAW-RAR001-S14-008 | :293 | ما الذي يمكن نشره دون Admin؟ |
| RAW-RAR001-S14-009 | :294 | كيف تعالج Cross-Org Assignment؟ |
| RAW-RAR001-S14-010 | :295 | هل نحتاج Dry Run؟ |
| RAW-RAR001-S14-011 | :296 | ما الحد الأدنى المطلوب الآن إذا كان التنفيذ مؤجلاً؟ |
| RAW-RAR001-S14-012 | :297 | هل تحتاج ADR أم Contracts فقط؟ |
| RAW-RAR001-S14-013 | :298 | كيف تعمل عند عدم توفر LLM؟ |
| RAW-RAR001-S14-014 | :299 | كيف تمنع Prompt Injection من مستند أو سجل؟ |
| RAW-RAR001-S14-015 | :300 | كيف يمثل شرط «عندما يكتمل الجميع» بشكل قابل للاختبار؟ |

## RAR-002 — Declarative Agent Builder  (33: §11=8 · §12=6 · §14=19)
### §11 — طلب إنشاء Agent من الأدمن
| RAW-ID | سطر | النص الخام |
|---|---|---|
| RAW-RAR002-S11-001 | :331 | المستخدم يكتب الهدف |
| RAW-RAR002-S11-002 | :332 | يحدد المعرفة المطلوبة |
| RAW-RAR002-S11-003 | :333 | يحدد ما يود أن يفعله Agent |
| RAW-RAR002-S11-004 | :334 | النظام يحلل الطلب دون إنشاء فعلي |
| RAW-RAR002-S11-005 | :335 | يرسل Request إلى Admin/Approver |
| RAW-RAR002-S11-006 | :336 | الأدمن يراجع المخاطر والـSkills والSources |
| RAW-RAR002-S11-007 | :337 | يقبل أو يعدل أو يرفض مع السبب |
| RAW-RAR002-S11-008 | :338 | عند القبول ينشأ Draft مملوكاً وفق السياسة |
### §12 — دورة الحياة المحتملة (الحالات الجانبية؛ مخطط الحالات كتلة سياق غير معدودة)
| RAW-ID | سطر | النص الخام |
|---|---|---|
| RAW-RAR002-S12-001 | :358 | Dependency Missing |
| RAW-RAR002-S12-002 | :359 | Knowledge Updating |
| RAW-RAR002-S12-003 | :360 | Policy Conflict |
| RAW-RAR002-S12-004 | :361 | Degraded |
| RAW-RAR002-S12-005 | :362 | Revoked |
| RAW-RAR002-S12-006 | :363 | Pending Revalidation |
### §14 — الأمن والعزل
| RAW-ID | سطر | النص الخام |
|---|---|---|
| RAW-RAR002-S14-001 | :407 | Institution/Tenant isolation إن كان موجوداً |
| RAW-RAR002-S14-002 | :408 | Org-unit scoped administration |
| RAW-RAR002-S14-003 | :409 | Creator vs Runtime Principal |
| RAW-RAR002-S14-004 | :410 | Least privilege |
| RAW-RAR002-S14-005 | :411 | Connector scopes |
| RAW-RAR002-S14-006 | :412 | Row/Object/Field permissions |
| RAW-RAR002-S14-007 | :413 | Secret handling |
| RAW-RAR002-S14-008 | :414 | Prompt Injection from knowledge |
| RAW-RAR002-S14-009 | :415 | Tool output sanitization |
| RAW-RAR002-S14-010 | :416 | Data exfiltration prevention |
| RAW-RAR002-S14-011 | :417 | Outbound network restrictions |
| RAW-RAR002-S14-012 | :418 | File scanning/classification |
| RAW-RAR002-S14-013 | :419 | Audit and non-repudiation |
| RAW-RAR002-S14-014 | :420 | Rate/usage quotas |
| RAW-RAR002-S14-015 | :421 | Model/provider policy |
| RAW-RAR002-S14-016 | :422 | Session memory vs verified facts |
| RAW-RAR002-S14-017 | :423 | Test sandbox boundaries |
| RAW-RAR002-S14-018 | :424 | Sensitive output redaction |
| RAW-RAR002-S14-019 | :425 | Cross-agent data leakage |

## RAR-003 — UI Foundation & Rocket Canonicalization  (46: §11=9 · §12=24 · §14=13)
### §11 — UI Design Constitution التاريخي
| RAW-ID | سطر | النص الخام |
|---|---|---|
| RAW-RAR003-S11-001 | :298 | مقارنة المبادئ مع ADR الحالي |
| RAW-RAR003-S11-002 | :299 | حفظ القواعد المستقرة: Brand، Tokens، Accessibility، RTL، Responsive، Offline |
| RAW-RAR003-S11-003 | :300 | فصل Brand عن Frontend Engineering إذا لزم |
| RAW-RAR003-S11-004 | :301 | إزالة أو Supersede إشارات Stack قديمة |
| RAW-RAR003-S11-005 | :302 | عدم وصف 44×44 بأنه شرط WCAG عالمي إن لم يكن كذلك |
| RAW-RAR003-S11-006 | :303 | السماح باستثناءات موثقة للـInline Computed Styles عند React Flow أو التموضع الديناميكي |
| RAW-RAR003-S11-007 | :304 | عدم فرض منع CSS داخل Screens مطلقاً؛ الممنوع القيم الاعتباطية والهوية لكل شاشة |
| RAW-RAR003-S11-008 | :305 | تحديد Version Canonical واحدة |
| RAW-RAR003-S11-009 | :306 | تحديد ما ينتقل إلى Code Standards وما يبقى Design Governance |
### §12 — Open WebUI — الجسر المؤقت (الفهم الحالي 8 · المطلوب 6 · أمثلة Exit 10)
| RAW-ID | سطر | النص الخام |
|---|---|---|
| RAW-RAR003-S12-001 | :314 | [فهم] ليس الواجهة النهائية |
| RAW-RAR003-S12-002 | :315 | [فهم] معزول عن Domain Logic |
| RAW-RAR003-S12-003 | :316 | [فهم] لا يعرض API keys للمستخدم |
| RAW-RAR003-S12-004 | :317 | [فهم] يعتمد هوية/جلسة محكومة من المنصة وفق التصميم |
| RAW-RAR003-S12-005 | :318 | [فهم] Actions الحساسة تمر Server-side مع Confirmation |
| RAW-RAR003-S12-006 | :319 | [فهم] له Decommission Plan |
| RAW-RAR003-S12-007 | :320 | [فهم] توجد أو يفترض وجود اختبارات Replacement/Isolation/Upgrade |
| RAW-RAR003-S12-008 | :321 | [فهم] Multi-user/session/identity/license/scale لم تثبت تشغيلياً بعد |
| RAW-RAR003-S12-009 | :325 | [مطلوب] فحص ADR والخطة الحالية |
| RAW-RAR003-S12-010 | :326 | [مطلوب] تحديد Exit Criteria قابلة للقياس |
| RAW-RAR003-S12-011 | :327 | [مطلوب] تحديد الوظائف التي يجب أن توفرها AQL UI قبل الإزالة |
| RAW-RAR003-S12-012 | :328 | [مطلوب] منع تسرب Contracts خاصة بـOpen WebUI إلى Domain |
| RAW-RAR003-S12-013 | :329 | [مطلوب] تحديد Scale/Identity/License checks قبل أول تفعيل |
| RAW-RAR003-S12-014 | :330 | [مطلوب] عدم تشغيل أو دمج Open WebUI في هذه الجولة |
| RAW-RAR003-S12-015 | :334 | [Exit] Chat workspace في AQL يغطي الاستخدامات المطلوبة |
| RAW-RAR003-S12-016 | :335 | [Exit] SSO/session يعمل |
| RAW-RAR003-S12-017 | :336 | [Exit] Evidence presentation يعمل |
| RAW-RAR003-S12-018 | :337 | [Exit] Approved actions تعمل عبر server-side bridge |
| RAW-RAR003-S12-019 | :338 | [Exit] Conversation history أو بديلها يعمل وفق السياسة |
| RAW-RAR003-S12-020 | :339 | [Exit] Export/attachments المطلوبة متاحة |
| RAW-RAR003-S12-021 | :340 | [Exit] No user-visible keys |
| RAW-RAR003-S12-022 | :341 | [Exit] Audit مكتمل |
| RAW-RAR003-S12-023 | :342 | [Exit] Replacement test ناجح |
| RAW-RAR003-S12-024 | :343 | [Exit] بيانات قابلة للنقل أو التصدير |
### §14 — Accessibility
| RAW-ID | سطر | النص الخام |
|---|---|---|
| RAW-RAR003-S14-001 | :373 | Semantic HTML |
| RAW-RAR003-S14-002 | :374 | Keyboard access |
| RAW-RAR003-S14-003 | :375 | Focus order |
| RAW-RAR003-S14-004 | :376 | Visible focus |
| RAW-RAR003-S14-005 | :377 | Labels and descriptions |
| RAW-RAR003-S14-006 | :378 | Error association |
| RAW-RAR003-S14-007 | :379 | Dialog focus trapping |
| RAW-RAR003-S14-008 | :380 | Contrast |
| RAW-RAR003-S14-009 | :381 | Reduced motion |
| RAW-RAR003-S14-010 | :382 | Screen reader announcements |
| RAW-RAR003-S14-011 | :383 | Data table semantics |
| RAW-RAR003-S14-012 | :384 | Accessible canvas alternatives |
| RAW-RAR003-S14-013 | :385 | Touch target policy المعقولة |

## RAR-004 — Governed Extension Store  (37: §11=17 · §12=11 · §14=9) — [ممثلوها يؤجَّلون إلى B2]
### §11 — Upgrade/Rollback/Compatibility
| RAW-ID | سطر | النص الخام |
|---|---|---|
| RAW-RAR004-S11-001..017 | :271–:287 | Version policy · Platform/API/spec compatibility · Database migrations · Maintenance windows · Backup before upgrade · Dependency conflicts · Downgrade restrictions · Configuration migration · Data ownership at uninstall · Rollback evidence · Orphaned workflows/actions · Impact preview before disable/remove · Pinning · LTS channels · End-of-support · Partial failure · Compatibility tests |
### §12 — Impact Analysis
| RAW-RAR004-S12-001..011 | :297–:307 | Workflows · Agents · Actions · Schedules · Connectors · Screens · Reports · Data ingestion jobs · Permissions · Stored configuration · Active runs |
### §14 — Code Execution Boundaries
| RAW-RAR004-S14-001..009 | :332–:340 | هل يعمل داخل Process؟ · داخل Container مستقل؟ · كخدمة خارجية داخل LAN؟ · كConfiguration فقط؟ · ما Network/File/System access؟ · ما Resource limits؟ · كيف تسجل Calls؟ · كيف تمنع package من تجاوز صلاحياتها؟ · كيف يختلف حسب Package Type؟ |

## RAR-005 — Workflow Decision Model  (38: §11=14 · §12=17 · §14=7) — [ممثلوها يؤجَّلون إلى B2]
### §11 — Delegation/Acting on Behalf Of
| RAW-RAR005-S11-001..009 | :269–:277 | تفويض مؤقت خلال إجازة · تفويض لمهمة محددة · تفويض لنوع Workflow · تفويض لدور · No further delegation · Delegation requiring approval · Expiration · Revocation · Conflict of interest exclusion |
| RAW-RAR005-S11-010..014 | :281–:285 | Reassignment · Delegation · Proxy decision · Acting role · Queue claim (تعريفات مفرّقة) |
### §12 — Escalation/SLA
| RAW-RAR005-S12-001..009 | :295–:303 | Reminder · Notify manager · Add alternate assignee · Reassign · Mark overdue · Trigger path · Pause (Dependency) · Escalate priority · Open incident/task |
| RAW-RAR005-S12-010..017 | :307–:314 | Business calendar · Timezone · Pause/resume · Holidays · Dependency waiting · Retry limits · Who can change SLA · Audit of manual override |
### §14 — Override/إعادة الفتح
| RAW-RAR005-S14-001..007 | :339–:345 | منع كامل في MVP · Reopen بصلاحية عالية وسبب إلزامي · New Step Run بدلاً من تعديل القديم · Reversal Event يحفظ القرار السابق · Compensation للأفعال المنفذة · إشعار الأطراف · أثر على الخطوات اللاحقة |

## RAR-006 — Real-time AI Readiness  (27: §11=8 · §12=8 · §14=11) — [ممثلوها يؤجَّلون إلى B2]
### §11 — Human in the Loop
| RAW-RAR006-S11-001..008 | :262–:269 | View only · Acknowledge · Accept/Reject recommendation · Edit before action · Approval workflow · Two-person rule · Auto-action within safe threshold · Rollback/compensation |
### §12 — مصادر Ingestion المحتملة
| RAW-RAR006-S12-001..008 | :277–:284 | Connector polling · Webhook داخل الشبكة · File drops · Manual event · Internal domain events · Message bus لاحقاً · Database CDC لاحقاً · Device/IoT gateway لاحقاً |
### §14 — Ordering/Replay
| RAW-RAR006-S14-001..004 | :312–:315 | [Ordering] هل الترتيب per source أم per subject؟ · Out-of-order Event؟ · Sequence Number؟ · كيف تعرض Live View بيانات متأخرة؟ |
| RAW-RAR006-S14-005..011 | :319–:325 | [Replay] لماذا يعاد؟ · من يملك الصلاحية؟ · النطاق الزمني؟ · منع Side Effects المكررة؟ · هل AI Inference يعاد؟ · تمييز Replay عن Live؟ · تسجيل Audit؟ |

## RAR-007 — Strategic Capability Backlog  (30: §11=2 · §12=14 · §14=14) — [ممثلوها يؤجَّلون إلى B2]
### §11 — الفرق بين Future Capability وDeferred Implementation
| RAW-RAR007-S11-001 | :302 | Future Capability: اتجاه منتج معتمد أو مرشح قد لا يكون تنفيذه مقرراً |
| RAW-RAR007-S11-002 | :303 | Deferred Implementation: تنفيذ قدرة/جزء معتمد مؤجل بترتيب/اعتماديات |
### §12 — مكان السجل داخل المستودع (فحص 9 · قرار 5)
| RAW-RAR007-S12-001..009 | :313–:321 | فحص: DEFERRED_IMPLEMENTATION.md · open-decisions.md · adr/ · phases//roadmap/ · knowledge/ · traceability/ · INDEX.md · AUTHORITY.md · أي Capability Catalogue |
| RAW-RAR007-S12-010..014 | :325–:329 | قرار: توسيع Deferred Register · إنشاء Strategic Registry مستقل · Idea Inbox خارج Tier-0 · Structured Source مع Markdown مولد · دمج بعض السجلات |
### §14 — العلاقة مع توليد وثائق المشروع
| RAW-RAR007-S14-001..014 | :371–:384 | BRD · FRD · SRS · SDS/Architecture Description · Data Dictionary · Screen Catalogue · Workflow Catalogue · Permission Matrix · API Documentation · User Guide · Admin Guide · Operations Guide · Test Plan · Release Documentation |

---
**الإجمالي الخام المُعاد اشتقاقه = 257** (46+33+46+37+38+27+30) — مطابق للمرجع غير الحاكم. حالة الكل `EXTRACTED`. لا بند يتيم في هذه المرحلة (كلٌّ يُحمل إلى التطبيع). المصائر (INDEPENDENT/SPLIT/MERGED/OUT_OF_SCOPE) في `CANONICAL-ITEM-UNIVERSE.md`.
