# Phase 6 — Intelligence Layer: LLM Gateway (Full), Agents, SQL Agent, Chat &amp; Reports

الحالة: Accepted v0.3 (2026-07-06) — مدخل تصميم ما-قبل-الأساس (استُعيد 2026-07-10 ضمن إغلاق F-3). هذه الوثيقة هي تصميم المرحلة المعتمد تاريخياً والموطن التعريفي لمعرفات FR الخاصة بها. عند تفعيل المرحلة يُنتَج «تصميم التفعيل» النهائي وفق قاعدة phase-roadmap بادئاً من هذه الوثيقة؛ وكل ما استجد في حزم v0.4 حتى v1.0-architecture-baseline والـ ADRs يعلوها عند أي تعارض (سلسلة م20). لا تنفيذ مباشر من هذه الوثيقة دون بطاقة مهمة وتصميم تفعيل.

> **Version:** 1.0 — Proposed (Accepted باعتماد v0.3) · **Date:** 2026-07-06 · **Authority عند الاعتماد:** المرتبة 6
> **Inherits:** Common Phase Baseline — PHASE_MASTER_PLAN §4. **Predecessor:** Phase 5 بكامل DoD. بطاقات المهام عند التفعيل.
> **بوابات:** أوزان نماذج chat/reasoning عبر license-review (بوابة 1) قبل تشغيلها؛ لا بوابات بنية جديدة.

## 1. Purpose
بناء طبقة الاستدلال المسنود فوق المعرفة المحكومة: اكتمال **LLM Gateway** (chat/completions + اختيار نموذج **لكل وكيل** من الواجهة)، وكلاء (Retrieval موجود، + Reasoning + Report + Validation fail-closed + Orchestrator خفيف)، **module `chat`** للجلسات المؤسسية المسنودة، **SQL Agent آمن** قراءة-فقط، و**تقارير طويلة** قسماً قسماً بالاستشهاد — **اللLM ليس مصدر حقيقة في أي مسار**.

## 2. Scope
Gateway كامل: عقد OpenAI-compatible، توجيه per-capability وper-agent، fallback chains، مهل وحدود سياق/رموز، حصص أساسية · Registry UI موسّع: ربط **كل وكيل** بنموذج + معاملات (حرارة/سياق) + fallback، بتدقيق (واعتماد في الإنتاج حسب سياسة P4) · Agents: Reasoning (تحليل فوق مقاطع مسترجَعة فقط) · Report (تأليف مقيّد بالمصادر) · Validation (فحص إسناد/تنسيق/سياسة — **fail-closed**) · Orchestrator خفيف (تسلسل معلن retrieval→reason→validate) · **Chat module**: جلسات/رسائل/سياق، ربط بمشروع، كل إجابة أعمال **مسنودة أو رفض No-Guessing**، عرض الاستشهادات، أزرار أفعال آمنة (فتح سجل/مصدر) · **SQL Agent**: توليد SQL **قراءة فقط** على **views مولّدة من الميتاداتا ضمن allow-list** + احترام RLS/التصنيف + عرض الاستعلام دائماً قبل/مع النتيجة + حواجز (منع DDL/DML/دوال خطرة/حدود صفوف) + audit كامل · **Long Reports**: قوالب metadata، توليد قسمياً مع استشهاد لكل قسم، مراجعة بشرية قبل الاعتماد، تصدير md (صيَغ أخرى OD).

## 3. Out of Scope
تكاملات/أدوات خارجية وتنفيذ أفعال عبر أنظمة (P7) · كتابة SQL معدِّلة إطلاقاً · تدريب/ضبط نماذج · وكلاء مستقلون طويلو المدى (Backlog) · قنوات خارجية.

## 4. Required Inputs
P5 DoD · هذا التصميم Accepted · نماذج chat/reasoning معتمدة الصفوف ومربوطة في Registry · قوالب تقارير أولية (OD-P6-1 عند التفعيل).

## 5. Expected Outputs
دردشة مؤسسية تجيب من مصادر الحقيقة باستشهاد أو ترفض؛ سؤال بياني يتحول SQL قراءة آمناً ضمن الصلاحية؛ تقرير طويل مُستشهَد قسمياً قابل للمراجعة والاعتماد.

