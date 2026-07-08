# UI_STITCH_REFINED_PROMPTS.md — موجّهات Stitch المحسّنة

> **Version:** 1.0 — Proposed (v0.5) · **Date:** 2026-07-07 · **الموضع الهدف:** `ui/UI_STITCH_REFINED_PROMPTS.md`
> **يبني فوق:** `UI_STITCH_PROMPTS_BY_PHASE.md` (v0.4) — **لا يستبدله**. يعالج مشاكل التجربة الأولى (تخطيط حضري، شعارات غريبة، ازدحام، بلا قواعد تفاعل) بديباجة قفل هوية أقوى وقواعد تفاعل/ظهور صريحة، ويعيد صياغة الـ prompts السبعة الأكثر ازدحاماً.
> **مرجع الاستخدام:** كل prompt يُلصق كاملاً في Stitch بعد الديباجة العامة §1؛ ثم يُقيَّم بـ `UI_REFINEMENT_GATE_REVIEW.md`.

---

## §1 الديباجة المشتركة الموسّعة (تُلصق حرفياً قبل كل مجموعة G-x)

### §1.1 Project Identity Lock (يُنسخ EN كما هو — لا يُترجم)
> **PROJECT IDENTITY LOCK — read before generating anything:**
> This is the "**Local RAG Enterprise Platform**" — a **Governed Enterprise AI Command Center** for a formal government/enterprise organization. The UI is an internal, air-gapped, permission-gated work environment used by employees and administrators.
>
> **This system IS:**
> - a governed AI workspace where staff query institutional knowledge and act on records under strict permission, validation, approval and audit;
> - an admin control plane where administrators define record types, actions, workflows, permissions and knowledge sources;
> - a deterministic runtime renderer that displays governed screens generated from metadata.
>
> **This system IS NOT (do NOT generate any of these):**
> - a **city / urban / municipal planning** system — no maps, no zoning, no districts, no city dashboards;
> - a **public marketing landing page** — no hero, no CTA banner, no "Get started free";
> - a **public SaaS product** — no pricing page, no signup;
> - an **unrelated logo, brand or product mark** — no city seal, no ministry logo, no third-party logos (Microsoft, Slack, GitHub, Notion, Linear, Jira, Salesforce, Dify, NocoDB, Directus, Appsmith, Budibase, Open WebUI, ChatGPT, Claude, Gemini, etc.);
> - a **consumer chatbot** — no colored message bubbles, no playful avatars, no emoji reactions, no "AI Assistant" mascot;
> - an **end-user low-code builder** — the builder is admin-only, appears as a formal control plane, and never as a drag-and-drop toy for end users;
> - a **BI dashboard product** — no analytics gallery, no chart carousel, no "Insights" hero.
>
> If any prompt appears ambiguous, default to: **formal, austere, governmental enterprise tooling** — closer to an internal admin console than to any consumer app.

