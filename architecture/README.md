# architecture/README.md — فهرس وثائق المعمارية

> **Version:** 1.2 (v0.8: تصحيح مرجعَي الإصدار v2.0 → v2.1) · **Status:** Current / Accepted · **Date:** 2026-07-10
> **Purpose:** دليل موقع محتوى المعمارية الآن، وخريطة استخراج الوثائق الفرعية لاحقاً.

## أين تعيش المعمارية الآن (المصادر المعتمدة)
المحتوى المعماري الكامل **موحَّد حالياً** في:
1. `catalogs/Feature_Technical_Architecture_Catalog.md` (v2.1) — الطبقات، الخدمات، البيانات، الصلاحيات، الوكلاء، RAG/SQL/Media، الإعداد/البروفايلات، التكاملات، التدقيق/المراقبة، الأمن.
2. `methodology/Spec_Driven_Modular_Monolith_Methodology.md` (v2.1) — الحدود، الـ Modules (36)، مصفوفة الاعتماد، النشر والنقل.
3. **المخطط المعتمد بصرياً:** `architecture/diagrams/Full_Stack_Architecture.svg` (يوضع هنا عند الرفع) — كل الطبقات + Operations Plane + حالات core/optional/protected.

**تحديث D1–D9 (2026-07-04):** المعمارية تشمل الآن صراحةً: **React+Vite SPA مستقلة** تستهلك OpenAPI/SDK · التجريدات **Cache/Queue/Lock** (افتراضي memory/PostgreSQL؛ Valkey optional-ready) · **ObjectStorageProvider** (افتراضي filesystem؛ MinIO|SeaweedFS لاحقاً) · **Observability Baseline** (Audit-PG + JSON logs + Log Viewer + Health + Error Catalog + IDs + /metrics اختياري؛ OTel adapter مستقبلاً) · نموذج **GitHub الآن → نقل مغلق موقّع** وGit داخلي كخيار مستقبلي · سياسة **Reference-aware clean implementation**. **المخططات SVG لم تُحدَّث بصرياً بعد** — `Full_Stack_Architecture.svg` يبقى المعتمد مفهومياً والنص أعلاه يحكم فروقه؛ تحديثها البصري مُدرج مع استخراج وثائق المعمارية لاحقاً (لن نرسم رسوماً شكلية لمجرد الإكمال).

## الوثائق الفرعية (تُستخرج لاحقاً — عند زرع specs، مهمة T-0.1.3)
| الملف | مصدر الاستخراج | ملاحظة |
|---|---|---|
| architecture.md | الكتالوج §1/§2 + المنهجية §3 | نظرة عامة موحّدة |
| data-architecture.md | الكتالوج §3.1 + Data sections | القواعد الأربع، درجات الفصل، الترحيل المحكوم |
| permission-architecture.md | الكتالوج (Permission) | سلسلة الإنفاذ، default-deny، RLS/FLS |
| agent-architecture.md | الكتالوج §10-mapping + Agents | الوكلاء وعقودهم وmodel-per-agent |
| orchestration.md | سيناريوهات التدفق | Orchestrator/Gates/No-Guessing |
| media-architecture.md | الكتالوج §3.6/§18-flows | pipeline الوسائط وRAG-over-media |
| integration-architecture.md | الكتالوج §3.7 + App Store | MCP/API/Webhooks/DB + المتجر |
| deployment-architecture.md | المنهجية §17 + الكتالوج §8 | Portability/Profiles/Bundles/offline |
| configuration-and-profiles.md | المنهجية §16 + الكتالوج §8 | المفاتيح والنطاقات وstatic/dynamic |

## المخططات (diagrams/)
- **معتمد:** `Full_Stack_Architecture.svg`.
- **Superseded (لا تُستخدم للتنفيذ):** `system-architecture-v1.svg` و`Component_Diagram.svg` القديمان (طبقة العرض فيهما سابقة لقرار Enterprise UI) — تُنقل إلى `superseded/`. المخططات المكمّلة (Agent/Deployment) صالحة كمرجع تاريخي وتُحدَّث عند الاستخراج.

**قاعدة:** أي تعديل معماري = تحديث المصدر المعتمد + ADR عند اللزوم؛ الوثائق المستخرجة لا تتعارض مع الكتالوج/المنهجية (Authority Order).

- `PROVIDER_MODEL_SECRET_CONFIG_SPEC.md` — عقد المزوّد/النموذج/السر بين Config/Ops والـ Backend والواجهة (D9/الخيار A — v0.7).