## 6. Functional Requirements
| # | المتطلب |
|---|---|
| FR-6.1 | Gateway كامل: chat/completions/streaming داخلي، توجيه per-agent/capability، fallback، مهل، حدود رموز، رفض أي استدعاء بلا سياق مستخدم. |
| FR-6.2 | Registry per-agent UI: نموذج+معاملات+fallback لكل وكيل؛ تغييرات مدقَّقة وباعتماد في الإنتاج. |
| FR-6.3 | Chat: جلسات بعنوان/مشروع، سياق مُجمَّع حصراً من (استرجاع محكوم + سجلات مسموحة + OKF موسوم)، حفظ الاستشهادات مع كل رسالة. |
| FR-6.4 | قاعدة الإجابة: ادعاء أعمال بلا مصدر ⇒ يُحجب ويُستبدل برفض No-Guessing؛ Validation-Agent يفحص قبل العرض (fail-closed). |
| FR-6.5 | SQL Agent: NL→SQL على allow-listed views فقط؛ منع بنيوي لغير SELECT؛ فرض RLS/تصنيف الناظر؛ عرض SQL الناتج؛ حد صفوف/مهلة؛ كل تنفيذ مدقَّق بنصه. |
| FR-6.6 | شرح النتائج البيانية بالاستناد إلى الصفوف المعادة فقط. |
| FR-6.7 | Reports: قالب (أقسام/مصادر مطلوبة) → توليد قسم-بقسم → استشهاد إلزامي لكل قسم → حالة مراجعة/اعتماد بشري → نسخ وversioning. |
| FR-6.8 | Orchestrator: خطوط معلنة ثابتة (لا تخطيط حر) مع نقاط فحص Validation بينية. |
| FR-6.9 | حدود استخدام أساسية لكل مستخدم/جلسة (رموز/طلبات) قابلة للضبط. |
| FR-6.10 | كل مخرجات الوكلاء تحمل وسم «مُولَّد» + مصادره — تمييز بصري ثابت عن بيانات المصدر. |

## 7. NFRs (الخاصة)
زمن أول رمز/استجابة يُقاس baseline بنموذج demo · انقطاع النموذج ⇒ fallback أو فشل مفسَّر (لا تعليق) · سجلات الوكلاء لا تتضمن أسراراً ولا نصوص مستندات فوق الحاجة (اقتطاع معلن).

## 8. User Stories
بصفتي موظفاً: أسأل عن سياسة فأحصل على إجابة بمصادر أفتحها · أسأل «كم معاملة متأخرة في إدارتي؟» فأرى SQL والنتيجة ضمن صلاحيتي · أطلب تقريراً شهرياً فأراجع أقسامه بمصادرها قبل اعتماده · حين لا توجد أدلة كافية يقول النظام ذلك صراحة.

## 9. Admin Stories
بصفتي أدمن: أبدّل نموذج وكيل التقارير من الواجهة فيسري بعد الاعتماد · أضبط حدود الرموز · أراجع سجل استعلامات SQL Agent بنصوصها · أوقف قدرة chat لقطاعٍ عبر flags دون كسر.

## 10. Main Modules + Epics
**Modules:** llm-gateway(اكتمال) · chat(جديد — ADR-0016) · sql-agent · reports · orchestrator/agents (+model/provider-registry توسعة).
**Epics:** E6.1 Gateway Full+Quotas → E6.2 Per-Agent Registry UI → E6.3 Chat Sessions+Grounded Context → E6.4 Validation fail-closed → E6.5 SQL Views Allow-list → E6.6 SQL Agent+Guards → E6.7 Report Templates → E6.8 Sectioned Generation+Cite → E6.9 Review/Approve Reports → E6.10 Hardening/Docs/Handoff.

## 11. Data Model Notes
chat_sessions/messages(+citations) · agent_bindings (per-agent model+params) · sql_allowlist_views(+تعريف التوليد من الميتاداتا) · sql_agent_log(نص الاستعلام/الناظر/العدّ) · report_templates/reports(+sections,citations,status,versions) · usage_counters — platform_db؛ لا نصوص مستندات تُخزَّن مكررة (مراجع chunks).

