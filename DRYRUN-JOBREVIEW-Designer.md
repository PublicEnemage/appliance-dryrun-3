# DRYRUN-JOBREVIEW — Designer

## Context visible to this session

### Project instruction files in context

1. **CLAUDE.md** (the Constitution, `/CLAUDE.md`) — mission and principles slots are
   unfilled template placeholders (`{{double braces}}`); bootstrap has not run. Core
   rules in effect: session protocol (read CLAUDE.md + STATE.md + input manifest only;
   work on own branch; no `git stash`; commit before ending; treat conversation as
   disposable); the five-role artifact chain (Consulted → Author → Challenger → Approver
   → Consumer); governance (agents branch and PR only, never push to main);
   single-principal disclosure (Intent Owner and Engineering Lead are one person, no
   independent review at this stage).

2. **STATE.md** (`/STATE.md`) — cycle 1, setup phase. `active_tracks: []`. No open
   decisions. No mid-task work. Product description field is empty (bootstrap has not
   run).

3. **No task input manifest in the repository.** This session received its task via
   conversation prompt. Per session protocol §3: "A decision counts only once it is
   written to a named artifact in the repository." I proceed from the files and treat the
   prompt as advisory. This divergence is noted here.

### Notes about the person (from session context)

- Email: imran.canuck@gmail.com (used for authorship and attribution only)
- Git user: PublicEnemage
- Holds: Intent Owner seat and Engineering Lead seat (listed as "Human 1" in
  `docs/roles.yml` holders; the name substitution that bootstrap performs has not
  happened yet)
- Single-principal disclosure applies (CLAUDE.md Governance): one person holds both
  human seats; no independent review is available at this stage

---

## 1. My own job (Designer seat)

Source: `docs/roles.yml` lines 120–137. I review each field and say keep or change.

### trigger

> "Use cases are approved and the product has a user interface; a UX challenge finding
> reopens a flow"

**KEEP with a note.** Two distinct trigger events: initial design when use cases are
approved and a UI is in scope, and reopening when a challenge finding arrives. The
condition "the product has a user interface" is unverifiable from the artifact trail alone.
No seat is chartered to make and record that determination before my trigger fires. Floor
D4 handles the no-UI case ("UX design … exists, or are signed not-applicable"), but the
decision to sign not-applicable sits with the Intent Owner, not with me. A fresh session
would not know whether to activate or wait for a not-applicable declaration unless an
explicit artifact (the approved intent, or a front-matter flag in the business case) says
so. See DESIGNER gap 1.

---

### inputs

| # | Artifact | From | Decision |
|---|---|---|---|
| 1 | users-use-cases | Product | **KEEP** — correct source and artifact type. Precondition: must be `status: approved` before I act (implicit, not stated). |
| 2 | architecture | Architect | **KEEP** — I need the architecture to understand the technical constraints on my frontend design, in particular the services and APIs layer that my flows will call. Precondition: must be `status: approved` (implicit). See DESIGNER gap 2 for a timing tension. |

Two inputs appear absent:

- `intent from Product` (or from Intent Owner) — floor D4 requires UX design to exist or
  be signed not-applicable, judged by Intent Owner. The intent artifact names the problem,
  users, and Intent Owner (floor C1). Without it as a formal input, a fresh session has
  no documented basis for understanding the product's purpose before designing flows.
  See DESIGNER gap 3.
