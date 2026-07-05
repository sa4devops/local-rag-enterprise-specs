> ⚠️ SUPERSEDED — لا يُستخدم للتنفيذ. المرجع الحالي: حزمة v2.0 (انظر superseded/README.md). تاريخ الوسم: 2026-07-03.

# تصميم النظام — منصة تشغيل معرفي مؤسسي تعمل في شبكة مغلقة
## حزمة التصميم التفصيلي (Detailed Design Package)

**بُنيت هذه الوثيقة على إجاباتك المعتمدة.** لا كود في هذه المرحلة. المبادئ الحاكمة المثبتة: النظام **منصة** لا chatbot؛ الـ LLM **ليس** مصدر الحقيقة؛ الواجهة النهائية **واجهة مؤسسية خاصة** (لا Open WebUI)؛ والنقل إلى الإنتاج يتم بـ **configuration فقط** ودون تعديل كود أو إعادة بناء معمارية.

---

## 1) الفهم الموحد المحدَّث (Updated Unified Understanding)

نبني **منتجاً كاملاً واحداً** يعمل بنفس الكود ونفس الـ repository ونفس بنية Docker على ثلاث بيئات (Local Dev على جهاز MSI Titan → Staging/Demo → Production لسيرفرات كبيرة تخدم 20,000–30,000 مستخدم مسجّل لكل مؤسسة)، والفرق بينها **إعدادات فقط** (environment / profiles / replicas / endpoints / secrets / resources / model providers).

النظام **metadata-driven**: الشاشات والحقول والصلاحيات والروابط تُعرَّف كبيانات في `platform_db`، وتُبنى من لوحة الأدمن دون تعديل كود. لوحة الأدمن تولّد الشاشات وجداولها عبر **خط أنابيب migrations محكوم** (توليد ملف migration → فحص تعارض/مخاطر → اعتماد → تطبيق → versioning → audit → شاشة توثيق)، **دون تنفيذ DDL مباشر من الـ LLM على الإنتاج**.

الحقيقة تأتي من: قواعد البيانات + المستندات المعتمدة + الـ APIs الداخلية + السجلات الرسمية. الـ LLM **يعالج فقط** ما تجلبه له الوكلاء ضمن حدود الصلاحية، ويُمنع من التخمين (No-Guessing Guard). كل عملية حرجة تُسجَّل في Audit Log، وتُعاد فيها التحقق live قبل التعديل/الاعتماد/التصدير.

الربط الأساسي **داخلي** (Internal APIs / MCP / Webhooks / DB Connectors)، مع مرونة لتكامل خارجي **اختياري** لاحقاً عبر proxy/gateway. الهوية تبدأ **Local Auth** مع تجريد (abstraction) يسمح لاحقاً بربط IdP داخلي (LDAP/AD/Keycloak/OIDC/SAML) **دون تعديل كود**. طبقة **OKF** تعمل محلياً كفهرس/قاموس/مسرد/تعريفات وتعليمات للوكلاء، لا كمصدر حقيقة ولا بديل عن القاعدة/الصلاحيات/التدقيق.

---

## 2) القرارات المعمارية المثبتة (Locked Architectural Decisions)