### §1.2 Visual Foundation (v0.4)
> Design language: "Calm Institutional Command". Surfaces near-white (#FFFFFF, #F4F6F9); ink #1B2430; single leading color deep institutional blue #1F4E79. **Reserved palettes** (never use for other purposes): five data-classification chips (gray #6B7280, blue #2F6FAD, amber #B7791F, orange #C2410C, dark red #8B1E1E — always icon + text + color), and violet #6D5BD0 used ONLY for an "AI-generated / مُولَّد" badge. Arabic-first typography (IBM Plex Sans Arabic style, Latin digits in data). Generous whitespace, 6–10px radii, hairline borders, two soft elevations, no gradients, no emojis, no consumer-app playfulness, WCAG AA. All layouts **RTL first**; English is secondary. Use **fictitious Arabic enterprise sample data** (invented ministry-style names). Output is a **static visual prototype for reference only — its code will not be used** in the final build.

### §1.3 Interaction Rules (v0.5 core)
> **Surface vocabulary — one meaning each, no overlap:**
> - **page** = full route, browser-back works, used for long tasks or formal records;
> - **tab** = view switch inside the same page;
> - **drawer** = side panel (start or end), for parallel reading or light interaction, ≤400px wide;
> - **modal** = centered blocking dialog, only for short critical decisions (typed/dual confirmation, HITL preview), ≤640px wide;
> - **panel** = fixed context region inside a page (not sliding);
> - **inline** = expand/collapse within the same row or card.
>
> **Selection rules:** long tasks → page. Parallel context → drawer end. Short critical decision → modal. Same data, different view → tab. Row detail → inline expand. Never mix (no page-in-modal, no modal-over-modal).

### §1.4 Visibility Rules (v0.5 core)
> **Every element carries one visibility tag:**
> `always` · `on-demand` · `by-permission` · `hidden-by-permission (HIDDEN-SERVER)` · `by-classification` · `admin-only` · `superadmin-only` · `ops-only` · `after-validation` · `after-approval` · `audit-visible` · `flag-gated` · `safe-mode-gated` · `state-gated`.
>
> **Rules:**
> - Elements a user is not allowed to see are NOT rendered at all (no ghost, no greyed-out placeholder).
> - Elements they may see but not act on right now render **disabled with a short i18n reason** (from a closed catalog).
> - Sensitive fields render as **`•••` with a small lock icon** — never real values.
> - "Audit trail" tab in the AI workspace has **no visible header** to users without `audit.view` — they don't know it exists.
> - Data-scope rule (RLS): rows outside the viewer's scope are silently excluded — do not show "N hidden results" counts to end users.

### §1.5 Progressive Disclosure Rules (v0.5 core)
> **Default is collapsed.** Show only what is essential to the primary decision on the screen (L0). Everything else is folded into "More", tabs, drawers, or moved to a full page.
> **Hard caps:**
> - ≤3 action buttons visible in any header (extras under "⋯ More");
> - ≤5 badges in any element header;
> - ≤7 fields visible by default in any form section or preview card (extras behind "More");
> - ≤7 columns visible by default in any table (extras behind a column picker);
> - each accordion/tab set opens exactly **one** section by default.
> **Send-to-Renderer triggers:** >10 result rows → "Open in list" (`run.list`); complex edits → "Open full form" (`run.form`); full record view → `run.detail`.

### §1.6 Component States to Include (min-set per canvas)
> For each component you design, include at least these states side by side: `default` · `loading (skeleton)` · `empty` · `error (with error_code + request_id shown)` · `permission-denied (surface-appropriate)` · `disabled with reason`. Add `masked`, `confirmation`, `approval`, `success`, `failed`, `audit-visible` when the component's role requires them.

### §1.7 Forbidden Outputs (repeat this list at the end of every prompt)
> Do NOT generate: city / municipality / urban / zoning artifacts; maps; landing pages; marketing sections; pricing; signup; unrelated logos or brand marks; colored chat bubbles; avatars; emojis in system text; endpoint URLs; API keys or secrets; drag-and-drop app builder canvases for end users; BI chart galleries; SaaS product framing; any real product's identity or layout.

### §1.8 Tool-Agnostic Prompt Rule (تُلصق حرفياً قبل كل prompt — لا تُترجم)
> **Tool-Agnostic Prompt Rule:** Any tool name mentioned in these prompts or documents, including Google Stitch, Stitch, Figma, Claude, Claude Design, Google AI Studio, design agent, or coding agent, refers only to a possible workflow tool used by the project team. Do not treat tool names as product features, UI labels, visible branding, platform dependencies, or required output format unless explicitly requested. If this prompt is used in another design generation tool, reinterpret "Stitch" as "the current design generation tool".
>
> **قاعدة حياد أسماء الأدوات:** أي اسم أداة مذكور في هذه البرومبتات أو الوثائق، مثل Google Stitch أو Figma أو Claude أو Google AI Studio أو Design Agent أو Coding Agent، يُقصد به أداة عمل محتملة يستخدمها فريق المشروع، وليس جزءاً من المنتج أو الواجهة أو الهوية أو المتطلبات التقنية. إذا استُخدم البرومبت داخل أداة تصميم أخرى، فافهم كلمة Stitch على أنها "أداة توليد التصميم الحالية".

---

## §2 المجموعات المُعاد صياغتها

### G1 — Design System (Reference Sheet)
**Goal:** Produce one style-guide canvas that becomes the visual contract for all other groups.
**Screens/Components:** color tokens (including the two reserved palettes), Arabic-first type scale, button hierarchy with the three confirmation variants (simple inline, **typed** modal, **dual** modal with countdown), the full badge taxonomy (lifecycle Draft→Active→RolledBack; approval Pending/Approved/Rejected/Returned; risk low→critical; five classification chips; violet "مُولَّد" badge; copyable audit-ref chip), sample table/form/modal/drawer/inline expand, and banners (environment strip, Safe-Mode strip, model-down strip).
**Default / Collapsed / Expanded:** show each component in its default state; for accordions/tabs, show one section open and the rest collapsed with counter chips indicating hidden fields.
**Visibility rules to demonstrate:** at least one `disabled-with-reason` button (with a real i18n reason like "الحالة الحالية لا تسمح"), one `masked` field, one `hidden-by-permission` example shown as a marker only ("this button would be here for admins — do not render for regular users").
**Progressive disclosure:** show the "More" pattern on a card header limited to 3 visible buttons + a "⋯" menu with 4 more.
**Must be visible:** the reserved-palettes swatches with explicit labels "RESERVED — classification only", "RESERVED — generated marker only"; RTL sample text with an LTR-isolated identifier inside.
**Must be hidden/collapsed:** any decorative illustration, marketing photography, non-token colors.
**Must never be generated:** icon sets from named products (Material logo, Fluent logo, Lucide brand), any city/urban imagery, any real logo.
**RTL/LTR:** all samples RTL; include one LTR-isolated identifier and one LTR-isolated SQL fragment.
**Output framing:** static reference sheet, prototype only; the design tokens will be re-implemented later in Tailwind + shadcn-style — no code emitted from this canvas is used.

> **Prompt (paste into Stitch after §1):**
> Produce a single Arabic-first style-guide canvas for a governed enterprise AI command center. Include: color tokens with two clearly labelled RESERVED palettes (five classification chips; one violet "مُولَّد" marker) that must never be used for other purposes; Arabic type scale with a Latin-digit sample; buttons in primary/secondary/tertiary/danger with three confirmation variants (simple inline, typed modal, dual modal with countdown); the full badge taxonomy (lifecycle, approval, risk, classification, generated, copyable audit-ref); one table sample (5 columns, one row selected), one form sample (one section open, two collapsed with field-counter chips), one modal sample (short critical decision), one drawer-end sample (parallel reading), one inline-expand sample; three banners (non-production environment strip, Safe-Mode strip, model-down strip). Show at least: one disabled button with a real i18n reason, one masked field with a lock icon, one card header limited to 3 buttons with a "⋯ More" menu. RTL throughout; one LTR-isolated identifier inside Arabic text. No product imitation; no gradients; no emojis; static reference only. **Forbidden outputs:** [paste §1.7 list].

---

### G13 — Runtime Renderer Templates (list / form / detail / entity profile)
**Goal:** Prove the deterministic runtime renderer works as **generic templates** across any entity, not as bespoke screens per record type.
**Screens/Components:** `run.list`, `run.form`, `run.detail`, `profile.entity`.
**Default:** list shows 5–7 columns + first row selected + a simple search + filter chip strip; form opens with the primary section only; detail shows classification chip + workflow-state chip + 3 header actions + one active tab; profile shows minimal identity block + timeline collapsed.
**Collapsed by default:** advanced filters (open in drawer end), column picker, non-primary form sections (with field-counter chips), extra action buttons under "⋯", audit side panel, activity timeline older than 30 days.
**Expanded on demand:** section click, tab click, drawer opens.
**Visibility rules:** buttons outside permission are HIDDEN-SERVER; row-actions gated by state show `disabled-with-reason`; at least one field per template is `masked` (•••); audit-side-panel header appears only for viewers with `audit.view`.
**Progressive disclosure:** row click → drawer end preview → "فتح كامل" → page detail; complex edits → page form; result >10 rows in a preview → "Open in list".
**Must be visible:** in list — a masked cell and a workflow-state chip on a row; in form — a validation error pinned to a field and a summary at top; in detail — a "⋯ More" menu with one disabled entry showing its reason; in profile — inheritance-of-strictest classification chip.
**Must be hidden/collapsed:** all secondary tabs, all audit content for non-authorized viewers, all raw endpoints, dev-only debug data.
**Must never be generated:** entity-specific screens ("Contracts Screen", "Employees Screen") — instead show **the same template skinned with two different fictitious entities side by side** to prove genericity.
**RTL/LTR:** columns start-end ordered; numeric/id columns LTR-isolated inside RTL row.
**Output framing:** four generic templates as static reference, not four separate apps.

> **Prompt (paste into Stitch after §1):**
> Produce four generic runtime renderer **templates** for a governed enterprise system — not bespoke apps per entity. Show each template twice, skinned with two different fictitious Arabic entities (e.g., "طلبات إجازة" and "عقود موردين") to prove the same template renders both.
> Template A — list: 5–7 columns, one row selected, simple search + filter chips (advanced filters live in a drawer end, closed); at least one row shows a workflow-state chip ("بانتظار الاعتماد") and at least one cell is masked with a lock icon.
> Template B — form: primary section open, two other sections collapsed with field-counter chips; a validation error pinned to a specific field plus an error-summary bar at the top with a jump-to-field link; a "حقول متقدمة" fold inside the primary section.
> Template C — detail: header with classification chip + workflow-state chip + 3 primary action buttons + a "⋯ More" menu revealing 4 more actions with one entry `disabled-with-reason` ("الحالة الحالية لا تسمح"); a right-side audit-trail panel collapsed (title visible only if the demo persona has `audit.view`).
> Template D — entity profile: identity block + timeline collapsed by default + inherited-strictest classification chip.
> RTL; Latin-digit numeric columns LTR-isolated inside RTL rows; no entity-specific chrome; no analytics; no maps; no logos. Static reference only. **Forbidden outputs:** [paste §1.7 list].

---

### G3 — AI Workspace Shell (ws.main) — **NOT a chatbot**
**Goal:** Design the workspace as an enterprise command environment where the conversation is one operational channel, not the product.
**Screens/Components:** three-zone layout — start-side session rail (collapsed to icons), central `ws.thread` (formal rows with hairline separators, **not colored bubbles**), end-side context panel with four tabs (Citations · Related · Attachments · Audit), a bottom-anchored `ws.composer` with a knowledge Scope selector.
**Default:** thread shows a **first-empty state listing this user's actual capabilities** (bilingual list); session rail collapsed to a strip of dots; context panel tabs all collapsed to headers; composer with a subtle placeholder; scope selector chip = "إدارتي".
**Collapsed by default:** all context tabs (headers only); the audit tab header is **not rendered at all** for users without `audit.view`.
**Expanded on demand:** context tab opens automatically when new content arrives (e.g., citations); session rail expands on hover.
**Visibility rules:** action suggestions the user cannot execute are not proposed at all; a refusal-permission card uses a shield icon and generic wording (never leaks policy text); a refusal-evidence card ("No-Guessing") lists which scopes were searched and why evidence is insufficient plus two safe next actions.
**Progressive disclosure:** show three thread states side by side — first empty · streaming (subtle pulse) · **full deterministic mode** (model-down banner across the top, composer switched to a keyword-search variant, plus a small "action launcher" palette listing this user's permitted actions).
**Must be visible:** the violet "مُولَّد" chip on every model turn; citation chips inline in the answer text with a numeric locator; a small copyable audit-ref receipt on any executed result; the environment strip if non-production.
**Must be hidden/collapsed:** the audit context tab for non-authorized personas; any avatar / mascot / persona for the AI; any suggestion or shortcut that resembles a consumer messenger.
**Must never be generated:** colored chat bubbles; playful avatars; emoji reactions; "AI Assistant" branding; a marketing hero above the composer; social buttons; any city / urban visual; any product logo.
**RTL/LTR:** message alignment start; identifiers and SQL fragments LTR-isolated within Arabic text.
**Output framing:** three side-by-side states of one shell, not three separate apps. Static reference only.

> **Prompt (paste into Stitch after §1):**
> Design **ws.main** as an enterprise command workspace — explicitly not a chat application. Three-zone RTL layout: start-side session rail collapsed to a thin dotted strip; central thread rendered as formal aligned rows separated by hairlines (never colored bubbles); end-side context panel with four collapsed tab headers (Citations, Related records, Attachments, Audit trail); a bottom composer with an attach control and a "knowledge scope" chip selector limited to permitted sources.
> Show three side-by-side states of the same shell:
> 1) First-empty state listing what this specific persona can actually do (bilingual capabilities list, no marketing copy).
> 2) Streaming state with a subtle pulse indicator; a model turn shows a violet "مُولَّد" chip; inline citation locators point to a partially-open Citations tab.
> 3) Full **deterministic mode** — a red-hairline model-down banner across the top; the composer switches to a keyword-search variant; an "action launcher" palette below the composer lists this persona's permitted actions with an explanatory line: "كل العمليات متاحة عبر القوائم".
> The Audit trail tab header must be **absent** in personas without audit permission — do not render a greyed placeholder. No avatars, no chat bubbles, no emoji, no marketing hero, no logos, no city imagery. RTL; identifiers LTR-isolated. Static reference only. **Forbidden outputs:** [paste §1.7 list].

