# RAW-EXTRACTION-REGISTER — B1 (المرحلة 1: الاستخراج الخام)

> **مخرج traceability/تحليلي غير حاكم** — ليس داخل authority ladder، ليس مصدراً حاكماً مستقلاً، ولا ينشئ سلطة موازية، ولا يُعدّ بديلاً عن الأصل الحاكم الذي يستشهد به. مرحلة pipeline: **الاستخراج الخام** (P3 B1 §7). لا تصنيف §10.4 هنا.
> **الموضع:** `traceability/rar-reconciliation/RAW-EXTRACTION-REGISTER.md` · **المدخل:** `references/analysis-inputs/rar-2026-07/RAR-00X-*.md` (أقسام §11/§12/§14 حصراً).

## قاعدة العدّ (مطبّقة على كل بند)
كل **عنصر قائمة منفصل** (نقطة `-` أو بند مرقّم `N.`) داخل §11/§12/§14 يُعدّ **بنداً خاماً مستقلاً واحداً**. تُستثنى (سياق لا بنود): جُمل التمهيد (مثل «على المراجعة معالجة:») · جُمل توجيه المراجعة (مثل «على Claude تقرير هل هذه Workflow عادية أم Capability») · كتل الكود/المخططات (lifecycle diagram · chain block). أُعيد اشتقاق العدد بهذه القاعدة وطابق المرجع 257 لكل قسم ولكل ملف (التفصيل في §C من تقرير B1). **حالة pipeline** لكل بند: `EXTRACTED` (يُحمل إلى التطبيع في `NORMALIZATION-AND-ATOMIC-MAP.md`).

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

> **[تصحيح 2026-07-25]** أُفرِدت بنود RAR-004..007 الـ132 إلى سجلات بندية مستقلة (معرف فريد · سطر مصدر خاص · نص). حُذفت صفوف النطاق ونقاط الحذف من المعرّفات الحاكمة. سجلات RAR-001..003 (أعلاه) لم تُمس.

## RAR-004 — Governed Extension Store  (37: §11=17 · §12=11 · §14=9) — [ممثلوها يؤجَّلون إلى B2 ما لم تنقلهم قاعدة أدنى RAR]
### §11 — Upgrade/Rollback/Compatibility
| RAW-ID | سطر | النص الخام |
|---|---|---|
| RAW-RAR004-S11-001 | :271 | Version policy |
| RAW-RAR004-S11-002 | :272 | Platform/API/spec compatibility |
| RAW-RAR004-S11-003 | :273 | Database migrations |
| RAW-RAR004-S11-004 | :274 | Maintenance windows |
| RAW-RAR004-S11-005 | :275 | Backup before upgrade |
| RAW-RAR004-S11-006 | :276 | Dependency conflicts |
| RAW-RAR004-S11-007 | :277 | Downgrade restrictions |
| RAW-RAR004-S11-008 | :278 | Configuration migration |
| RAW-RAR004-S11-009 | :279 | Data ownership at uninstall |
| RAW-RAR004-S11-010 | :280 | Rollback evidence |
| RAW-RAR004-S11-011 | :281 | Orphaned workflows/actions |
| RAW-RAR004-S11-012 | :282 | Impact preview before disable/remove |
| RAW-RAR004-S11-013 | :283 | Pinning |
| RAW-RAR004-S11-014 | :284 | LTS channels |
| RAW-RAR004-S11-015 | :285 | End-of-support |
| RAW-RAR004-S11-016 | :286 | Partial failure |
| RAW-RAR004-S11-017 | :287 | Compatibility tests |
### §12 — Impact Analysis
| RAW-RAR004-S12-001 | :297 | Workflows |
| RAW-RAR004-S12-002 | :298 | Agents |
| RAW-RAR004-S12-003 | :299 | Actions |
| RAW-RAR004-S12-004 | :300 | Schedules |
| RAW-RAR004-S12-005 | :301 | Connectors |
| RAW-RAR004-S12-006 | :302 | Screens |
| RAW-RAR004-S12-007 | :303 | Reports |
| RAW-RAR004-S12-008 | :304 | Data ingestion jobs |
| RAW-RAR004-S12-009 | :305 | Permissions |
| RAW-RAR004-S12-010 | :306 | Stored configuration |
| RAW-RAR004-S12-011 | :307 | Active runs |
### §14 — Code Execution Boundaries
| RAW-RAR004-S14-001 | :332 | هل يعمل داخل Process؟ |
| RAW-RAR004-S14-002 | :333 | داخل Container مستقل؟ |
| RAW-RAR004-S14-003 | :334 | كخدمة خارجية داخل LAN؟ |
| RAW-RAR004-S14-004 | :335 | كConfiguration فقط؟ |
| RAW-RAR004-S14-005 | :336 | ما Network/File/System access؟ |
| RAW-RAR004-S14-006 | :337 | ما Resource limits؟ |
| RAW-RAR004-S14-007 | :338 | كيف تسجل Calls؟ |
| RAW-RAR004-S14-008 | :339 | كيف تمنع package من تجاوز صلاحياتها؟ |
| RAW-RAR004-S14-009 | :340 | كيف يختلف ذلك حسب Package Type؟ |

