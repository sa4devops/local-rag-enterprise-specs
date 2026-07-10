# Phase Design Package — Repository Placement Plan (README)

> **Version:** 1.0 · **Date:** 2026-07-06 · **Status:** Proposed — تصبح الحزمة كلها **Accepted** باعتماد المالك وإصدار v0.3.
> **قاعدة:** هذه الحزمة **تصميم فقط** — لا كود، لا تنفيذ، لا تعديل GitHub ضمن إنتاجها. الرفع يقوم به المالك.

## 1) مواضع الملفات داخل specs repo (`local-rag-enterprise-specs`)
| ملف الحزمة | الموضع الهدف |
|---|---|
| phases/PHASE_MASTER_PLAN.md | `/phases/PHASE_MASTER_PLAN.md` |
| phases/designs/phase-1..8-*.md (8 ملفات) | `/phases/designs/…` (مجلد جديد) |
| phases/BACKLOG_DEFERRED_SCOPE.md | `/phases/BACKLOG_DEFERRED_SCOPE.md` |
| methodology/agent-execution-model.md | `/methodology/agent-execution-model.md` |
| هذا الملف (README الحزمة) | لا يُرفع كما هو — محتواه إجرائي؛ يُنقل ملخصه إلى رسالة الـ Release |

**ملاحظة:** تصميم Phase 0 القائم `/phases/phase-0-foundation-full-stack-skeleton.md` (v2.1) **يبقى كما هو** — الخطة الرئيسية تشير إليه ولا تعيد كتابته.

## 2) ترتيب الرفع (commits مقترحة على main)
1. `Add phase master plan` → PHASE_MASTER_PLAN.md
2. `Add phase designs 1-8` → مجلد designs/ كاملاً
3. `Add deferred scope backlog` → BACKLOG_DEFERRED_SCOPE.md
4. `Add agent execution model` → methodology/agent-execution-model.md
5. `Update package checklist and docs structure for phase design package` → التحديثات الوصفية في §3
6. إنشاء الـ Release (§4) ثم تحديث `docs/SPEC_SOURCE.md` في platform إلى الوسم الجديد (المصدر الوحيد للرقم).

## 3) تحديثات مطلوبة على وثائق قائمة (تُنفَّذ عند الرفع — موصوفة هنا فقط)
- **PACKAGE_CHECKLIST.md → v1.2:** إضافة صفوف: PHASE_MASTER_PLAN.md · designs/ (8 ملفات) · BACKLOG_DEFERRED_SCOPE.md · agent-execution-model.md — كلها "جاهز للرفع ✅ / التنفيذ رهن بواباته".
- **github-docs-structure.md:** إضافة `phases/designs/` و`phases/PHASE_MASTER_PLAN.md` و`phases/BACKLOG_DEFERRED_SCOPE.md` و`methodology/agent-execution-model.md` إلى الشجرة مع وصف سطري.
- **phases/phase-roadmap.md → v1.2:** إضافة سطر واحد تحت «قواعد عامة»: «التفصيل المُلزم لكل مرحلة: `PHASE_MASTER_PLAN.md` + `designs/phase-N-*.md`؛ بطاقات المهام تُولَّد عند تفعيل كل مرحلة.» (لا تغيير آخر).
- **handoff/handoff.md:** إدخال **H-0003** يوثّق إنتاج الحزمة واعتمادها.
- **platform/docs/SPEC_SOURCE.md:** تحديث الوسم المعتمد إلى v0.3 (وREADME/AGENTS يبقيان يحيلان إلى SPEC_SOURCE).

## 4) الـ Release المقترح
- **Tag:** `v0.3-phase-design-package` · **Title:** Phase Design Package v0.3 · **Type:** Pre-release
- **Description (معنىً):** Adds the complete phase design package: master plan, individual designs for Phases 1–8 (Phase 0 design pre-existing), deferred-scope backlog, and the agent execution model. Task cards are generated at each phase activation. No implementation code.

## 5) قواعد ما بعد الاعتماد
باعتماد v0.3: حالة كل تصميم تتحول **Accepted for Design** · تفعيل أي مرحلة = جلسة **Clarify خفيفة** (إغلاق ODs تصميمها) + جلسة **Tasks** (توليد البطاقات) ثم التنفيذ ببطاقة/جلسة وفق agent-execution-model · أي تعديل لاحق على تصميمٍ يرفع نسخته ويستلزم Release جديداً.