- `review from Verifier` — my verifier sends review findings that may reopen a flow (my
  trigger's second event). Yet `review from Verifier` is not listed as an input. Without
  it, the reopening trigger has no named artifact to act on. See DESIGNER gap 4.

---

### value

> "Designs how the product looks and behaves for its users: experience intent, flows,
> navigation and states, and the design system, so that interface decisions are drawn and
> not left to be read many ways"

**KEEP.** Accurate. The phrase "interface decisions are drawn and not left to be read many
ways" captures the core purpose well: my deliverables remove ambiguity that would
otherwise be resolved inconsistently by each Builder session.

One note: "experience intent" is listed here as part of my value but the template list
holds only `docs/templates/ux-design.md`. The experience intent is presumably a section
within that template. If it is not, the value statement promises output that no template
covers. See DESIGNER gap 5.

---

### outputs

| # | Artifact | For | Decision |
|---|---|---|---|
| 1 | ux-design | Builder | **CHANGE** — Builder's inputs do not list ux-design from Designer. My output lists Builder as the consumer, but no corresponding input exists in Builder's job. In addition, Intent Owner's outputs state they approve "UX design" and forward it to Architect — a path that exists in no seat's job description as a formal output or input. The correct consumer chain is: Designer authors → Intent Owner approves (human_approver: true in artifact-types.yml) → Builder and Architect consume the approved version. My output should list Intent Owner as the approval hop and both Builder and Architect as downstream consumers. See DESIGNER gap 6. |
| 2 | design system | Builder | **CHANGE** — `design system` has no entry in `docs/artifact-types.yml`. It has no `prefix`, no `dir`, no `human_approver` flag, and no required diagrams. Without a formal artifact type, the design system cannot be versioned, located, named, or checked by any current check. The output is promised in my job description but cannot be produced as a valid artifact. It is also absent from Builder's inputs. See DESIGNER gap 7. |

---

### standards

`docs/dor/floor.yml` and `docs/artifact-types.yml`

**KEEP.** Both are necessary. The floor governs my artifacts at each gate. The
artifact-types file governs naming, location, and approval requirements. One gap: the
design system has no entry in artifact-types.yml (see DESIGNER gap 7), so the standard I
must follow for producing it is undefined.

---

### templates

`docs/templates/ux-design.md`

**KEEP with a note.** Only one template is listed. The design system is a second output
but has no corresponding template. This means I have no authoritative template to follow
when producing the design system. If a future project adds a `design-system` artifact
type and template, this list needs updating. See DESIGNER gap 7 (mirror).

---

### verifier

Seat: Verifier. Evidence: "A review file beside each UX artifact; required diagrams
present (E16); each use case traced to a flow"

**KEEP with a note.** The evidence items are appropriate: E16 enforces diagram presence
and form, and tracing use cases to flows is the correct acceptance criterion for UX
artifacts. However, Designer and Verifier are **not listed as an incompatible pair** in
`docs/roles.yml`. The minimum-crew holders assign Designer and Verifier to Agent B and
Agent D respectively, which keeps them separate in practice. But the incompatibility is
not enforced by the SEATS check because there is no rule in `incompatible_pairs` for
`[Designer, Verifier]`. If a future holder were to hold both seats, nothing would block
it. See DESIGNER gap 8.

---

### qualified_layers

`[frontend]`

**KEEP.** I qualify for a single layer, which is appropriate given my concern. The
Architect also qualifies for `frontend`. D6 requires author and challenger to be
different qualified seats. If I author the frontend layer of the UX design, the Architect
can challenge it (and vice versa). This wiring is available but not stated explicitly.
See DESIGNER gap 9.

---

### What I cannot do as written

1. Author or challenge any architecture layer other than `frontend`.
2. Produce the design system as a formal typed artifact — it has no entry in
   `docs/artifact-types.yml` and therefore no naming convention, storage location, or
   approval path.
3. Approve my own artifacts — `human_approver: true` for ux-design; Intent Owner approves.
4. Receive the architecture from Architect before it is approved — but no check enforces
   the approved-status precondition on my inputs.
5. Formally route the approved ux-design to Architect — Intent Owner's outputs describe
   this forwarding, but no mechanism in my job description links to it.
6. Activate without an explicit determination that the product has a user interface — the
   condition exists in my trigger but no artifact records the decision.

---

### What I would refuse to accept as input

1. `users-use-cases` with `status` not `approved` — designing flows from unapproved use
   cases risks invalidated work if the use cases change.
2. `architecture` with `status` not `approved` — technical constraints on the frontend
   layer (APIs, state model) must be stable before I commit them to flows.
3. A direct instruction from a seat other than through a named artifact — conversation
   context is disposable (CLAUDE.md §3); I act only on artifacts in the repository.
4. A task with no input manifest — floor I7 requires every task to carry its own input
   manifest; I will not act on conversation context alone.
5. A review finding that asks me to change an approved upstream artifact (users-use-cases,
   architecture) — I surface the finding to the relevant seat; I cannot author upstream
   artifacts.
6. A `design system` specification without a formal artifact type being defined — I cannot
   produce a trackable, checkable output without a type, prefix, and directory.

---

## 2. The other seats

### Intent Owner

**Recommendation: Accept with conditions**

*What I hand to them:* `ux-design` for approval. My outputs list Builder as the consumer,
but artifact-types.yml shows `human_approver: true` for ux-design. The Intent Owner must
approve my ux-design before it reaches any downstream consumer. This is not stated in my
outputs — it is implicit in the `human_approver` flag.

*What I take from them:* the approval decision (status → approved on the ux-design
artifact); also implicitly the determination that the product has a user interface (or a
not-applicable declaration per floor D4).

*Overlap:* None. Intent Owner decides worth and experience acceptance; I design experience
execution.

*Conditions:*
1. My outputs should explicitly list `{artifact: ux-design, for: Intent Owner, acceptance:
   "approves or returns with findings; floor D4 met or signed not-applicable"}` before
   the Builder hop.
2. The "UI in scope" determination must be recorded in a named artifact (the intent or
   business case) so I have an artifact basis for activating.

*Wiring check:* Intent Owner's outputs list "approved … UX design … for Architect" — but
Designer's outputs list ux-design only for Builder, and Architect's inputs do not include
ux-design from Intent Owner or Designer. Three separate wiring gaps converge here. See
METHOD gap 1.

---

### Engineering Lead

**Recommendation: Accept**

*What I hand to them:* nothing directly. Engineering Lead approves engineering artifacts;
ux-design is approved by Intent Owner.

*What I take from them:* nothing directly.

*Overlap:* None. Engineering Lead governs soundness and governance of engineering
artifacts; I govern user interface decisions.

*Wiring check:* Clean. No artifacts cross between us.

---

### Product

**Recommendation: Accept with conditions**

*What I hand to them:* nothing formally. My outputs go to Builder.

*What I take from them:* `users-use-cases` (my input #1).

*Overlap:* None. Product owns use case content and paths; I translate them into visual
and interaction decisions.

*Conditions:*
1. Product's outputs list `{artifact: "intent, business case, users and use cases", for:
   Architect}` — Designer is not named as a consumer. Yet my job requires users-use-cases
   from Product as a first input. Product's job does not formally output to me. A fresh
   Product session authoring stories would not know to notify me when use cases are
   approved. Propose that Product's outputs add `{artifact: users-use-cases, for:
   Designer}` or that the existing output broadens its consumer list to include Designer.

*Wiring check:* My input lists `users-use-cases from Product` — consistent with Product
as the source. Product's output lists the same artifact for Architect only. The send is
undeclared on Product's side. See DESIGNER gap 10.

---

### Delivery

**Recommendation: Accept**

*What I hand to them:* nothing directly.

*What I take from them:* nothing directly.

*Overlap:* None. Delivery owns process and cadence; I own interface design.

*Wiring check:* Clean. No artifacts cross between us.

*Note:* If Delivery cuts an increment that includes a use case before the UX design for
that use case is approved, Builder may start implementing without a stable design. No
coordination gate prevents this. See METHOD gap 2.

---

### Architect

**Recommendation: Accept with conditions**

*What I hand to them:* `ux-design` — not as a formal output in my job description, but
Intent Owner's outputs list "approved … UX design … for Architect." After Intent Owner
approves my ux-design, Architect needs to receive it because architectural decisions for
the frontend layer must be consistent with the approved UX flows. My job description does
not list `ux-design for Architect` as an output, and Architect's inputs do not list
`ux-design from Designer` (or from Intent Owner). See METHOD gap 1.

*What I take from them:* `architecture` (my input #2).

*Overlap:* Both Architect and I qualify for the `frontend` layer (Architect's
`qualified_layers` includes `frontend`; mine is `[frontend]`). D6 requires each layer to
have a different author and challenger. If I author the UX design's frontend flow
decisions, Architect can challenge them (and I can challenge Architect's frontend
architectural decisions). However, neither job description states this convention
explicitly. Without a stated authoring split, two sessions could author overlapping
frontend decisions without a tiebreaker. See METHOD gap 3.

*Conditions:*
1. Add `{artifact: ux-design, for: Architect}` to my outputs (after Intent Owner approves)
   to close the wiring gap.
2. Resolve the frontend authoring convention: who authors vs. challenges the frontend
   section of the architecture vs. the UX design?

*Wiring check:* I receive architecture from Architect — consistent with Architect's output
listing architecture `for: Builder`. But Architect's outputs do not include anything
`for: Designer`. I receive architecture because I need it as an input, not because
Architect formally targets me. The implicit targeting means a fresh Architect session's
task manifest might not include Designer as a consumer and might not notify me when
architecture is approved.

---

### Verifier

**Recommendation: Accept with conditions**

*What I hand to them:* `ux-design` set to in-review, with all required diagrams and use
cases traced to flows.

*What I take from them:* `review` — findings on each artifact I author, answered item by
item.

*Overlap:* Designer and Verifier are not listed as an incompatible pair. In the minimum
crew, Agent B holds Designer and Agent D holds Verifier — separation in practice. But
there is no structural rule preventing one holder from holding both seats. See DESIGNER
gap 8.

*Conditions:*
1. Add `[Designer, Verifier]` to `incompatible_pairs` in `docs/roles.yml`. (Proposed
   here; I do not edit that file.)
2. Add `{artifact: review, from: Verifier}` to my inputs — the review is the artifact
   I act on when a challenge finding reopens a flow (my trigger's second event), but it
   is not currently listed as a formal input.

*Wiring check:* Verifier's outputs include `{artifact: review, for: Architect}` and
`{artifact: review, for: Product}` but no explicit `{artifact: review, for: Designer}`.
The "any artifact in review" catch-all in Verifier's inputs likely covers my ux-design,
but the explicit return path (review back to Designer) is absent from Verifier's outputs.
See DESIGNER gap 11.

---

### Builder

**Recommendation: Accept with conditions**

*What I hand to them:* `ux-design` and `design system` (my listed outputs).

*What I take from them:* nothing directly.

*Overlap:* Builder and Designer are listed as an incompatible pair (`[Builder, Designer]`).
Correct — Builder implements what I design; if one session held both seats, it would
implement its own design without independent challenge.

*Conditions:*
1. Builder's inputs (`increment-intent`, `architecture`, `test-strategy`, `cicd`) do not
   list `ux-design from Designer` or `design system from Designer`. My outputs target
   Builder, but Builder has no formal receive. A fresh Builder session's task manifest
   would not include my artifacts. See DESIGNER gap 12.
2. The `design system` has no artifact type, so Builder has no defined artifact to point
   to even if the input were added.

*Wiring check:* I send two artifacts to Builder; Builder lists neither as an input. The
wiring is entirely one-sided.

---

### Operator

**Recommendation: Accept**

*What I hand to them:* nothing directly.

*What I take from them:* nothing directly.

*Overlap:* None. Operator owns security, deployment and run; I own user interface design.

*Wiring check:* Clean. No artifacts cross between us.

*Note:* Operator's risk assessment may identify privacy or security constraints that
affect UI flows (e.g., how credentials are entered, what data is displayed). No formal
mechanism routes those constraints to me. If Operator's risk assessment is produced after
my UX design is approved, I have no artifact basis for incorporating them. See METHOD
gap 4.

---

### Steward

**Recommendation: Accept**

*What I hand to them:* nothing directly. Steward audits the process trail.

*What I take from them:* nothing directly.

*Overlap:* None. Steward holds no artifact seat; it can audit my process compliance
without a conflict.

*Wiring check:* Clean. Steward receives my artifacts indirectly through the audit trail
and through the review that Verifier produces beside each of my artifacts.

---

## 3. Help protocol

### What I offer each seat and when

| Seat | What I offer | When |
|---|---|---|
| Intent Owner | ux-design set to in-review with all required diagrams; experience intent, flows, navigation and states complete | When use cases are approved and architecture is approved (or when a challenge finding reopens a flow) |
| Engineering Lead | Nothing directly | — |
| Product | Nothing formally; may raise a finding if a use case has no clear UI surface | When authoring ux-design and a use case is ambiguous |
| Designer (self) | Not applicable | — |
| Architect | Approved ux-design (after Intent Owner approval) | After ux-design is approved; also raise an inconsistency finding if my flows conflict with the approved architecture's frontend section |
| Verifier | ux-design set to in-review, with template fields populated and required diagrams present | Each time I complete a draft or revise after a finding |
| Delivery | Nothing directly | — |
| Builder | Approved ux-design and design system; each use case mapped to a flow, components and tokens defined | After all approvals are in place and before Builder starts implementing a use case with a UI |
| Operator | Nothing directly | — |
| Steward | Clean artifact trail: correct folder, status transitions recorded, parents cited | Continuously |

### What I ask of each seat, where I write it, and how long I wait

| Seat | What I ask | Where I write the request | Wait limit | Escalate to |
|---|---|---|---|---|
| Product | Approved users-use-cases | Task manifest for my session (lists artifact path); STATE.md note if blocked | One cycle | Steward (audit entry); open decision in STATE.md |
| Architect | Approved architecture | Task manifest for my session; STATE.md note if blocked | One cycle | Steward |
| Intent Owner | Approval of ux-design; determination that the product has a UI (or not-applicable declaration) | Artifact set to `in-review`; STATE.md note if blocked | Not defined — Intent Owner and Engineering Lead are the same person; no independent escalation path | Note in STATE.md as open decision; no further escalation authority defined (see METHOD gap 5) |
| Verifier | Review of ux-design | Artifact status `in-review`; review file path in STATE.md | One cycle | Steward |

---

## 4. Authority

### What I decide alone

- The experience intent: the intended user feeling and the design principles that govern
  all interface decisions, within the scope the approved use cases set
- Which flows to draw for each use case: the main path, alternate paths, and failure paths
  through the interface
- Screen layout, navigation structure, component choice, and visual states, within the
  approved architecture's frontend constraints
- Whether a use case has been mapped to a flow and the mapping is complete
- Whether an artifact meets its own template requirements before I set it to in-review

### What I decide only after consulting

| Decision | Consult | Reason |
|---|---|---|
| A flow requires a frontend capability the approved architecture does not provide | Architect | Architect owns the architecture; I cannot change the frontend layer unilaterally |
| A use case requires UI behavior that raises a privacy or security concern | Operator | Operator owns security and privacy; I surface the concern, they assess and record it |
| A flow requires a use case that is not yet approved | Product | Product owns use case content; I cannot invent use cases |
| The product has no user interface and I should sign D4 not-applicable | Intent Owner | Intent Owner judges floor D4; the decision must be in an approved artifact |
| A design choice requires a cross-cutting ADR (e.g., a styling framework decision) | Architect | ADRs for cross-cutting choices are an Architect responsibility (floor D3); I flag the need, Architect authors the ADR |

### When I ask before acting

- Before beginning any design work while architecture or users-use-cases is still in
  `draft` or `in-review` status
- Before signing floor D4 not-applicable (no UI) — this is Intent Owner's decision
- Before raising a challenge finding against the architecture's frontend section — I
  confirm the inconsistency is real and document it in the review file, not in conversation
- Before delivering ux-design to Builder — I confirm Intent Owner has approved it (status:
  approved)

### What I would refuse

- Authoring any artifact outside the `frontend` layer in the architecture
- Approving my own ux-design — `human_approver: true`; Intent Owner approves
- Treating a conversation decision as an approved artifact (CLAUDE.md §3)
- Producing a `design system` as a formal artifact until a type, prefix, and directory
  are defined in `docs/artifact-types.yml` — I can draft it as a document but cannot
  submit it to any check or approval path
- Acting on a task with no input manifest (floor I7)
- Delivering ux-design to Builder before it is approved by Intent Owner

### Where the procedure left me less room than my job description implies

1. **The design system is untrackable.** My value statement includes the design system as
   a deliverable, and my outputs list it for Builder. But no artifact type exists for it.
   I can produce a document, but it cannot be versioned, checked, or formally approved
   under the current process. In practice, my design system decisions are not auditable
   or traceable to a gate.

2. **I cannot activate without a human decision I have no way to prompt.** My trigger
   requires that "the product has a user interface." The Intent Owner holds floor D4, but
   nothing in the procedure routes an activation prompt to the Intent Owner, or routes
   the not-applicable declaration back to me. I must wait passively or check the artifact
   trail myself.

3. **The approval-to-Builder path is undescribed.** My job says I output ux-design for
   Builder. But human_approver is true, meaning Intent Owner must approve first. My job
   description makes me look like I hand directly to Builder, when in reality I hand to
   Intent Owner first. The procedure shortens my apparent authority — I am not the one who
   decides when Builder receives my work.

4. **No formal mechanism to signal Architecture of an approved UX design.** Intent Owner
   sends the approved UX design to Architect (per Intent Owner's outputs), but neither
   my job nor Architect's inputs describe this path. If a constraint in my approved UX
   design conflicts with the architecture, there is no artifact-level handshake that
   triggers a redesign.

---

## 5. Guessing log

Every point where the procedure left me without a clear answer. Labels:
DESIGNER = a gap in my job description or the wiring to/from it;
METHOD = a gap in the process design visible from my seat.

| Label | Description |
|---|---|
| DESIGNER gap 1 | **"The product has a user interface" is an undocumented decision.** My trigger requires this condition, but no artifact records the determination, and no seat is chartered to make and forward it. Floor D4 handles the no-UI case via a not-applicable, but who decides this and where it is written is unspecified before my session activates. Proposed fix: require the intent or business-case artifact to include a `has_ui` flag or equivalent, or require the Intent Owner to produce a floor-D4 not-applicable artifact before my trigger is skipped. |
| DESIGNER gap 2 | **Timing tension: architecture and use-case approval may not be simultaneous.** My trigger fires when "use cases are approved." My second input requires an approved architecture. Architect's trigger fires when "the business case and use cases are approved" — approximately the same time as mine. If I activate before architecture is approved, I have no second input. A session could begin designing flows against unapproved architectural constraints. Proposed fix: state that my trigger requires both use cases and architecture to be approved, or clarify that I begin with use cases only and incorporate architecture as it becomes available. |
| DESIGNER gap 3 | **Intent artifact absent from inputs.** The intent names the problem, users, and Intent Owner (floor C1). Designing without it risks flows that contradict the stated problem or serve an unlisted user. Proposed fix: add `{artifact: intent, from: Product}` (approved) to my inputs. |
| DESIGNER gap 4 | **Review from Verifier absent from inputs.** My trigger's second event is "a UX challenge finding reopens a flow," but `review from Verifier` is not a listed input. A fresh session cannot open a task manifest for the reopening case without a formal input entry. Proposed fix: add `{artifact: review, from: Verifier}` to my inputs. |
| DESIGNER gap 5 | **Experience intent may have no template section.** My value statement lists "experience intent" as a deliverable, but only `docs/templates/ux-design.md` is listed. If the template does not contain an experience-intent section, I have no standard form for it. Unable to verify without reading the template (session protocol limits reads to named inputs). |
| DESIGNER gap 6 | **ux-design output consumer chain is broken.** My output lists ux-design `for: Builder`. Artifact-types.yml marks it `human_approver: true`. Intent Owner's outputs mention "approved … UX design … for Architect." Three different consumer paths are implied (Builder, Intent Owner approval, Architect forwarding), none of which are complete in any seat's job description. The approval hop through Intent Owner and the forwarding to Architect are undescribed. Proposed fix: outputs should read `{artifact: ux-design, for: Intent Owner}` first, then `{artifact: approved ux-design, for: Builder and Architect}` after approval. |
| DESIGNER gap 7 | **design system has no artifact type.** `docs/artifact-types.yml` defines `ux-design` but not `design system`. There is no `prefix`, `dir`, `human_approver`, or required-diagrams entry. The design system cannot be formally produced, versioned, checked, or approved under the current process. Proposed fix: add a `design-system` artifact type to `docs/artifact-types.yml` with an appropriate prefix (e.g., `DS`), directory (`docs/design`), `human_approver: true`, and a template at `docs/templates/design-system.md`. |
| DESIGNER gap 8 | **[Designer, Verifier] not in incompatible_pairs.** The five-role chain forbids the author and challenger of an artifact to be the same session. Designer is verified by Verifier. But `[Designer, Verifier]` is absent from `incompatible_pairs`, meaning a single holder could hold both seats and challenge their own UX artifacts without the SEATS check refusing it. Proposed fix: add `[Designer, Verifier]` to `incompatible_pairs` in `docs/roles.yml`. |
| DESIGNER gap 9 | **Frontend authoring convention between Architect and Designer is unstated.** Both seats qualify for `frontend`. D6 requires a different author and challenger per layer. Who authors vs. challenges the frontend layer section of the architecture, and who authors vs. challenges the UX design's frontend flows? Neither job description specifies the split. A session-level convention (Architect authors the technical frontend section; Designer authors the interaction frontend section; each challenges the other) exists implicitly in the seat concerns, but is not written down. |
| DESIGNER gap 10 | **Product does not list users-use-cases for Designer in its outputs.** Product's outputs list "intent, business case, users and use cases" `for: Architect` only. Designer is not named. A fresh Product session's task manifest would not include Designer as a consumer of users-use-cases, and might not route the approved artifact to me. Proposed fix: add `{artifact: users-use-cases, for: Designer}` to Product's outputs (not my job to fix, but raises the issue here). |
| DESIGNER gap 11 | **Verifier does not list a review output for Designer.** Verifier's outputs name review `for: Product` and `for: Architect` but not `for: Designer`. When Verifier challenges my ux-design, the review finding must reach me, but the routing is absent from Verifier's job. Proposed fix: add `{artifact: review, for: Designer, acceptance: "Each finding has a severity, and open_findings counts what is unanswered"}` to Verifier's outputs. |
| DESIGNER gap 12 | **Builder does not list ux-design or design system as inputs.** Builder's inputs are increment-intent, architecture, test-strategy, and cicd. Neither of my outputs appears there. A fresh Builder session would not include my artifacts in its task manifest and could implement UI without reading the approved design. Proposed fix: add `{artifact: ux-design, from: Designer}` and `{artifact: "design system", from: Designer}` to Builder's inputs. |
| METHOD gap 1 | **UX design approval and forwarding chain is described by no seat's job.** Intent Owner's outputs state they approve UX design and send it "for Architect." Designer's outputs send ux-design to Builder. Architect's inputs do not list ux-design. The artifact travels Designer → Intent Owner (approval) → Architect (receive), but this three-hop chain is in no seat's job description end to end. A process gap exists: if Architect's frontend architecture section conflicts with the approved UX design, there is no artifact-level trigger to reopen the architecture. |
| METHOD gap 2 | **No gate prevents Builder from starting a use case before its UX design is approved.** Delivery sets the increment plan; Builder pulls from it. Nothing in the plan gate or increment gate requires the UX design to be approved before Builder starts a use-case implementation. Builder could implement from the architecture alone, leaving UX decisions implicit in code. |
| METHOD gap 3 | **Frontend layer authoring tiebreaker is absent.** Both Architect and Designer qualify for `frontend`. If Architect's frontend architectural section and my UX flows conflict, no seat has authority to adjudicate. The diagram-governs rule (CLAUDE.md §Rules that stay with judgment) applies within an artifact but does not resolve conflicts across artifacts from different seats. |
| METHOD gap 4 | **Operator's risk assessment may arrive after UX design is approved.** Operator's trigger fires after NFRs and architecture are approved — roughly the same time as mine. If my UX design is approved first, it may include interaction patterns that Operator later flags as security or privacy risks. No artifact-level mechanism reopens my design based on Operator's risk assessment. |
| METHOD gap 5 | **No escalation path for blocked Intent Owner / Engineering Lead seat, mirroring gaps found in Product and Architect reviews.** Both human seats are held by one person. If they are unavailable to approve ux-design, the process stalls. STATE.md records the open decision, but no escalation authority is named. |