## RAR-005 — Workflow Decision Model  (38: §11=14 · §12=17 · §14=7) — [ممثلوها يؤجَّلون إلى B2 ما لم تنقلهم قاعدة أدنى RAR]
### §11 — Delegation/Acting on Behalf Of
| RAW-ID | سطر | النص الخام |
|---|---|---|
| RAW-RAR005-S11-001 | :269 | تفويض مؤقت خلال إجازة |
| RAW-RAR005-S11-002 | :270 | تفويض لمهمة محددة |
| RAW-RAR005-S11-003 | :271 | تفويض لنوع Workflow |
| RAW-RAR005-S11-004 | :272 | تفويض لدور |
| RAW-RAR005-S11-005 | :273 | No further delegation |
| RAW-RAR005-S11-006 | :274 | Delegation requiring approval |
| RAW-RAR005-S11-007 | :275 | Expiration |
| RAW-RAR005-S11-008 | :276 | Revocation |
| RAW-RAR005-S11-009 | :277 | Conflict of interest exclusion |
| RAW-RAR005-S11-010 | :281 | Reassignment: نقل المسؤولية |
| RAW-RAR005-S11-011 | :282 | Delegation: منح صلاحية مؤقتة |
| RAW-RAR005-S11-012 | :283 | Proxy decision: قرار بالنيابة |
| RAW-RAR005-S11-013 | :284 | Acting role: تولي دور رسمي مؤقتاً |
| RAW-RAR005-S11-014 | :285 | Queue claim: استلام عنصر من قائمة |
### §12 — Escalation/SLA
| RAW-RAR005-S12-001 | :295 | Reminder |
| RAW-RAR005-S12-002 | :296 | Notify manager |
| RAW-RAR005-S12-003 | :297 | Add alternate assignee |
| RAW-RAR005-S12-004 | :298 | Reassign |
| RAW-RAR005-S12-005 | :299 | Mark overdue |
| RAW-RAR005-S12-006 | :300 | Trigger path |
| RAW-RAR005-S12-007 | :301 | Pause بسبب Dependency |
| RAW-RAR005-S12-008 | :302 | Escalate priority |
| RAW-RAR005-S12-009 | :303 | Open incident/task |
| RAW-RAR005-S12-010 | :307 | Business calendar |
| RAW-RAR005-S12-011 | :308 | Timezone |
| RAW-RAR005-S12-012 | :309 | Pause/resume |
| RAW-RAR005-S12-013 | :310 | Holidays |
| RAW-RAR005-S12-014 | :311 | Dependency waiting |
| RAW-RAR005-S12-015 | :312 | Retry limits |
| RAW-RAR005-S12-016 | :313 | Who can change SLA |
| RAW-RAR005-S12-017 | :314 | Audit of manual override |
### §14 — Override/إعادة الفتح
| RAW-RAR005-S14-001 | :339 | منع كامل في MVP |
| RAW-RAR005-S14-002 | :340 | Reopen بصلاحية عالية وسبب إلزامي |
| RAW-RAR005-S14-003 | :341 | New Step Run بدلاً من تعديل القديم |
| RAW-RAR005-S14-004 | :342 | Reversal Event يحفظ القرار السابق |
| RAW-RAR005-S14-005 | :343 | Compensation للأفعال المنفذة |
| RAW-RAR005-S14-006 | :344 | إشعار الأطراف |
| RAW-RAR005-S14-007 | :345 | أثر على الخطوات اللاحقة |