1. **منتج واحد قابل للنقل** (single portable product) — لا نسخة تطوير ونسخة إنتاج منفصلتين؛ لا fork للإنتاج.
2. **نشر مدفوع بالإعدادات** (configuration-driven deployment) بأسلوب Twelve-Factor: كل ما يتغيّر بين البيئات في env/config، لا في الكود.
3. **ثلاثة بروفايلات نشر**: Local Development / Staging-Demo / Production — نفس الصور، إعدادات مختلفة.
4. **قابلية التوسع الأفقي** (horizontal scalability): backend عديم الحالة (stateless) خلف load balancer، workers مستقلة، عُقد inference للـ GPU منفصلة.
5. **الواجهة النهائية = Enterprise UI خاصة** (Arabic/English، RTL كامل، white-label). Open WebUI **ليس** الوجه النهائي — يُدرَس كمرجع UX أو طبقة دردشة داخلية اختيارية فقط، **ولا يُستخدم أي كود منه أو من غيره إلا بعد مراجعة ترخيص تجيز التعديل/التوزيع/white-label/الاستخدام المؤسسي واسع النطاق/التشغيل المغلق ودون قيود branding أو عدد مستخدمين**.
6. **نموذج قاعدة البيانات** (`database.docx`): `platform_db` (تعريفات/حوكمة/صلاحيات/metadata) + `apps_db` (تطبيقات/شاشات، schema-per-app/domain) + `integration_db` + `reporting_db`. لا قاعدة فيزيائية منفصلة لكل إدارة من البداية.
7. **ثلاث درجات فصل مدعومة**: Logical (صلاحيات + ownership columns + RLS + classification) → Schema (لكل تطبيق/domain) → Physical (فقط عند سبب قوي: حساسية/حجم/عزل صارم)، وأي تطبيق يُنقل لقاعدة مستقلة لاحقاً **دون إعادة بناء المنصة** (تغيير endpoint في الإعدادات).
8. **التوليد التلقائي = خط أنابيب محكوم**: metadata → migration file → conflict check → risk check → approval → apply → versioning → audit → شاشة توثيق. **لا DDL مباشر من LLM في الإنتاج**.
9. **نموذج الصلاحيات**: RBAC + ABAC + ReBAC + Data Classification (Public/Internal/Confidential/Secret/Restricted) + Row-Level + Field-Level + Screen-Level + Action-Level + Least Privilege + Need-to-know + SoD، **مُقيَّمة قبل أي استرجاع** و**default-deny**.
10. **أعمدة الملكية والحوكمة** على السجلات: `department_id`, `sector_id`, `owner_user_id`, `classification` (+ حقول تدقيق).
11. **الوكلاء (Agents)** مع اختيار model/provider **لكل وكيل** مخزَّن كإعداد في `platform_db` وقابل للتغيير دون كود (نمط RedAmon)، عبر **LLM Gateway** مجرِّد يدعم Ollama/vLLM.
12. **OKF محلي** من البداية بدور محدود (Catalog/Dictionary/Glossary/Definitions/Agent-metadata)، **لا يعتمد على أي خدمة سحابية**.
13. **الهوية**: Local Auth الآن + **Identity Provider Adapter** يسمح بـ LDAP/AD/Keycloak/OIDC/SAML لاحقاً دون تعديل كود؛ الرقم الوظيفي واسم المستخدم **محميان وثابتان**؛ دعم تعطيل/تفعيل/تغيير كلمة المرور؛ SSO لاحقاً.
14. **Spec Kit** لتنظيم التطوير (constitution → specify → clarify → plan → tasks → implement)، والمخرجات/البرومبتات **محايدة لأي Coding Agent** (Claude Code/Codex/Cursor/Windsurf/Cline/Aider/OpenHands/Continue…)، و**Coding Model** منفصل (Qwen/DeepSeek/GLM Coder…). الـ specs مُلزِمة: الأداة تنفّذ ما هو مكتوب فقط.
15. **التدقيق (Audit)** عمود فقري (append-only) يُستدعى في كل عملية تغيير أو عملية حرجة، ويُسجّل قرار الصلاحية (allow/deny + السياسة الحاكمة).
16. **الكاش طبقة تسريع فقط**: لا final-response cache في بيانات الأعمال؛ RAG cache مربوط بنسخة المستند/الفهرس/السكيم/نطاق الصلاحية/الوقت؛ إعادة تحقق live قبل العمليات الحرجة.
17. **PentAGI/RedAmon**: استعارة أنماط فقط (تنسيق الوكلاء، اختيار النموذج لكل وكيل، human-in-the-loop، بوابات الاعتماد، التشغيل المغلق، config-driven، السجلات، ضبط تنفيذ الأدوات)، مع احتمال دمجهما لاحقاً **كأدوات** داخل المتجر لفريق الأمن/Red Team/CERT.
18. **الفيديو في MVP**: صوت→نص (Whisper) + تلخيص + keyframes/وصف أساسي؛ الفهم البصري الكامل مؤجَّل (غير محذوف).
19. **التقارير الطويلة** تُبنى قسماً قسماً (map-reduce فوق المصادر) مع الاستشهاد بالمصدر.
20. **بيئة مغلقة بالكامل**: كل الاعتماديات (images/wheels/models) تُنقل عبر حزمة offline قابلة للتحقق والاستعادة.

