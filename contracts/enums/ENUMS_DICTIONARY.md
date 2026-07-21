# ENUMS_DICTIONARY.md — القاموس المركزي للتعدادات

```contract
id: enums.dictionary
version: 1.0
status: Proposed
owner: Specification Architect (SA-delegated)
since: 2026-07-19 (G1)
relates: contracts.standard §1 · ADR-0035 · aql@eab9f99 (مصدر البذرة التجريبي)
```

> **Purpose:** كل قيمة تعداد تُعرَّف هنا مرة واحدة وتُستهلك بالمعرف؛ الترجمة عبر `enum.{enum_id}.{value}`. **البذرة أدناه مصدرها تجربة aql `[حقيقة — src/mocks/types.ts]` وحالتها Candidate** — اعتمادها النهائي ومواءمتها مع دورة الحياة الكنسية بوابةُ **FP-0001**.

| enum_id | القيم (snake_case) | المصدر | الحالة | ملاحظة المواءمة |
|---|---|---|---|---|
| `status_value` | `draft` · `under_review` · `approved` · `rejected` · `archived` | ‏aql-trial | **Candidate** | **فحص إلزامي في FP-0001:** المواءمة مع حالات دورة الحياة في شريط الـ Builder (بطاقات 11/13) وعائلة البادجات في `UI_DESIGN_SYSTEM` — قد تنقسم إلى `lifecycle_state` للسجلات و`definition_status` للتعريفات |
| `risk_level` | `low` · `medium` · `high` · `critical` | ‏aql-trial | **Candidate** | تتقاطع مع مصفوفة مخاطر عقد الفعل (بطاقة 12) — توحيد المرجع عند اعتماد عقد `admin.actions` |
| `classification_level` | `public` · `internal` · `confidential` · `top_secret` | ‏aql-trial | **Candidate** | مطابقة التصنيف الخماسي الكنسي تُفحص (أربع قيم هنا) — أي تعديل للتصنيف يتطلب ADR (سجل README) |
| `user_role` | `employee` · `supervisor` · `manager` · `system_admin` | ‏aql-trial | **Candidate** | أدوار **العرض التجريبي فقط** — نموذج الصلاحيات الحقيقي RBAC/ABAC (‏admin.roles/policies) لا أربعة أدوار ثابتة |
| `field_type` | `text` · `longtext` · `number` · `date` · `select` · `reference` · `user` · `attachment` · `classification` · `status` | ‏aql-trial | **Candidate** | تُفحص ضد كتالوج أنواع الحقول في تصميم P1 عند تفعيله |
| `workflow_node_type` | `start` · `task` · `condition` · `action` · `notification` · `end` | ‏aql-trial | **Candidate** | مرتبطة بانحراف الـ canvas (‏OD-P3-2) — انظر عقد `admin.workflows` §الانحرافات |
| `workflow_status` | `draft` · `published` | ‏aql-trial | **Candidate** | تُواءم مع دورة اعتماد التعريفات (‏SoD: معتمِد ≠ معرِّف — بطاقة 13) التي تقتضي حالة وسيطة على الأقل |
| `scope_inheritance` | `SELF_ONLY` (افتراضي) · `SELF_AND_DESCENDANTS` · `EXPLICIT_ORG_UNITS` | قرار مالك (R1) | **Accepted — قرار مالك (R1 2026-07-21)** | اختيار النطاق وتغييره يُسجَّلان بالتدقيق (ADR-0037) |

**قاعدة:** لا يضيف أي عميل/وكيل قيمة تعداد خارج هذا القاموس؛ الإضافة = تعديل عقد بنسخة جديدة.

**Related:** `../NAMING_AND_CONTRACTS_STANDARD.md` §1 · `../screens/admin.record_types.md` · `../screens/admin.actions.md` · `../screens/admin.workflows.md`