---

### G4 — Action Cards (governed inside the thread)
**Goal:** Show the governed action contract as a card storyboard inside the thread — not as loose buttons or free text.
**Screens/Components:** `card.action_preview`, `card.result`, `card.refusal_permission`, `card.refusal_evidence`, `card.sql_answer`, oversized-result summary card.
**Default:** preview card header (action name + risk chip + classification chip) + one-line declared-effect sentence ("سيتم إنشاء سجل عقد جديد وربطه بالمشروع…") + **only the required fields** in an editable grid + a confirm button.
**Collapsed by default:** optional fields folded behind "مزيد"; a dependency-impact line collapsed; irreversibility warning appears only when applicable.
**Expanded on demand:** clicking "مزيد" reveals optional fields; hover shows tooltip on a disabled control.
**Visibility rules:** actions the user cannot execute never appear as suggestions; the refusal-permission card never quotes policy text (generic phrase "يتطلب صلاحية {اسم عام}"); sensitive input fields render as masked "•••" with a lock; the SQL panel shows the query text always, LTR-isolated in mono font, above the result.
**Progressive disclosure:** show a full S3→S9 storyboard as separate cards on one canvas: PROPOSED → CLARIFYING (asks for one missing field only, not a whole form) → VALIDATED → CONFIRMING → PENDING_APPROVAL → EXECUTING → SUCCEEDED (result card).
**Must be visible:** the risk chip and classification chip on every card header; the "مُولَّد" chip on the AI-turn wrapper (not on the card body); the audit-ref receipt on the result card; the two safe next actions on the refusal-evidence card.
**Must be hidden/collapsed:** raw endpoint URLs; the full policy text; every field of the target entity (only required + expandable optional).
**Must never be generated:** a big "one-click execute" button without a governed preview; an "AI decides on your behalf" tone; a fun success animation; a share/like/report button.
**RTL/LTR:** labels RTL; identifiers, dates, and IDs LTR-isolated.
**Output framing:** one canvas, seven cards side by side, telling the S3→S9 storyboard.