---

## 3) النواقص المتبقية (Remaining Gaps — لا تُعطّل التصميم)

هذه بنود ستُحسم لاحقاً كـ **إعدادات/قياسات**، ولا يتوقف عليها تصميم المعمارية:

- **العدد المتزامن** (concurrent users) الفعلي، ومنه أحجام replicas وعُقد الـ GPU.
- **العتاد النهائي للإنتاج** (عدد/نوع GPU، RAM، CPU، التخزين، الشبكة).
- **العدد النهائي** للإدارات/القطاعات/الشاشات، وحجم المستندات والسجلات (يحدد sizing لـ Qdrant/OpenSearch/MinIO/PostgreSQL).
- **جرد الأنظمة الداخلية** المراد ربطها وعقود الـ API/الـ MCP لكل منها.
- **الـ IdP المحدَّد** (LDAP/AD/Keycloak/OIDC/SAML) وخريطة الصفات (attribute mapping) عند مرحلة الربط.
- **مصفوفات الاعتماد** (approval matrices) و**قواعد SoD** التفصيلية لكل مؤسسة.
- **سياسات الاحتفاظ/النسخ الاحتياطي** و**نهج TLS/PKI** داخل الشبكة المغلقة.

**كلها قابلة للتأجيل** لأن التصميم يجعلها معاملات (parameters) وسياسات (policies) في `platform_db`/config، لا ثوابت في الكود.

---

## 4) تقييم خيارات بداية التنفيذ (A / B / C)

**الخيار A — Admin Foundation أولاً:** يؤسّس الهوية/التنظيم/الصلاحيات/التدقيق قبل الشاشات. *ميزة:* حوكمة قبل القدرة، مخاطر أمنية أقل. *عيب:* يؤخّر إثبات **جوهر المشروع الأعلى مخاطرةً تقنياً** (توليد الشاشات وقواعدها تحت الحوكمة)، فتبقى أكبر مجهولية دون تحقق مبكر.

**الخيار B — Screen Builder / DB Generator أولاً:** prototype ملموس سريع يثبت الفكرة. *عيب حاسم:* يخالف مبدأ المنصة نفسه («الحوكمة قبل القدرة»)، و**مستحيل عملياً نظيفاً** لأن باني الشاشات يكتب في **سجل الميتاداتا** ويحتاج هوية + بوابة صلاحية + تدقيق موجودة أولاً؛ البناء دون ذلك = إعادة كتابة لاحقة (وهو ما تريد تجنّبه صراحةً).

**الخيار C — Hybrid:** أساس أدمن مُصغَّر + باني شاشات مُصغَّر معاً.

---

## 5) القرار: **Hybrid (الخيار C) على هيئة «هيكل ماشٍ محكوم» (Governed Walking Skeleton)**

**السبب:** أفضل ممارسة معمارية هنا هي إثبات **أعلى مكوّن مجهولية** مبكراً عبر **شريحة رأسية رفيعة (vertical slice)** تمرّ خلال كل الطبقات الحرجة — لكن باني الشاشات **لا يُبنى على فراغ**؛ يحتاج هوية حقيقية + سجل ميتاداتا حقيقي + بوابة صلاحية مُنفَّذة + تدقيق حقيقي. لذلك نبني الأساس **حقيقياً لكن حدّه الأدنى**، ونمرّر عليه شريحة واحدة كاملة من توليد شاشة → ترحيل → اعتماد → CRUD. هذا يثبت **الأمن والحوكمة** و**جوهر المشروع** معاً end-to-end، **دون أي شيء يُعاد بناؤه لاحقاً** لأن الأساس حقيقي (فقط مُصغَّر). كل ما بعده (RBAC/ABAC/ReBAC الكامل، سير الاعتماد، RAG، الوكلاء، بوابة النماذج، المتجر، التقارير) **يُضاف طبقةً فوقه** بلا هدم.

### الحد الأدنى الدقيق للمرحلة ١ (Hybrid Lite — Walking Skeleton)

