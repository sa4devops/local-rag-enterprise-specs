# UI_COMPONENT_STATES.md — كتالوج حالات المكوّنات

> **Version:** 1.0 — Proposed (v0.5) · **Date:** 2026-07-07 · **الموضع الهدف:** `ui/UI_COMPONENT_STATES.md`
> **مبنيّ فوق:** UI_INTERACTION_MODEL · UI_VISIBILITY_RULES · UI_PROGRESSIVE_DISCLOSURE (v0.5) · UI_ACTION_BUTTON_MODEL · UI_DESIGN_SYSTEM (v0.4).
> **الغرض:** جدول حالات موحّد لكل مكوّن رئيسي، لتُنتَج تصاميم Stitch بحالات دقيقة (لا رسم للحالة «الافتراضي السعيد» فقط).
> **المفتاح الموحّد للحالات الـ15:** `default` (S1) · `collapsed` (S2) · `expanded` (S3) · `loading` (S4) · `empty` (S5) · `error` (S6) · `permission-denied` (S7) · `disabled` (S8) · `hidden` (S9) · `masked` (S10) · `confirmation` (S11) · `approval` (S12) · `success` (S13) · `failed` (S14) · `audit-visible` (S15).
> **قواعد قراءة:** إن لم تُذكر حالة لمكوّن ⇒ **لا تُصمَّم** (لا تُخترع). إن كانت الحالة «لا تنطبق N/A» ⇒ ذُكرت صراحة.

---