> **Prompt (paste into Stitch after §1):**
> Produce a single canvas showing the governed action-card storyboard inside a workspace thread. Seven cards side by side in Arabic RTL:
> Card 1 — **PROPOSED**: preview card for a fictitious action like "إنشاء عقد مورد جديد"; header shows risk chip (medium), classification chip (داخلي), and the AI-turn "مُولَّد" wrapper; body shows only 4 required fields with a "مزيد" fold; footer shows a one-line declared effect and a "تأكيد" button.
> Card 2 — **CLARIFYING**: same preview but one field is empty and highlighted with a single targeted question below it ("ما رقم المشروع المرتبط؟"), not a generic "please provide more info".
> Card 3 — **VALIDATED**: same preview but a validated tick appears near the confirm button; a masked sensitive field remains "•••" with a lock.
> Card 4 — **CONFIRMING**: a modal appears over the card (typed confirmation for high-risk variant).
> Card 5 — **PENDING_APPROVAL**: the card body is replaced by a status chip "بانتظار الاعتماد" and a link "فتح البند" to the approvals surface; the confirm button is gone.
> Card 6 — **EXECUTING**: a subtle progress line replaces the confirm button; card is otherwise unchanged.
> Card 7 — **SUCCEEDED**: result card with a green edge, a link to open the created record, a copyable audit-ref chip, and (if supported) an "Undo" chip inside the retention window.
> On the same canvas also include, off to the side, two refusal cards: **permission-denied** (shield icon, generic wording, two safe next actions "طلب وصول"/"إنشاء مهمة لمن يملكها") and **insufficient-evidence No-Guessing** (lists which scopes were searched and why evidence is insufficient, plus two safe next actions), and one **SQL answer card** with the query text always visible in an LTR-isolated mono block above a small result table.
> RTL; no colored bubbles; no emojis; no share/like/report; no consumer chatbot chrome; no logos. Static reference only. **Forbidden outputs:** [paste §1.7 list].