1. **Local Auth حقيقي:** تسجيل دخول/خروج، admin واحد مُزروع، تجزئة كلمات المرور، جلسة/JWT، و**واجهة IdentityProvider** (تنفيذ `LocalAuthProvider` الآن؛ LDAP/OIDC لاحقاً = تنفيذ جديد بلا تعديل جوهر).
2. **نموذج تنظيمي:** organization → sector → department، وربط المستخدم بإدارة/قطاع، و2–3 أدوار مزروعة (SystemAdmin / Manager / User).
3. **العمود الفقري للصلاحيات:** `PermissionService` **يُستدعى فعلياً قبل كل عملية بيانات** (قواعد v1 مبسّطة: دور + ملكية + تصنيف)، أعمدة ملكية على السجلات، enum للتصنيف، و**بوابة صلاحية مُنفَّذة لا وهمية**.
4. **سجل الميتاداتا** في `platform_db`: جداول `screen_definitions`, `field_definitions`, سجل التطبيقات/الأسكيمات، وسجل الـ migrations. باني الشاشات يكتب هنا.
5. **العمود الفقري للتدقيق:** `audit_log` (append-only) و`AuditService` تستدعيه كل عملية تغيير.
6. **شريحة باني الشاشات الرأسية:** واجهة أدمن مصغّرة لـ (١) تعريف شاشة + حقول → (٢) توليد **ملف migration** لجدول في `apps_db` تحت schema خاص بالتطبيق → (٣) فحص تعارض + مخاطر → (٤) إجراء اعتماد من الأدمن → (٥) تطبيق الترحيل → (٦) سجل توثيق التوليد → (٧) شاشة CRUD أساسية للمستخدم على الكيان المولَّد — **كل خطوة مُصرَّح بها ومسجَّلة**.
7. **قشرة Enterprise UI مصغّرة** (Arabic/English، RTL) تستضيف: الدخول، لوحة الأدمن (مستخدمون/تنظيم/أدوار + باني الشاشات)، وعارض الشاشة المولَّدة مع CRUD. **بلا** دردشة/متجر/باني workflow في هذه المرحلة.

> **خارج نطاق المرحلة ١** (يأتي في مراحل لاحقة): RAG/OCR، الوكلاء وبوابة النماذج، سير الاعتماد الكامل والإشعارات، RBAC/ABAC/ReBAC الكامل وField-Level، المتجر والتكاملات، التقارير الطويلة، المراقبة الكاملة.

---

## 6) نظرة عامة على المعمارية (Architecture Overview)

سبع طبقات داخل حدود مغلقة، مع شريط عرضي دائم (Audit/Cache/Monitoring/License/Hardware/Security). راجع المخطط العام `معمارية_النظام.svg` (سُلّم سابقاً) والمخططات التفصيلية أدناه.

`Presentation (Enterprise UI + طبقة دردشة اختيارية)` ← `Backend API (FastAPI, stateless)` ← `Agent Orchestrator/Router (Classifier + Context Builder + Permission Gate + No-Guessing Guard)` ← `Agents` ← `Knowledge & Models (OKF + LLM Gateway → Ollama/vLLM)` ← `Sources of Truth (platform/apps/integration/reporting DBs + Qdrant + OpenSearch + MinIO + Redis + Neo4j-opt)` ← `Connectors (MCP/API/Webhook/DB → أنظمة داخلية)`.

**قاعدة ذهبية:** الصلاحية تُفحص **قبل** أي استرجاع/SQL/API؛ الـ LLM يعالج فقط ما جلبه الوكيل؛ العمليات الحرجة تُعيد التحقق live.

---

## 7) مخطط المكوّنات (Component Diagram)

راجع `Component_Diagram.svg`. المكوّنات الرئيسية وحدودها:

- **Enterprise UI (Web):** Admin Console + User Workspace + Dynamic Screen Renderer + (Chat اختياري) + i18n/RTL + White-label theming.
- **API Gateway / Backend (FastAPI):** Auth & Session, Authorization (Permission Engine), Metadata Service (screens/fields/apps), Records/CRUD Service, Migration/Generation Pipeline, Audit Service, Integration Admin, App Store Service, Reports Service, LLM Gateway Client, Config/Profile Loader.
- **Orchestrator & Agents (Worker layer):** Orchestrator/Router + الوكلاء العشرة (Retrieval/SQL/Validation/Reasoning/Security-Policy/OCR-Doc/API-Integration/Report/Admin-Metadata) — قابلة للتوسع كـ workers مستقلة.
- **LLM Gateway:** تجريد موحّد فوق Ollama/vLLM؛ اختيار model/provider لكل وكيل من `platform_db`.
- **Data Plane:** PostgreSQL (4 قواعد) + Qdrant + OpenSearch + MinIO + Redis (+ Neo4j اختياري).
- **Connectors:** MCP servers + Internal API clients + Webhooks + DB connectors.
- **Cross-Cutting Services:** Audit, Cache, Monitoring (Prometheus/Grafana/Loki), License, Hardware/Runtime Manager, Security/Policy.

المكوّنات تتواصل عبر عقود واضحة (REST/gRPC داخلي + طابور مهام عبر Redis للوكلاء)، وكلها stateless قدر الإمكان لدعم التوسع الأفقي.

---

## 8) معمارية البيانات (Data Architecture)

**القواعد الأربع:**
- `platform_db` — الميتاداتا والحوكمة: المستخدمون، التنظيم، الأدوار، سياسات الصلاحيات (RBAC/ABAC/ReBAC)، مستويات التصنيف، تعريفات الشاشات/الحقول، سجل التطبيقات/الأسكيمات، سجل الـ migrations، إعدادات الوكلاء/النماذج، سجل التوليد، Audit Log، إعدادات النظام.
- `apps_db` — بيانات التطبيقات: **schema-per-application/domain**؛ جداول مولَّدة عبر خط الأنابيب المحكوم؛ كل سجل يحمل `department_id/sector_id/owner_user_id/classification` + حقول تدقيق.
- `integration_db` — حالة التكاملات: تسجيل الأنظمة، ربط حسابات المستخدمين، رموز/جلسات التفويض (مُعمّاة)، سجلّات الاستدعاء.
- `reporting_db` — القراءة التحليلية: نُسخ/تجميعات للتقارير (يمكن جعلها read-replica لاحقاً)، معزولة عن حِمل الكتابة التشغيلي.

**درجات الفصل الثلاث (مطبَّقة معاً):**
1. **Logical:** RLS على أعمدة الملكية + FLS + classification + Need-to-know.
2. **Schema:** عزل كل تطبيق/domain في schema مستقل داخل `apps_db`.
3. **Physical:** نقل تطبيق/domain حسّاس إلى قاعدة مستقلة **بتغيير endpoint في الإعدادات فقط** (الكود لا يفترض قاعدة واحدة؛ يستخدم موجِّه اتصال يقرأ الوجهة من الإعداد).

**المخازن المتخصصة:** Qdrant (متجهات RAG، مع quantization/sharding للتوسع) · OpenSearch (بحث نصي/BM25 وسجلّات) · MinIO (ملفات/مستندات، S3-compatible، erasure coding في الإنتاج) · Redis (كاش تسريع + طابور مهام + حالة جلسات لدعم backend عديم الحالة) · Neo4j (علاقات/رسم بياني، اختياري).

**خط أنابيب التوليد/الترحيل:** تعريف الشاشة (metadata) → مولِّد migration → فحص تعارض (أسماء/أنواع/مفاتيح) + فحص مخاطر (تصنيف/حجم/كسر توافق) → **اعتماد** → تطبيق داخل schema التطبيق → **versioning** لكل migration → **audit** → **شاشة توثيق** (توليد/تعديل/إيقاف/حذف). لا DDL مباشر من LLM.