## RAR-006 — Real-time AI Readiness  (27: §11=8 · §12=8 · §14=11) — [ممثلوها يؤجَّلون إلى B2 ما لم تنقلهم قاعدة أدنى RAR]
### §11 — Human in the Loop
| RAW-ID | سطر | النص الخام |
|---|---|---|
| RAW-RAR006-S11-001 | :262 | View only |
| RAW-RAR006-S11-002 | :263 | Acknowledge |
| RAW-RAR006-S11-003 | :264 | Accept/Reject recommendation |
| RAW-RAR006-S11-004 | :265 | Edit before action |
| RAW-RAR006-S11-005 | :266 | Approval workflow |
| RAW-RAR006-S11-006 | :267 | Two-person rule |
| RAW-RAR006-S11-007 | :268 | Auto-action within safe threshold |
| RAW-RAR006-S11-008 | :269 | Rollback/compensation |
### §12 — مصادر Ingestion المحتملة
| RAW-RAR006-S12-001 | :277 | Connector polling |
| RAW-RAR006-S12-002 | :278 | Webhook داخل الشبكة |
| RAW-RAR006-S12-003 | :279 | File drops |
| RAW-RAR006-S12-004 | :280 | Manual event |
| RAW-RAR006-S12-005 | :281 | Internal domain events |
| RAW-RAR006-S12-006 | :282 | Message bus لاحقاً |
| RAW-RAR006-S12-007 | :283 | Database CDC لاحقاً |
| RAW-RAR006-S12-008 | :284 | Device/IoT gateway لاحقاً |
### §14 — Ordering/Replay
| RAW-RAR006-S14-001 | :312 | [Ordering] هل الترتيب per source أم per subject؟ |
| RAW-RAR006-S14-002 | :313 | [Ordering] ماذا يحدث عند Out-of-order Event؟ |
| RAW-RAR006-S14-003 | :314 | [Ordering] هل يوجد Sequence Number؟ |
| RAW-RAR006-S14-004 | :315 | [Ordering] كيف تعرض Live View بيانات متأخرة؟ |
| RAW-RAR006-S14-005 | :319 | [Replay] لماذا يعاد التشغيل؟ |
| RAW-RAR006-S14-006 | :320 | [Replay] من يملك الصلاحية؟ |
| RAW-RAR006-S14-007 | :321 | [Replay] ما النطاق الزمني؟ |
| RAW-RAR006-S14-008 | :322 | [Replay] كيف تمنع Side Effects المكررة؟ |
| RAW-RAR006-S14-009 | :323 | [Replay] هل AI Inference يعاد؟ |
| RAW-RAR006-S14-010 | :324 | [Replay] كيف تميز Replay عن Live Processing؟ |
| RAW-RAR006-S14-011 | :325 | [Replay] كيف تسجل Audit؟ |

## RAR-007 — Strategic Capability Backlog  (30: §11=2 · §12=14 · §14=14) — [ممثلوها يؤجَّلون إلى B2 ما لم تنقلهم قاعدة أدنى RAR]
### §11 — الفرق بين Future Capability وDeferred Implementation
| RAW-ID | سطر | النص الخام |
|---|---|---|
| RAW-RAR007-S11-001 | :302 | Future Capability: اتجاه منتج معتمد أو مرشح قد لا يكون تنفيذه مقرراً |
| RAW-RAR007-S11-002 | :303 | Deferred Implementation: تنفيذ قدرة/جزء معتمد مؤجل بترتيب/اعتماديات |
### §12 — مكان السجل داخل المستودع (فحص 9 · قرار 5)
| RAW-RAR007-S12-001 | :313 | فحص: `decisions/DEFERRED_IMPLEMENTATION.md` |
| RAW-RAR007-S12-002 | :314 | فحص: `decisions/open-decisions.md` |
| RAW-RAR007-S12-003 | :315 | فحص: `decisions/adr/` |
| RAW-RAR007-S12-004 | :316 | فحص: `phases/` أو `roadmap/` |
| RAW-RAR007-S12-005 | :317 | فحص: `knowledge/` |
| RAW-RAR007-S12-006 | :318 | فحص: `traceability/` |
| RAW-RAR007-S12-007 | :319 | فحص: `INDEX.md` |
| RAW-RAR007-S12-008 | :320 | فحص: `AUTHORITY.md` |
| RAW-RAR007-S12-009 | :321 | فحص: أي Capability Catalogue قائم |
| RAW-RAR007-S12-010 | :325 | قرار: توسيع Deferred Register |
| RAW-RAR007-S12-011 | :326 | قرار: إنشاء Strategic Registry مستقل |
| RAW-RAR007-S12-012 | :327 | قرار: Idea Inbox خارج Tier-0 |
| RAW-RAR007-S12-013 | :328 | قرار: استخدام Structured Source مع Markdown مولد |
| RAW-RAR007-S12-014 | :329 | قرار: دمج بعض السجلات |
### §14 — العلاقة مع توليد وثائق المشروع
| RAW-RAR007-S14-001 | :371 | BRD |
| RAW-RAR007-S14-002 | :372 | FRD |
| RAW-RAR007-S14-003 | :373 | SRS |
| RAW-RAR007-S14-004 | :374 | SDS / Architecture Description |
| RAW-RAR007-S14-005 | :375 | Data Dictionary |
| RAW-RAR007-S14-006 | :376 | Screen Catalogue |
| RAW-RAR007-S14-007 | :377 | Workflow Catalogue |
| RAW-RAR007-S14-008 | :378 | Permission Matrix |
| RAW-RAR007-S14-009 | :379 | API Documentation |
| RAW-RAR007-S14-010 | :380 | User Guide |
| RAW-RAR007-S14-011 | :381 | Admin Guide |
| RAW-RAR007-S14-012 | :382 | Operations Guide |
| RAW-RAR007-S14-013 | :383 | Test Plan |
| RAW-RAR007-S14-014 | :384 | Release Documentation |

---
**الإجمالي الخام المُعاد اشتقاقه = 257** (46+33+46+37+38+27+30) — مطابق للمرجع غير الحاكم. حالة الكل `EXTRACTED`. لا بند يتيم في هذه المرحلة (كلٌّ يُحمل إلى التطبيع). المصائر (INDEPENDENT/SPLIT/MERGED/OUT_OF_SCOPE) في `CANONICAL-ITEM-UNIVERSE.md`.