---

### G5 — Admin Console Shell (Control Plane)
**Goal:** Establish the admin console as a **control plane**, distinctly different from the workspace — formal, dense, version/status forward.
**Screens/Components:** console shell (start-side grouped sidebar filtered by permission, top admin-search bar, environment strip, optional Safe-Mode strip), `admin.dashboard`, `admin.features`.
**Default:** dashboard with ≤4 tiles (pending approvals · failed jobs · health summary · recent policy changes) + a bilingual admin search; sidebar shows only permitted groups; a subtle amber environment strip at the top for non-production; features screen lists capabilities with dependency-impact side panel.
**Collapsed by default:** deep operational details (all live behind links to dedicated screens); dependency graph collapses to a summary chip until a change is proposed.
**Expanded on demand:** a dependency-impact dialog with typed confirmation appears when a feature is disabled; the Safe-Mode banner replaces the environment strip when active.
**Visibility rules:** every sidebar group carries a permission tag — hide entire groups the persona cannot access; A10 protected items appear locked (grey, permanent lock icon, tooltip "عناصر أساسية — غير قابلة للتعطيل") and the server rejects any attempt regardless.
**Progressive disclosure:** dashboard shows only 4 tiles maximum; features screen shows a compact list with a right-side impact drawer, not a wall of toggles.
**Must be visible:** an environment strip (production vs non-production made obvious); the version/status bar on definition-style screens (even if empty); a permanent visual distinction between "editable admin surfaces" and "read-only D9 surfaces" (config profiles, ops status).
**Must be hidden/collapsed:** any secrets, endpoints, GPU / replicas / container lifecycle controls; any BI chart gallery.
**Must never be generated:** an admin "welcome hero"; a marketing banner; a chatbot floating widget in the console; product logos; a "dark mode toggle" (deferred).
**RTL/LTR:** all Arabic; version tags and identifiers LTR-isolated.
**Output framing:** one canvas showing the shell + dashboard + features screen with a dependency-impact drawer open.

> **Prompt (paste into Stitch after §1):**
> Design an admin **control plane** shell for a governed enterprise system, distinctly different from a consumer app. RTL layout: start-side grouped sidebar (each group carrying an inline permission tag; hide entire groups the persona cannot access), a top admin-search bar with a "بيئة: تجربة" amber environment strip above it.
> Show `admin.dashboard` with exactly 4 compact tiles: pending approvals, failed ingestion jobs, health summary (green/amber/red), recent policy changes — each tile shows only a number and a title, and links to its dedicated screen. No charts, no widgets, no hero.
> Show `admin.features` in the same canvas: a compact list of capabilities (fictitious Arabic names), each with an on/off state and a small dependency count; at least three items are permanently locked grey ("عناصر أساسية — غير قابلة للتعطيل"); a right-side drawer is open showing "أثر التعطيل" for one selected item with a dependency list and a typed-confirmation button.
> Include a subtle Safe-Mode banner variant off to the side, showing what the shell looks like when Safe Mode is on (most actions become disabled with a shared reason "الوضع الآمن مفعَّل").
> No secrets, no endpoints, no GPU controls, no chatbot widget, no hero, no logos, no dark-mode toggle. Static reference only. **Forbidden outputs:** [paste §1.7 list].