**افتراضات القياس المبدئية (Sizing) وما يجب قياسه لاحقاً:**
- مسجّلون 20–30k/مؤسسة؛ افتراض تزامن مبدئي 2–5% (≈ 400–1500 متزامن) **للتحقق لاحقاً**.
- يجب قياس: ذروة المحادثات المتزامنة، متوسط الرموز/طلب، عدد المستندات وحجمها (GB)، عدد المتجهات (يحكم ذاكرة Qdrant)، QPS للبحث/SQL، معدل نمو السجلات.
- **Dev sizing** (MSI Titan): 1–2 مستخدم، نموذج رئيسي واحد يُبدَّل عبر Ollama، corpus صغير، replica واحدة.
- **Production sizing**: عُقد GPU منفصلة (vLLM)، N من backend replicas خلف LB، PostgreSQL مُدار/مُنسَخ + PgBouncer + read replicas للتقارير، Qdrant/OpenSearch/MinIO عناقيد، Redis (cluster/sentinel)، حزمة مراقبة.
- كل ذلك **قابل للتغيير عبر config لا كود**.

---

## 9) معمارية الصلاحيات (Permission Architecture)

**التقييم قبل أي استرجاع، بترتيب دفاعٍ متعمّق (default-deny في كل خطوة):**
1. **Authentication** — تحديد الهوية.
2. **RBAC** — الدور → الأفعال/الشاشات المسموحة (تصفية خشنة).
3. **ABAC** — صفات المستخدم (إدارة/قطاع/درجة تصنيف/سياق كالوقت/الشبكة) مقابل صفات المورد.
4. **ReBAC** — العلاقة الهرمية (مدير-لـ / عضو-في / مفوَّض-عن) → وصول هرمي.
5. **Data Classification** — درجة تصريح المستخدم ≥ تصنيف المورد + Need-to-know.
6. **Row-Level Security** — تُحقن على أعمدة الملكية/النطاق في مُنشئ الاستعلام.
7. **Field-Level Security** — إخفاء/منع حقول بعينها حسب الدور/التصنيف.
8. **Screen-Level & Action-Level** — رؤية الشاشة X، تنفيذ الإجراء Y.
9. **Separation of Duties (SoD)** — منشئ ≠ معتمِد، تعارضات الأدوار.
10. **Least Privilege** — الأصل المنع، والسماح استثناء موثّق.

**نقاط الإنفاذ (Enforcement Points):** middleware في الـ API (خشن) → **Permission Gate** في الـ Orchestrator (قبل الاسترجاع) → **query builder** يحقن RLS/FLS → **Answer engine** يخفي الحقول النهائية → **Audit** يسجّل القرار (allow/deny + السياسة الحاكمة). كل السياسات **بيانات في `platform_db`** (role_permissions، abac_policies، classification_levels، field_policies، screen_permissions، sod_rules)، قابلة للتحرير من لوحة الأدمن، **مُؤرشَفة (versioned) ومدقَّقة**.

**تكامل الكاش:** RAG cache مفتاحه يشمل نطاق الصلاحية + نسخة المستند/الفهرس/السكيم → يمنع تسريب بيانات مصنّفة؛ إعادة تحقق live قبل العمليات الحرجة.

---

## 10) معمارية الوكلاء (Agent Architecture)

راجع `Agent_Architecture.svg`. لكل وكيل **عقد واضح** و**model/provider قابل للضبط من `platform_db` دون كود** (نمط RedAmon) عبر LLM Gateway.

- **Orchestrator/Router:** يصنّف الطلب (استرجاع/SQL/إجراء/تقرير/مختلط)، يبني السياق (هوية + صلاحيات + ميتاداتا/OKF ذات صلة)، يُشغّل Permission Gate، يوزّع على الوكلاء، ويفرض No-Guessing Guard.
- **Retrieval Agent:** بحث هجين (Qdrant متجهي + OpenSearch نصي) → إعادة ترتيب (bge-reranker) → مقاطع **مُصفّاة بالصلاحية** مع provenance.
- **SQL Agent:** قراءة فقط، مقيّد بالسكيم والصلاحيات؛ يولّد SELECT مُعامَل ضمن جداول/أعمدة/صفوف مسموحة (allow-list + RLS)؛ **لا DDL/DML**؛ يعيد الصفوف + الاستعلام للتدقيق.
- **Validation Agent:** يتحقق أن الإجابة **مسنودة بالأدلة المسترجَعة** (وجود استشهادات)، يعلّم الادعاءات غير المدعومة، يفرض التصنيف على المخرَج.
- **Reasoning Agent:** يركّب التحليل/الإجابة **حصراً** من بيانات الوكلاء.
- **Security/Policy Agent:** فحوص السياسة، معالجة PII/التصنيف، **بوابات تنفيذ الأدوات** (human-in-the-loop للإجراءات الحساسة).
- **OCR/Doc Agent:** إدخال → OCR → تقطيع → embedding → فهرسة؛ الصوت عبر Whisper.
- **API-Integration Agent:** استدعاء الأنظمة الداخلية/أدوات MCP ضمن صلاحيات الحساب المربوط + بوابات اعتماد.
- **Report Agent:** تقارير طويلة **قسماً قسماً** (map-reduce فوق المصادر) مع استشهاد.
- **Admin/Metadata Agent:** يساعد في بناء الشاشات/الحقول/الـ migrations (**يولّد مخرجات للمراجعة، ولا يطبّق مباشرة**).