## 1) Action Card (بطاقة معاينة الفعل في ws.thread)
| # | الحالة | ما يظهر | ما يُخفى | مصدر التبديل |
|---|---|---|---|---|
| S1 | default | رأس (اسم الفعل + مخاطر + تصنيف) + سطر «سيتم…» + حقول إلزامية فقط + زر تأكيد | حقول اختيارية، أثر تبعيات تفصيلي، «مزيد» | الافتراضي |
| S2 | collapsed | رأس البطاقة + شارة الحالة الحالية فقط | كل الحقول | نقر «طيّ» أو ظهور بطاقة أحدث في نفس thread |
| S3 | expanded | كل الحقول (إلزامية+اختيارية) + شرح الأثر التفصيلي | — | نقر «مزيد» |
| S4 | loading | skeleton لرأس البطاقة + خطوط للحقول + نبض خفيف | زر التأكيد (يظهر معطَّلاً بسبب «جارٍ التحضير…») | استقبال اقتراح من النموذج |
| S5 | empty | N/A — البطاقة لا تُنشأ بلا اقتراح | — | — |
| S6 | error | البطاقة تظهر بأخطاء تحقق مثبتة على الحقول + ملخص أعلى | زر تأكيد (يبقى disabled حتى الإصلاح) | Validation خادمية أرجعت أخطاء |
| S7 | permission-denied | تبدَّل ببطاقة `card.refusal_permission` (درع + صياغة عامة + فعلان آمنان) | كل الحقول | AUTHORIZED failed |
| S8 | disabled | البطاقة ظاهرة، الزر معطَّل + سبب مقتضب أعلى الأزرار | — | خارج نافذة idempotency / السياق تغيّر |
| S9 | hidden | N/A (بطاقة لا تُنشأ بلا اقتراح؛ لا حالة «مخفية» بعد الإنشاء) | — | — |
| S10 | masked | حقول حساسة تظهر «•••» + قفل | القيمة الفعلية | كلوحقٍ ذا clearance أعلى من الناظر |
| S11 | confirmation | نافذة تأكيد داخلية للـ simple، أو تحوّل إلى modal typed/dual للـ high/critical | البطاقة تعود L0 بعد الإلغاء | نقر زر التأكيد |
| S12 | approval | شارة «بانتظار الاعتماد» + رابط لبند في `queue.approvals` + مؤقّت تتبع | زر التأكيد (يختفي) | approval_required=true بعد Confirm |
| S13 | success | تحوّل إلى `card.result` (روابط فتح + مرجع تدقيق # + تراجع إن مدعوماً) | حقول الإدخال | EXECUTED |
| S14 | failed | البطاقة بحافة failure + error_code + request_id + زر «إعادة المحاولة» إن آمناً | — | فشل التنفيذ |
| S15 | audit-visible | إيصال مرجع تدقيق # في التذييل (لصاحب البطاقة)؛ لـ `audit.view` المخوّل: رابط «سلسلة كاملة» يفتح drawer end | — | حالة نهائية (success/failed) |

---

## 2) Action Button (زر فعل ضمن `run.detail` أو رأس شاشة)
| # | الحالة | ما يظهر | ملاحظات |
|---|---|---|---|
| S1 | default | نص + أيقونة اختيارية + مستوى بصري حسب risk (low/med/high/critical) | التنسيق من UI_DESIGN_SYSTEM §4 |
| S2 | collapsed | يختفي داخل قائمة «مزيد» (⋯) عند تجاوز 3 أزرار ظاهرة | مطبَّق بمعيار priority من Registry |
| S3 | expanded | يخرج من «مزيد» ليصبح ظاهراً | حين يفتح المستخدم القائمة |
| S4 | loading | زر بمؤشر دوّار داخلي + تعطيل التفاعل | أثناء EXECUTING |
| S5 | empty | N/A | — |
| S6 | error | tooltip أحمر خفيف بجانب الزر إن كان الخطأ متعلقاً بشرطه (نادر — الأصل رسائل عبر modal/toast) | — |
| S7 | permission-denied | **HIDDEN-SERVER** — لا يصل للمتصفح | القاعدة الحاسمة |
| S8 | disabled | زر رمادي + tooltip بسبب i18n مقتضب (كتالوج مغلق — OD-VZ-1) | مثال: «الحالة الحالية لا تسمح» |
| S9 | hidden | مطابق S7 (لا فرق دلالي عملي) | — |
| S10 | masked | N/A (الأزرار لا تُقنَّع؛ إما تظهر أو تُخفى/تُعطَّل) | — |
| S11 | confirmation | نقره يفتح: نافذة تأكيد inline (simple)، modal typed (high)، modal dual مع عدّاد (critical) | من ACTION_BUTTON §4 |
| S12 | approval | زر ينتقل إلى «بانتظار الاعتماد» + رابط للبند | يختفي فعل التنفيذ حتى قرار المعتمِد |
| S13 | success | toast/inline قصير + تحديث الشاشة (حالة السجل/الصف) | لا يبقى ظاهراً >4 ثوان |
| S14 | failed | toast أحمر بـ error_code + request_id + زر «تفاصيل» يفتح drawer end | — |
| S15 | audit-visible | شارة «مرجع تدقيق» على الصف بعد التنفيذ | تُفتح كسلسلة للمخوّل |

---

## 3) Citation Panel (`panel.citations` داخل context panel في ws.main)
| # | الحالة | ما يظهر |
|---|---|---|
| S1 | default | التبويب مطويّ عنوانياً؛ يفتح تلقائياً عند وصول استشهاد جديد (OD-IX-2) |
| S2 | collapsed | رأس التبويب + عدد الاستشهادات فقط |
| S3 | expanded | قائمة الاستشهادات (عنوان/محدد دقيق/شارة تصنيف/منشأ) — L1 |
| S4 | loading | skeleton بثلاثة صفوف |
| S5 | empty | «لا توجد استشهادات في هذه الرسالة» — بلا خطأ |
| S6 | error | «تعذّر تحميل الاستشهادات» + إعادة محاولة |
| S7 | permission-denied | استشهاد بعينه ⇒ تُبدَّل بطاقته بـ «مصدر مقيّد» بلا كشف تفاصيل |
| S8 | disabled | N/A |
| S9 | hidden | التبويب لا يظهر إن لم يكن هناك استشهاد قط في الجلسة |
| S10 | masked | نص المقتطف يظهر «•••» للحقول الحساسة، الرابط قد يبقى مفتوحاً لعنوان المصدر فقط |
| S11 | confirmation | N/A |
| S12 | approval | N/A |
| S13 | success | فتح المصدر ناجح ⇒ drawer end أو page المصدر |
| S14 | failed | فتح المصدر فشل (حذف/تحريك) ⇒ رسالة بديلة + رابط للنسخة السابقة إن وُجدت |
| S15 | audit-visible | حدث DOC_VIEWED لسجلات الوصول الحساسة يظهر للمخوّل عبر panel.audit |

---

## 4) Scope Selector (`ws.scope_selector` داخل ws.composer)
| # | الحالة | ما يظهر |
|---|---|---|
| S1 | default | نطاق افتراضي (مثلاً «إدارتي») — chip واحد |
| S2 | collapsed | chip واحد + عدد النطاقات المضافة |
| S3 | expanded | لوحة اختيار متعدد بمجموعات (وحدتي/مصادر معينة/OKF) — L1 |
| S4 | loading | skeleton خفيف عند جلب المصادر المسموحة |
| S5 | empty | N/A — دائماً هناك افتراضي |
| S6 | error | «تعذّر جلب المصادر» + الاحتفاظ بالافتراضي |
| S7 | permission-denied | خيارات غير المسموحة **لا تظهر** (HIDDEN-SERVER) |
| S8 | disabled | يُعطَّل في وضع الدردشة الحتمية أو Safe Mode مع سبب |
| S9 | hidden | N/A |
| S10 | masked | N/A |
| S11 | confirmation | تغيير النطاق لا يتطلب تأكيداً؛ يحدّث سياق الجلسة فوراً |
| S12 | approval | N/A |
| S13 | success | تغيير مطبَّق فوراً + تأشير بصري خفيف |
| S14 | failed | فشل التطبيق ⇒ العودة للنطاق السابق مع رسالة |
| S15 | audit-visible | تغييرات النطاق قد تُدقَّق لجلسات الحساسة (سياسة تفعيل) |

---

## 5) Related Records Panel (تبويب Related داخل ws.main)
| # | الحالة | ما يظهر |
|---|---|---|
| S1 | default | مطويّ عنوانياً؛ يفتح عند اكتشاف سجل مرتبط بالسياق |
| S2 | collapsed | رأس + عدد السجلات |
| S3 | expanded | قائمة (عنوان/نوع/شارة تصنيف/إجراء «فتح») — 5 صفوف كحد أقصى ثم «عرض الكل» ⇒ `run.list` |
| S4 | loading | skeleton |
| S5 | empty | التبويب لا يظهر إن لم توجد ارتباطات |
| S6 | error | رسالة قصيرة + إعادة محاولة |
| S7 | permission-denied | السجلات خارج نطاق الناظر مخفية دون عدّ (صمت البيانات — OD-VZ-3) |
| S8 | disabled | N/A |
| S9 | hidden | كما S5 |
| S10 | masked | حقول العنوان الحساسة مقنَّعة داخل الصف |
| S11 | confirmation | N/A |
| S12 | approval | N/A |
| S13 | success | «فتح» ينقل إلى drawer end (معاينة) أو page `run.detail` |
| S14 | failed | فشل فتح السجل (حذف) ⇒ إشعار قصير |
| S15 | audit-visible | حدث RECORD_OPENED للحساس |

---

## 6) Runtime Renderer List (`run.list`)
| # | الحالة | ما يظهر |
|---|---|---|
| S1 | default | جدول بـ 5–7 أعمدة + شريط بحث/فلترة بسيط + صف مختار مبدئياً (أول صف) |
| S2 | collapsed | شريط الفلاتر المتقدم مطويّ في drawer end |
| S3 | expanded | column picker مفتوح أو الفلاتر المتقدمة في drawer end |
| S4 | loading | skeleton صفوف (10) + شريط رأس ثابت |
| S5 | empty | حالة إرشادية: «لا توجد بيانات ضمن نطاقك» + دعوة لإنشاء أول سجل إن كان الفعل مسموحاً |
| S6 | error | رسالة عليا + زر «إعادة المحاولة» + الاحتفاظ بالفلاتر |
| S7 | permission-denied | الوصول للصفحة مرفوض 403 مفسَّرة (لا يصلها المستخدم أصلاً غالباً) |
| S8 | disabled | N/A (على مستوى الشاشة) |
| S9 | hidden | صفوف خارج النطاق **لا تظهر** ولا تُعدّ |
| S10 | masked | خلايا الحقول الحساسة «•••» + قفل صغير |
| S11 | confirmation | إجراءات bulk (مؤجلة) — لا تنطبق v1 |
| S12 | approval | صفوف بحالات «بانتظار الاعتماد» تحمل شارتها |
| S13 | success | بعد فعل صف: toast + تحديث الصف/الحالة بلا إعادة تحميل كاملة |
| S14 | failed | toast أحمر + الصف يعود لحالته السابقة |
| S15 | audit-visible | زر «سلسلة تدقيق الصف» في drawer end للمخوّل |

---

## 7) Runtime Renderer Form (`run.form`)
| # | الحالة | ما يظهر |
|---|---|---|
| S1 | default | القسم الأساسي مفتوح فقط، الأقسام الأخرى مطوية بعدّاد حقول |
| S2 | collapsed | كل الأقسام مطوية عدا الأساسي |
| S3 | expanded | قسم واحد يفتحه المستخدم (تراكم مسموح — لكن الافتراضي واحد) |
| S4 | loading | skeleton حقول القسم النشط فقط |
| S5 | empty | نموذج جديد ⇒ حقول فارغة بـ placeholders إرشادية |
| S6 | error | ملخص أخطاء أعلى + إشارات على الحقول + رابط قافز لكل خطأ |
| S7 | permission-denied | حقول بعينها HIDDEN-SERVER؛ إن رُفض الحفظ ⇒ رسالة عامة |
| S8 | disabled | حقول قراءة فقط في حالة معينة (workflow state) + سبب |
| S9 | hidden | حقول شرطية لا تظهر حتى تفعّل شرطها |
| S10 | masked | قيمة حساسة سابقة تظهر «•••» ولا تُرسل ما لم يُحرَّرها المستخدم |
| S11 | confirmation | حفظ الفعل high/critical يفتح modal typed | 
| S12 | approval | حفظ يفتح بند اعتماد ⇒ النموذج ينتقل لحالة «بانتظار الاعتماد» ويصبح غير قابل للتحرير حتى القرار |
| S13 | success | إعادة توجيه إلى `run.detail` أو الرجوع إلى `run.list` — بناءً على تفضيل معلن |
| S14 | failed | يبقى في النموذج + الأخطاء ظاهرة + توست |
| S15 | audit-visible | «آخر تعديل بواسطة/في» للمخوّل أعلى النموذج |

---

## 8) Runtime Renderer Detail (`run.detail`)
| # | الحالة | ما يظهر |
|---|---|---|
| S1 | default | شارة الحالة + بيانات أساسية + 3 أزرار أفعال في الرأس + tabs (تفاصيل/سجل/مرفقات) |
| S2 | collapsed | tabs الثانوية مطوية؛ panel.audit جانبي مطويّ للمخوّل |
| S3 | expanded | tab إضافي أو panel.audit مفتوح |
| S4 | loading | skeleton شارات ورأس + محتوى tab نشط |
| S5 | empty | N/A (الوصول يعني وجود السجل) |
| S6 | error | «تعذّر تحميل السجل» + زر إعادة |
| S7 | permission-denied | 403 مفسَّرة قبل الوصول |
| S8 | disabled | الأزرار غير المسموحة بالحالة تظهر معطَّلة بسبب |
| S9 | hidden | حقول/tabs بعينها بحسب صلاحيات الناظر |
| S10 | masked | حقول حساسة داخل تفاصيل السجل مقنَّعة |
| S11 | confirmation | كل فعل high/critical يفتح modal مناسباً |
| S12 | approval | إن كان السجل في حالة بانتظار اعتماد ⇒ شارة عليا + رابط للبند |
| S13 | success | تحديث بصري لحالة السجل بعد أي فعل |
| S14 | failed | toast + الاحتفاظ بالحالة السابقة |
| S15 | audit-visible | panel.audit جانبي للمخوّل بسلسلة correlation |

---

## 9) Approval Card / Decision Bar (`queue.approval_detail`)
| # | الحالة | ما يظهر |
|---|---|---|
| S1 | default | ملخص البند + الأثر المعلن + شريط قرارات (موافقة/رفض/إرجاع) + thread أدنى |
| S2 | collapsed | ملخص البند فقط + عدد رسائل thread |
| S3 | expanded | تفاصيل كاملة + مرفقات + سياسة الاعتماد المعمول بها |
| S4 | loading | skeleton |
| S5 | empty | N/A |
| S6 | error | «تعذّر جلب البند» |
| S7 | permission-denied | إن كان الناظر ليس طرفاً/معتمِداً ⇒ 403 |
| S8 | disabled | القرار يُعطَّل إن كان الناظر هو المقدِّم (SoD) — سبب صريح |
| S9 | hidden | حقول لا تخص الناظر (مثلاً تعليقات معتمِد آخر) قد تُخفى إذا كان النطاق يفرض ذلك |
| S10 | masked | حقول حساسة في الأثر المعلن مقنَّعة إذا تجاوزت clearance الناظر |
| S11 | confirmation | «موافقة» بلا تعليق تكفي بـ simple؛ «رفض» يستوجب تعليقاً إلزامياً؛ الحرِج بـ typed |
| S12 | approval | هذا هو سطح الاعتماد نفسه — لا يستدعي اعتماداً إضافياً إلا في السياسة (اعتماد مزدوج) |
| S13 | success | البند ينتقل إلى Approved/Rejected/Returned + إشعار للأطراف |
| S14 | failed | فشل الشبكة ⇒ الاحتفاظ بحالة draft للقرار حتى إعادة الإرسال |
| S15 | audit-visible | حدث APPROVAL_DECIDED + THREAD_POSTED — سلسلة كاملة للمخوّل |

---

## 10) Admin Definition Card (بطاقة تعريف: نوع/فعل/workflow/سياسة)
| # | الحالة | ما يظهر |
|---|---|---|
| S1 | default | شريط دورة الحياة (Draft→Validated→Approved→Active→RolledBack) + رأس التعريف + tab نشط واحد |
| S2 | collapsed | الرأس + الحالة + المسؤولون فقط |
| S3 | expanded | tab آخر مفتوح (diff/محاكاة/تبعيات) |
| S4 | loading | skeleton |
| S5 | empty | تعريف جديد ⇒ نموذج فارغ |
| S6 | error | خطأ Validation ⇒ لوحة أخطاء بيانية (دورات/حالات ميتة …) |
| S7 | permission-denied | لا يصل غير admin أصلاً |
| S8 | disabled | أزرار «تفعيل» معطَّلة قبل Approval — سبب صريح |
| S9 | hidden | tabs بعينها (مثل «إعدادات متقدمة») تظهر بصلاحية superadmin |
| S10 | masked | N/A |
| S11 | confirmation | «اعتماد» يستدعي typed بشخص مختلف (SoD ظاهر) |
| S12 | approval | نفس البطاقة تنتقل لحالة «بانتظار اعتماد شخص مختلف» |
| S13 | success | تفعيل ناجح ⇒ الحالة تصبح Active + إشعار |
| S14 | failed | فشل التفعيل (تعارض migration) ⇒ رسالة تفصيلية + إجراء تصحيحي مقترح |
| S15 | audit-visible | كل الأحداث (DEFINED/VALIDATED/APPROVED/ACTIVATED/ROLLED_BACK) تظهر للمخوّل في drawer end «سلسلة التعريف» |

---

## 11) Provider Status Card (بطاقة قدرة/مزوّد/نموذج في `admin.capabilities`)
| # | الحالة | ما يظهر |
|---|---|---|
| S1 | default | capability + provider ref + model ref + fallback + chip حالة (نشط/معطَّل) |
| S2 | collapsed | صف مضغوط في الجدول |
| S3 | expanded | drawer end بتفاصيل الربط + خطة إعادة الفهرسة إن embedding |
| S4 | loading | skeleton صف |
| S5 | empty | «لم يُربط أي نموذج بهذه القدرة» |
| S6 | error | فشل «اختبار الاتصال» ⇒ chip فشل + رسالة عامة (بلا endpoint) |
| S7 | permission-denied | الشاشة لا تظهر لغير admin.models.manage |
| S8 | disabled | تغيير الربط يُعطَّل في Safe Mode |
| S9 | hidden | endpoints/secrets **لا تظهر أبداً** — لا حالة تُظهرها (D9) |
| S10 | masked | N/A (لا شيء حساس يُعرض أصلاً) |
| S11 | confirmation | تغيير الربط في الإنتاج ⇒ modal typed + شارة «يتطلب اعتماداً» |
| S12 | approval | البطاقة تنتقل «بانتظار الاعتماد» ⇒ بند في `queue.approvals` |
| S13 | success | «اختبار الاتصال» ⇒ chip نجاح فقط (بلا كشف) |
| S14 | failed | «اختبار الاتصال» ⇒ chip فشل + رسالة قابلة للنسخ بـ correlation |
| S15 | audit-visible | CAPABILITY_BINDING_CHANGED مع «قبل/بعد» للمخوّل |

---

## 12) Retrieval Tester Result (`admin.retrieval_tester`)
| # | الحالة | ما يظهر |
|---|---|---|
| S1 | default | حقل استعلام + زر تشغيل — النتائج فارغة قبل التشغيل |
| S2 | collapsed | عرض نتيجة واحدة برأس + عدد النتائج + قرار الكفاية |
| S3 | expanded | قائمة نتائج مع محددات provenance مفصَّلة |
| S4 | loading | مؤشر تنفيذ + skeleton نتائج |
| S5 | empty | «لم يُعثر على نتائج ضمن نطاق صلاحيتك» |
| S6 | error | خطأ في الاسترجاع ⇒ error_code + سبب عام |
| S7 | permission-denied | الشاشة تظهر فقط لـ admin.knowledge.manage |
| S8 | disabled | زر التشغيل يُعطَّل في Safe Mode |
| S9 | hidden | نتائج خارج نطاق **المُجرِّب نفسه** لا تظهر (اختبار داخل صلاحيته) |
| S10 | masked | مقاطع تحوي حقولاً حساسة تظهر بمقتطف مقنَّع |
| S11 | confirmation | N/A |
| S12 | approval | N/A |
| S13 | success | لافتة كفاية «كافٍ» خضراء + النتائج |
| S14 | failed | لافتة «غير كافٍ» صفراء + عدم عرض إجابة (يطابق No-Guessing) |
| S15 | audit-visible | RAG_QUERY_SIMULATED مع نص الاستعلام والنطاق للمخوّل |

---

## 13) Audit Log Row (`admin.audit`)
| # | الحالة | ما يظهر |
|---|---|---|
| S1 | default | صف: الوقت · الفاعل · الفعل · الهدف · الحالة |
| S2 | collapsed | نفس S1 (الصف مضغوط دائماً في القائمة) |
| S3 | expanded | نقر الصف ⇒ drawer end بسلسلة correlation كاملة + before/after |
| S4 | loading | skeleton صفوف |
| S5 | empty | «لا توجد أحداث تطابق الفلتر» |
| S6 | error | «تعذّر جلب السجلات» + إعادة |
| S7 | permission-denied | الشاشة لا تظهر لغير audit.view |
| S8 | disabled | N/A (قراءة فقط) |
| S9 | hidden | صفوف خارج نطاق الناظر لا تظهر؛ مع بند «نتائج خارج نطاقك: N» (استثناء OD-VZ-3 المعلن) |
| S10 | masked | حقول حساسة داخل payload الحدث مقنَّعة |
| S11 | confirmation | N/A |
| S12 | approval | N/A |
| S13 | success | التصدير المحكوم ينجح ⇒ AUDIT_EXPORTED |
| S14 | failed | فشل التصدير (سياسة تصنيف) ⇒ رفض مفسَّر |
| S15 | audit-visible | ذات نفسها — كل سجل هو تدقيق؛ فتح الحدث يعرض chain كامل |

---

## 14) Provider Card — بطاقة مزوّد (admin.capabilities / تبويب Providers) — (Δ v0.6)
| # | الحالة | ما يظهر |
|---|---|---|
| S1 | default | حقول القائمة المقفلة (§3 من مواصفة المزوّدات): alias · type · secret_ref-بالاسم+قفل · chip الحالة · آخر فحص · العدّادات الثلاثة · زر اختبار · زر طلب تغيير |
| S2 | collapsed | صف مضغوط في القائمة (alias + chip + عدّاد قابل للاستخدام) |
| S3 | expanded | drawer end تفاصيل — **بلا أي حقل حساس حتى هنا** |
| S4 | loading | skeleton بطاقة |
| S5 | empty | «لا مزوّدات معلنة — تُعرَّف عبر config» + زر «طلب تهيئة مزوّد» |
| S6 | error | تعذّر قراءة الحالة ⇒ chip رمادي متقطع + إعادة محاولة |
| S7 | permission-denied | الشاشة admin-only — لا بطاقة تصل لغير المخوّل |
| S8 | disabled | Safe Mode: زرا الاختبار والطلب معطَّلان بسبب موحّد |
| S9 | hidden | N/A (كل المعلن في config يظهر للمخوّل) |
| S10 | masked | **تقنيع بنيوي دائم**: secret_ref اسماً فقط؛ لا وجود أصلاً لقيم URL/سر |
| S11 | confirmation | N/A (لا فعل خطر مباشر — التغيير عبر workflow) |
| S12 | approval | شارة «طلب معلّق #» عند وجود wf.provider_change مفتوح |
| S13 | success | اختبار الاتصال ⇒ chip نجاح فقط |
| S14 | failed | اختبار ⇒ chip فشل + رسالة عامة قابلة للنسخ بمرجع correlation |
| S15 | audit-visible | drawer «تاريخ الفحوصات/الطلبات» للمخوّل |

---

## 15) Model Profile Selector (`ws.model_profile_selector`) — (Δ v0.6)
| # | الحالة | ما يظهر |
|---|---|---|
| S1 | default | **مخفي للمستخدم العادي** (الافتراضي يعمل بصمت — OD-MX-1)؛ للدور المخوَّل: chip باسم الـ Profile الحالي بجوار محدد النطاق |
| S2 | collapsed | chip فقط |
| S3 | expanded | قائمة Profiles المسموحة لدوره (label + سطر وصف) — **لا أسماء نماذج خام أبداً** |
| S4 | loading | skeleton خفيف |
| S5 | empty | N/A (Default Profile موجود دائماً) |
| S6 | error | تعذّر الجلب ⇒ الإبقاء على الحالي + إشعار خفيف |
| S7 | permission-denied | الخيارات خارج الدور HIDDEN-SERVER |
| S8 | disabled | Profile بمزوّد ساقط ⇒ خيار معطَّل بسبب؛ Safe Mode ⇒ المحدد كله معطَّل |
| S9 | hidden | حالة S1 للمستخدم العادي |
| S10 | masked | N/A |
| S11 | confirmation | التبديل فوري بلا تأكيد (نطاق الجلسة) |
| S12 | approval | N/A (الاعتماد على تعريف الـ Profile في الـ Console) |
| S13 | success | تطبيق فوري + تأشير بصري |
| S14 | failed | رجوع للسابق + رسالة |
| S15 | audit-visible | model_ref/profile_key ضمن حمولة أحداث الجلسة للمخوّل |

---

## 16) Run Timeline Step — خطوة الخط الزمني (runs.detail) — (Δ v0.6)
| # | الحالة | ما يظهر |
|---|---|---|
| S1 | default | صف L0: رقم · اسم · أيقونة نوع (وكيل/Validation/فعل/موصل) · chip حالة · مدة |
| S2 | collapsed | كما S1 (الصف مضغوط أصلاً) |
| S3 | expanded | inline ملخص سطرين ⇒ «تفاصيل» يفتح Step Drawer |
| S4 | loading | running بنبض |
| S5 | empty | N/A |
| S6 | error | failed + error_code (السبب المفسَّر في الـ Drawer) |
| S7 | permission-denied | **بنية الخط مرئية لصاحب التشغيل دائماً؛ التقنيع للمحتوى**: خطوة بمحتوى فوق clearance تُظهر العنوان والحالة ومحتواها «مقيّد» |
| S8 | disabled | «إعادة من هنا» معطَّل لغير المؤهلة بسبب (نجحت/غير قابلة للإعادة) |
| S9 | hidden | N/A (انظر S7) |
| S10 | masked | digest المدخل/المخرج مقنَّع بحسب التصنيف |
| S11 | confirmation | retry_step ⇒ typed عند أثر act |
| S12 | approval | awaiting_approval: عقدة بوابة مميّزة + «فتح البند» (القرار على queue) |
| S13 | success | succeeded |
| S14 | failed | failed؛ والتوابع skipped بملاحظة «تخطٍّ بسبب فشل الخطوة N» |
| S15 | audit-visible | مراجع أحداث الخطوة داخل الـ Drawer للمخوّل |

---

## 17) Run Output Panel — لوحة الأدلة/المخرجات (runs.detail) — (Δ v0.6)
| # | الحالة | ما يظهر |
|---|---|---|
| S1 | default | تبويبات مطوية: المخرجات (بعدّاد) · الاستشهادات · التدقيق |
| S2 | collapsed | رؤوس فقط؛ **رأس «التدقيق» غائب كلياً** لغير audit.view |
| S3 | expanded | تبويب واحد مفتوح؛ «المخرجات» يفتح تلقائياً عند أول ناتج (قياس OD-IX-2) |
| S4 | loading | skeleton عناصر |
| S5 | empty | «لا مخرجات بعد» |
| S6 | error | صف عنصر تعذّر جلبه + إعادة |
| S7 | permission-denied | عنصر بتصنيف أعلى من الناظر ⇒ يظهر «عنصر مقيّد» **بلا فتح** (القاعدة الذهبية §9 من المواصفة) |
| S8 | disabled | زر فتح معطَّل بسبب حالة العنصر (قيد اعتماد) |
| S9 | hidden | لغير المخوّل بالـ run لا لوحة أصلاً |
| S10 | masked | مقتطفات الاستشهاد الحساسة «•••» |
| S11 | confirmation | N/A |
| S12 | approval | عنصر تقرير بانتظار مراجعة ⇒ شارة + رابط reports.review |
| S13 | success | فتح العنصر في سطحه |
| S14 | failed | ملف offload مفقود/محذوف ⇒ رسالة بديلة + مرجع |
| S15 | audit-visible | تبويب التدقيق: سلسلة correlation للـ run بنفس محرك admin.audit |

---

## 18) قواعد الاستخدام في Stitch
1. **لا تُصمَّم حالة لم تُدرَج هنا** — إن احتاج المصمم حالة إضافية ⇒ تضاف بقاعدة (OD جديد) لا تُرتجل.
2. **لكل بطاقة/شاشة يُطلب من Stitch عرض ≥6 حالات حرجة** كحد أدنى: default · collapsed · loading · empty · error · permission-denied — والباقي حسب طبيعة المكوّن (confirmation/approval للأفعال؛ masked للحساس؛ audit-visible للمخوّل).
3. **الحالات غير المنطبقة (N/A) تُذكر صراحة** لتجنب اختراع Stitch لتصميمات لا لزوم لها.
4. **الحالات تُعرض بترتيب موحّد** (S1→S15) في storyboard الـ prompt لتسهيل المراجعة.
5. **لا حالة تُخترق قاعدة صلاحية أو تصنيف** حتى في التصميم — القيم دائماً وهمية، والحساس دائماً مقنَّع بصرياً.