---

### G7 — Metadata / Actions (Control Plane — **NOT a low-code builder for end users**)
**Goal:** Present the record-type builder, action registry and migrations review as **admin control plane surfaces** with versioned lifecycle, not as a drag-and-drop app builder.
**Screens/Components:** `admin.record_types` (list + Builder page), `admin.actions` (list + action-contract editor page), `admin.migrations` (proposal + risk report + SoD approval).
**Default:** each list is compact (name, lifecycle status chip, version tag); the Builder opens on a page with a lifecycle bar and one active tab; the action-contract editor opens on a page with the 13-field contract as a structured form (labelled sections, not free JSON).
**Collapsed by default:** the Builder's Fields tab shows a table of fields but not their full property panel; Policies tab shows RLS scope + FLS matrix summary, editable in a drawer; Validation report and Version diff live in drawers.
**Expanded on demand:** clicking a field opens its property drawer; "diff" opens a drawer comparing two versions with neutral additions/removals; a simulation panel "من سيرى هذا الزر؟" opens as a drawer with an explained, labelled "محاكاة — لا أثر" result.
**Visibility rules:** the entire Builder is admin-only; the "Approve" button is disabled with a visible SoD reason for the same person who created the version; the "Activate" button is disabled until Approved; migrations screen requires a different approver from the proposer (SoD visibly enforced).
**Progressive disclosure:** show the same visual lifecycle bar (Draft → Validated → Approved → Active → RolledBack) on all three (record-type, action, migration); never surface every field of the record type at once — Fields tab is a table with a property drawer.
**Must be visible:** the lifecycle bar; a version chip; the approver line (who approved, when); a "محاكاة" call-to-action on both record-type and action editors.
**Must be hidden/collapsed:** any free-code textarea; any scripting IDE; any WYSIWYG page painter; the full JSON of the contract (structured form instead).
**Must never be generated:** a Webflow / Bubble / Wix-style visual painter; a "publish to public URL" button; a marketplace section; product logos; a "drag components here" empty state that looks like a consumer builder.
**RTL/LTR:** labels RTL; ASCII identifiers (action_id, screen_id, field names) LTR-isolated in mono font.
**Output framing:** one canvas showing the three screens as an admin control plane, not as an app builder.

> **Prompt (paste into Stitch after §1):**
> Design three **admin control-plane** screens for defining metadata and governed actions — strictly not an end-user low-code builder.
> 1) `admin.record_types` list + Builder page. The list is compact (name, lifecycle status chip, version tag). The Builder page has a lifecycle bar (Draft → Validated → Approved → Active → RolledBack), a version chip, and three tabs: Fields (a compact table of fields with a property drawer on click — do NOT show every property inline), Policies (a summary of RLS scope + FLS matrix with an "edit in drawer" affordance), Documentation (read-only). The "اعتماد" button is disabled with a visible SoD reason for the current persona. Include a small "محاكاة: من سيرى هذه الشاشة؟" call-to-action opening a labelled "محاكاة — لا أثر" drawer.
> 2) `admin.actions` list + action-contract editor page. The list shows fictitious action_ids like `record.create`, `workflow.approve`, `connector.tool.act` with risk chips. The editor is a **structured form** presenting the governed action contract in labelled sections (Identity, Permission, Inputs &amp; Validation, Risk &amp; Confirmation, Effect (declared, chosen from a closed list), Audit event) — never a free code textarea, never a WYSIWYG canvas. Include an inline "من سيرى هذا الزر؟" simulation opening in a drawer.
> 3) `admin.migrations` review screen. Shows a proposal card with a risk report, an approver line, and a typed-confirmation "اعتماد" button; the approve button is disabled for the same persona who proposed (SoD visibly enforced).
> RTL; ASCII identifiers LTR-isolated in mono. No drag-and-drop canvas, no free-code IDE, no publish-to-URL, no marketplace, no logos, no consumer builder empty states. Static reference only. **Forbidden outputs:** [paste §1.7 list].

---