**No-Guessing Guard:** عند نقص الأدلة أو تقييد الصلاحية → «لا تتوفّر بيانات مُصرَّح بها كافية» بدل التخمين. **بوابات الاعتماد** (نمط PentAGI/RedAmon) على أي إجراء يغيّر حالة.

---

## 11) وحدات الواجهة (UI Modules)

**عامة:** Enterprise-grade، Arabic/English، RTL/LTR، white-label theming، Action/CTA buttons، Wizards للعمليات المعقّدة، أوامر طبيعية عبر LLM، جودة UX عالية.

- **Auth:** دخول/خروج، تغيير كلمة المرور، (SSO لاحقاً).
- **Admin Console:** المستخدمون · التنظيم (قطاعات/إدارات) · الأدوار والصلاحيات · التصنيفات · **باني الشاشات** · باني الحقول · **مراجعة/اعتماد التوليد والترحيل** · **توثيق التوليد** · إدارة التكامل (MCP/API) · عارض التدقيق · المراقبة · الترخيص · إعدادات النماذج/المزوّدين لكل وكيل · About/التراخيص.
- **User Workspace:** الرئيسية/لوحة · الشاشات الديناميكية (CRUD) · السجلات · ملف الكيان (Entity Profile) · المهام (Tasks) · المشاريع (Projects) · الإشعارات (بدردشة لكل إشعار) · **المتجر (App Store)** · الدردشة (أوامر LLM طبيعية) · التقارير/التصدير.
- **حسب المرحلة:** المرحلة ١ تُظهر فقط: Auth + Admin (مستخدمون/تنظيم/أدوار + باني شاشات) + عارض شاشة مولَّدة + CRUD.

---

## 12) معمارية النشر (Deployment Architecture) — Portable & Configuration-Driven

راجع `Deployment_Architecture.svg`. **الهدف الأول:** نفس الكود/الـ repo/الصور ينتقل من جهازك إلى الإنتاج بتغيير **إعدادات فقط**.

**المبادئ:**
- **Twelve-Factor:** الإعداد في البيئة لا الكود؛ صورة واحدة لكل خدمة؛ لا تفريعات حسب البيئة.
- **ملفات النشر:** `docker-compose.yml` (أساس) + `docker-compose.override.yml` (تطوير) + `docker-compose.prod.yml` (إنتاج: replicas، حدود موارد، TLS، endpoints خارجية) + `.env.local` / `.env.staging` / `.env.production`.
- **كل ما يتغيّر عبر config:** endpoints القواعد/التخزين/الكاش/البحث · مزوّدو ونقاط النماذج · إعدادات GPU/الموارد · عدد workers/replicas · secrets وTLS وpaths · feature flags · وجهات فصل القواعد الفيزيائي.
- **هرمية الإعداد:** defaults → profile env → runtime secrets، مع **تحقّق عند الإقلاع (fail-fast)** إن نقص إعداد حرج.
- **طبقات تجريد قابلة للتبديل عبر الإعداد:** LLM Provider (Ollama/vLLM) · Identity Provider (Local/LDAP/AD/OIDC/SAML) · Object Storage (MinIO/S3) · Vector/Search/Cache endpoints · Database connection router.
- **التوسع الأفقي:** backend عديم الحالة (جلسات في Redis/JWT) → replicas · workers (مستهلكو الطابور) تتوسّع مستقلة · inference على عُقد GPU منفصلة يُشار إليها بالإعداد.
- **الهجرات (migrations) نفسها** تعمل في كل البيئات.
- **البروفايلات الثلاثة:** Local Dev (جهازك، 1–2 مستخدم، Ollama، replica واحدة) · Staging/Demo (نفس الكود، إعدادات أكبر، اختبار workflows/صلاحيات/RAG/تكاملات) · Production (عُقد أكبر، backend متعدد، workers أكثر، GPU inference، قواعد إنتاج، monitoring، backup/restore، TLS، HA لاحقاً).
- **النقل المغلق:** حزمة offline (images + wheels + models) + استعادة + تحقق.