## 12. API Notes
/chat/* (sessions/messages/stream) · /agents/bindings/* · /sql-agent/query (تعيد SQL+النتيجة) · /reports/* (templates/generate-section/review/approve) — خلف الـ Gate؛ كل نداء نموذج داخلياً عبر GatewayAPI فقط.

## 13. UI Notes
Chat workspace (استشهادات جانبية، وسم «مُولَّد»، زر عرض المصدر) · SQL answer panel (الاستعلام ظاهر + جدول نتيجة) · Report studio (قالب→أقسام→مراجعة→اعتماد) · Per-agent model settings — RTL كاملة وتمييز ثنائي اللغة للاقتباسات.

## 14. Security &amp; Permissions
سياق الدردشة يُبنى **بعد** فلترة الصلاحية (لا حقن مستند غير مسموح) · SQL: allow-list + قراءة فقط + RLS/تصنيف بمستوى الـ views + حسابات DB بأدنى صلاحية · التقارير ترث «الأشد» من مصادرها ولا تُصدَّر إلا بسياسة P4 · حدود D9 على شاشات الإعداد.

## 15. Audit &amp; Logging
chat.session_created · chat.answer_served(بمعرّفات الاستشهاد وقرار الكفاية) · validation.blocked(سبب) · agent.binding_changed(+approval) · sql_agent.executed(النص/الناظر/الصفوف)/denied · report.section_generated/reviewed/approved/exported · quota.exceeded — مع correlation عبر السلسلة كاملة.

## 16. Configuration / Environment Impact
GATEWAY_TIMEOUTS/RETRIES · TOKEN_LIMITS/QUOTA_* · SQL_MAX_ROWS/TIMEOUT · REPORT_* — defaults+validation؛ اختيار النماذج من Registry (dynamic باعتماد)؛ لا حاويات جديدة (المزوّد Ollama/vLLM المطفأ يُفعَّل بعلَمه وصف صورته الشكلي من P0).

## 17. Provider Abstractions Impact
LLMProvider كامل عبر Gateway (Ollama dev / vLLM prod بالإعداد) · لا SDK نماذج خارج التنفيذ · بقية المزوّدات كما في P5.

## 18. Database / Migration Notes
Baseline migrations لجداول المرحلة · **allow-list views تُولَّد عبر خط التوليد المحكوم** (اعتماد بشري لكل view) — لا view يدوي خارج الخط · فهارس لسجل SQL والاستخدام.

## 19. Testing Strategy (إضافات)
أمان SQL: حزمة هجمات (DDL/DML/UNION خارج allow-list/تعليقات خبيثة/دوال خطرة) كلها تُرفض بنيوياً · إجابة بلا استشهاد تُحجب (اختبار Validation fail-closed) · حقن سياق: مستند غير مسموح لا يدخل الـ prompt (فحص تجميع السياق) · fallback نموذج يعمل · quota تُفرض · تقارير: قسم بلا مصدر يفشل الاعتماد آلياً.

## 20. Acceptance Criteria
1) دردشة تجيب بمصادر قابلة للفتح أو ترفض صراحة — بلا استثناء مُثبت اختبارياً. 2) SQL Agent لا ينفّذ إلا SELECT على allow-list ضمن صلاحية الناظر، والنص معروض ومدقَّق. 3) تقرير طويل يُولَّد قسمياً بمصادر لكل قسم ويُعتمد بشرياً. 4) تبديل نموذج وكيل من الواجهة يسري بتدقيق/اعتماد. 5) Validation fail-closed مُثبت (تعطيله يوقف الإجابات لا يفتحها). 6) وسم «مُولَّد» ظاهر دائماً. 7) لا استدعاء نموذج خارج الـ Gateway (CI). 8) RTL سليم.

## 21. Risks
هلوسة رغم الإسناد (تخفيف: Validation صارم + إظهار المقاطع نفسها) · حقن أوامر عبر محتوى المستندات (تخفيف: عزل تعليمات النظام + تعقيم السياق + اختبارات حقن) · تكلفة سياق (تخفيف: حدود وrerank) · إفراط صلاحيات views (تخفيف: توليدها المحكوم باعتماد).

## 22. Open Decisions
| OD | الموضوع | التوصية | البوابة |
|---|---|---|---|
| OD-P6-1 | قوالب التقارير الأولية | بذرتان: «تقرير حالة شهري» و«ملخص كيان» metadata قابلة للتحرير | Clarify التفعيل |
| OD-P6-2 | صيَغ تصدير التقارير غير md | تأجيل pdf/docx إلى صفوف ترخيص أدواتها ثم قرار | عند الطلب |
| OD-P6-3 | نماذج chat/reasoning الافتراضية | قياس عربي على مرشحين معتمدَي الأوزان ثم تثبيت في Registry | قبل التشغيل |

## 23. Definition of Done
Baseline المشترك + AC 1–8 خضراء + توثيق Chat/SQL/Reports + حزمة اختبارات أمان SQL ضمن CI + handoff بقائمة "لا يُلمس" (Gateway وValidation وallow-list) لوكيل P7.

## 24. Coding Agent Prompt
> القالب الموحّد §6 مع: **PHASE=6 · DESIGN=phases/designs/phase-6-gateway-agents-sql-chat-reports.md · RELEASE=v0.3-phase-design-package** — قاعدة حاكمة: **مصدر أو رفض**؛ التزم بأقسام 6/14/19/22.