### G9 — RAG / Retrieval Tester (admin.retrieval_tester + surrounding knowledge admin)
**Goal:** Show the knowledge-admin retrieval tester as an **admin verification tool with an evidence-sufficiency verdict**, not as an end-user AI answer surface.
**Screens/Components:** `admin.retrieval_tester` primary; small strip references to `admin.rag_sources` and `admin.ingestion` for context.
**Default:** a query input, a small "نطاق: صلاحياتي" chip (the tester runs within the admin's own permissions, not elevated), a "تشغيل" button, and an empty results area with an explanatory line ("سيتم عرض النتائج ومحدد الكفاية بعد التشغيل").
**Collapsed by default:** advanced parameters (top-k, evidence threshold) live in a drawer end; per-result provenance detail lives in a drawer end; source and ingestion admin are linked, not embedded.
**Expanded on demand:** clicking a result opens a provenance drawer (document, page/segment locator, classification chip, origin tag "مستند/سجل/OKF"); clicking "إعدادات متقدمة" opens a parameters drawer.
**Visibility rules:** results outside the admin's own scope do not appear (RLS applies to the tester too); sensitive snippets are masked; the tester screen is `admin-only`.
**Progressive disclosure:** show two side-by-side result states — one **"كافٍ"** (green banner + 4 results + a note that a workspace answer would be permitted) and one **"غير كافٍ"** (amber banner + 2 weak results + a note that a workspace answer would be **refused** as No-Guessing).
**Must be visible:** the evidence-sufficiency banner (always the primary verdict, above the results list); the "admin — داخل صلاحياتك" chip; provenance locators for every visible result; a link to `admin.rag_sources` and `admin.ingestion` for follow-up.
**Must be hidden/collapsed:** any composed workspace-style answer — this is the retrieval tester, it shows chunks and verdicts, it does NOT produce a chat answer; advanced parameters until requested.
**Must never be generated:** a public search product framing; a "share results" or "rate this answer" widget; endpoint URLs; a "clear tokens" control; product logos.
**RTL/LTR:** query and results RTL; document identifiers, page numbers, offsets LTR-isolated.
**Output framing:** one canvas showing the tester twice (sufficient / insufficient verdicts) plus a small strip showing the surrounding admin.rag_sources and admin.ingestion screens compact.

> **Prompt (paste into Stitch after §1):**
> Design the admin **retrieval tester** as a verification tool with a prominent evidence-sufficiency verdict. RTL layout: a query input at the top, a "نطاق: صلاحياتي" chip beside it, a "تشغيل" button, and below it the results area.
> Show two side-by-side runs of the tester on the same canvas, using fictitious Arabic policy queries:
> Run A — **"كافٍ"**: a green sufficiency banner across the top of the results area ("الأدلة كافية — يمكن للـ Workspace تقديم إجابة مسنودة"), followed by 4 result cards each with a title, a precise locator (وثيقة / صفحة / فقرة), a classification chip, an origin tag (مستند / سجل / OKF), and an "افتح" link that would open a provenance drawer end.
> Run B — **"غير كافٍ"**: an amber sufficiency banner ("الأدلة غير كافية — سيرفض الـ Workspace الإجابة (No-Guessing)"), followed by 2 weak result cards; one result card has a masked snippet (•••) demonstrating classification masking.
> To the side, show a small strip preview of `admin.rag_sources` (5 fictitious sources with scope tags) and `admin.ingestion` (a job list with 3 running, 1 failed with an error_code, 2 done) — both compact, not embedded functionality.
> Do NOT produce a chat answer, a "share" or "rate" widget, a public search product framing, or any endpoint URLs. Do NOT show sources by full URL. Static reference only. **Forbidden outputs:** [paste §1.7 list].

---

### G14 — Run &amp; Execution (runs.list · runs.detail) — سطح مراقبة مؤسسي، **ليس console** — (Δ v0.6)
**Goal:** توليد سطحَي مراقبة التنفيذ المحكوم: قائمة التشغيلات وتفصيل تشغيل بخط زمني وبوابات اعتماد وأدلة — **enterprise monitoring surface** يقرأ سلسلة التدقيق، لا سطح تنفيذ حر.
**Screens/Components:** runs.list · runs.detail · Run Timeline (بفروع متوازية وعقدة دمج) · Run Timeline Step · Step Drawer · Tool/Action Call Row · Run Output Panel (المخرجات/الاستشهادات/التدقيق-المخوّل) · عقدة بوابة Approval/HITL داخل الخط.
**Default / Collapsed / Expanded:** القائمة بفلتر «تشغيلاتي النشطة» و≤7 أعمدة؛ التفصيل: رأس ≤3 أزرار سياقية + الخط الزمني L0 + لوحة المخرجات مطوية الرؤوس؛ تفاصيل الخطوة inline سطرين ثم Step Drawer؛ السجل المُهيكل والاستشهادات والتدقيق مطوية.
**Visibility rules:** رأس تبويب «التدقيق» **غائب كلياً** لغير audit.view؛ digest المدخل/المخرج مقنَّع بالتصنيف؛ عنصر مخرَج أعلى من clearance يظهر «عنصر مقيّد» بلا فتح؛ retry/cancel وسمها state-gated؛ Safe Mode يجمّد غير A10 بسبب موحّد.
**Progressive disclosure:** بنية الخط مرئية لصاحب التشغيل والتقنيع للمحتوى؛ المخرَج الضخم **auto-offload إلى ملف محكوم** (صف «مخرَج كبير — ملف») — لا inline dump.
**Must be visible:** حالة partial بملخص «نجح X/Y — فشلت الخطوة Z» · «إعادة من الخطوة» على خطوة فاشلة مؤهلة · modal إلغاء typed · عقدة بوابة paused برابط «فتح البند» (⇒ queue.approval_detail — القرار هناك حصراً) · روابط «فتح المراجعة» ⇒ reports.review و«فتح في التدقيق» ⇒ admin.audit بفلتر correlation · مرجع تدقيق قابل للنسخ.
**Must be hidden/collapsed:** تبويب التدقيق لغير المخوّل · السجل المُهيكل افتراضياً · أي معاملات مزوّد/نموذج (تُدار في G10).
**Must never be generated:** **terminal UI · command console · pentest dashboard · tool-hacking UI · raw command output · أي cybersecurity-specific UI** (لا فحص/ثغرات/أهداف/attack-surface) · secrets · endpoints · Base URL/API Key · «تنفيذ حر» أو حقل أوامر · شعارات أدوات.
**Affirmations (تُذكر نصاً في الـ prompt):** enterprise monitoring surface · no free execution · action steps are **governed enterprise actions only** (كل خطوة تحمل action_id/مرجع تعريف معلناً) · القرارات على سطح الاعتماد الرسمي · المصدر الوحيد للسلسلة هو التدقيق القائم.
**RTL/LTR:** الخط الزمني RTL؛ run_id والمعرّفات والمدد LTR-isolated بخط mono.
**Output framing:** canvas واحد يعرض runs.list (نشطة/فارغة) + runs.detail بحالات: running · paused-على-بوابة · failed-مع-إعادة-من-خطوة · partial؛ static reference only. (قاعدة §1.8 Tool-Agnostic سارية.)

> **Prompt (paste into the design generation tool after §1):**
> Design an **enterprise run-monitoring surface** for a governed platform — explicitly **not** a terminal, not a command console, not a pentest or security dashboard. Two RTL screens on one canvas:
> 1) **runs.list**: a formal table (definition name, initiator, status chip, started, duration, progress x/y, type), default filter "تشغيلاتي النشطة", advanced filters in a closed end-drawer; an empty-state variant listing what this persona may launch; a typed-confirmation cancel modal triggered from a row.
> 2) **runs.detail** (full page): header with definition name + version, an LTR-isolated run_id, initiator, status chip, progress, and at most 3 contextual actions (Cancel while running; Retry-from-step when failed; "⋯" holds Compare and Open-in-audit). Main area: a vertical **execution timeline** with two parallel lanes merging at a join node; each step row shows index, Arabic step name, a type icon (agent / validation / governed action / connector), status chip, duration; one failed step shows an error code and an enabled **"إعادة من هذه الخطوة"**; downstream steps show "skipped". Include one distinguished **approval/HITL gate node** in paused state with a "فتح البند" link (the decision happens on the formal approvals surface, not here). A **Step Drawer** (end) shows masked input digest, output digest, and one Tool/Action Call Row whose large output is offloaded: "مخرَج كبير — ملف" with an open-file link — never raw dumps. An **Output Panel** (end, collapsed tabs): المخرجات (each item with classification chip + open link to its own surface, one item shown as "عنصر مقيّد" not openable), الاستشهادات, and an **audit tab whose header exists only for the authorized persona**, rendering the correlation chain with a "فتح في التدقيق" deep-link. Show a **partial-completion** summary banner "نجح 4/6 — فشلت الخطوة 5 (سبب)" and a link "فتح المراجعة" to the report-review surface.
> Every step is a **governed enterprise action step** with a declared effect — no free execution, no command input, no shell text, no green-on-black styling, no secrets, no endpoints, no Base URL or API key anywhere. Fictitious Arabic enterprise data; Latin digits LTR-isolated; static reference only. **Forbidden outputs:** [paste §1.7 list] + terminal UI, command console, pentest dashboard, tool-hacking UI, raw command output, any cybersecurity-specific UI.

---

## §3 قواعد إقفال هذا الملف
1. **الديباجة §1 كاملة تسبق كل prompt** — بما فيها Identity Lock EN و§1.7 المكرَّرة في نهاية كل prompt و**§1.8 Tool-Agnostic Prompt Rule** الملصقة قبل كل prompt.
2. **لا تُوَلَّد مجموعة خارج هذه الثماني (G1 · G13 · G3 · G4 · G5 · G7 · G9 · G14) الآن.** بقية المجموعات من v0.4 تبقى صالحة لكن تُعاد صياغتها بنفس هذه القواعد قبل تشغيلها في Stitch.
3. **مخرجات Stitch مرجع بصري فقط** — لا كودها يدخل ريبو التنفيذ (سياسة `UI_REFERENCE_USAGE_POLICY.md`).
4. **البيانات وهمية عربية** فقط — قاعدة الأداة الخارجية §4 من سياسة المراجع سارية.
5. **الفحص بعد التوليد** إلزامي عبر بنود القسم D في `UI_REFINEMENT_GATE_REVIEW.md` قبل قبول أي canvas.