---

## 13) المخاطر والتخفيف (Risks & Mitigations)

- **انحراف البيئات (dev vs prod drift):** فرض «اختلاف الإعدادات فقط»؛ CI يبني صورة واحدة؛ منع كود خاص ببيئة؛ اختبارات تكامل لكل بروفايل.
- **GPU واحد لا يشغّل كل النماذج:** تبديل النماذج في التطوير (Ollama) + مجموعة نماذج مضبوطة بالبروفايل + LLM Gateway مجرِّد؛ الإنتاج vLLM متعدد GPU.
- **تعقيد metadata-driven:** خط ترحيل صارم (مراجعة/اعتماد/versioning/audit) دون DDL حي.
- **تجاوز الصلاحيات:** default-deny + بوابة قبل الاسترجاع + RLS/FLS في طبقة الاستعلام + تدقيق القرارات + اختبارات.
- **هلوسة الـ LLM كحقيقة:** No-Guessing Guard + Validation Agent + استشهادات + الحقيقة من القاعدة/المستندات/الـ APIs فقط.
- **تلوّث التراخيص:** لا كود خارجي دون مراجعة ترخيص؛ OKF محلي فقط؛ صفحة About/attribution؛ تجنّب كود Open WebUI المقيّد بالعلامة (v0.6.6+).
- **تحديث/نقل في بيئة مغلقة:** حزمة offline + تحقق + استعادة.
- **التوسع لـ 20–30k مستخدم:** backend عديم الحالة + replicas + PgBouncer + كاش تسريع + read replicas للتقارير.
- **إرهاق الاعتماد/ثغرات SoD:** مصفوفات اعتماد قابلة للضبط + قواعد SoD في الميتاداتا.
- **تسريب تصنيف عبر RAG cache:** مفتاح كاش يشمل نطاق الصلاحية + نسخ المستند/الفهرس/السكيم + إعادة تحقق live.

---

## ملحق — خريطة المراحل المحدَّثة (Phase Roadmap)

- **Phase 0 — Skeleton & Deployment Foundation:** repo + Spec Kit (constitution/specify/plan/tasks) + Docker Compose + البروفايلات الثلاثة + نظام الإعداد + هيكل المجلدات + health checks. لا منطق أعمال (إثبات إقلاع المنظومة واتصال الخدمات فقط).
- **Phase 1 — Governed Walking Skeleton (Hybrid Lite):** الحد الأدنى في القسم ٥.
- **Phase 2 — Full Screen/Field Builder + Records Engine:** كل أنواع الحقول والتحققات، إنفاذ RLS/FLS، خط توليد أغنى.
- **Phase 3 — Draft/Approval/Workflow + Action Buttons + Notifications.**
- **Phase 4 — Full Authorization (RBAC+ABAC+ReBAC) + Field/Row-level + SoD + Entity Profile.**
- **Phase 5 — Files/OCR/RAG + OKF layer + Safe SQL Agent + No-Guessing Guard + Orchestrator core.**
- **Phase 6 — LLM Gateway + per-agent model/provider + Hardware/Runtime Manager + Chat surface.**
- **Phase 7 — Integration Management (MCP/API/Webhook/DB) + Enterprise App Store + per-user linking.**
- **Phase 8 — Reports/Export + Monitoring + Offline transport/backup/restore + HA readiness.**

**البرومبتان 0 و1 مرفقان كملفّين مستقلّين للتنفيذ في محادثات منفصلة.**
