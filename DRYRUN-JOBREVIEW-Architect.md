# DRYRUN-JOBREVIEW — Architect

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

## 1. My own job (Architect seat)

Source: `docs/roles.yml` lines 99–119. I review each field and say keep or change.

### trigger

> "The business case and use cases are approved; NFRs are needed; a challenger finding or
> failed gate reopens the design"

**KEEP with a note.** Three distinct trigger events, covering the initial design pass
and reopening after challenge. Clear enough for a fresh session to know when to activate.
One implicit gap: "NFRs are needed" implies I also author the NFR artifact, but NFRs are
listed only in outputs, not in the trigger text. The trigger should read "…NFRs are
authored and the architecture is due…" to make it explicit that NFRs and architecture
both start here. Propose adding: "…and the NFR and architecture artifacts are due."

---

### inputs

| # | Artifact | From | Decision |
|---|---|---|---|
| 1 | users-use-cases | Product | **KEEP** |
| 2 | business-case | Product | **KEEP** |
| 3 | risk-assessment | Operator | **CHANGE** — timing problem: Operator's trigger is "NFRs and architecture are approved," meaning Operator activates *after* me. I cannot receive a risk-assessment from Operator before I have produced the NFR. The dependency is circular. See ARCHITECT gap 1. |
| 4 | review | Verifier | **KEEP** — correctly covers the challenger-finding and failed-gate reopening path |

Three additional inputs are absent from the list but appear as outputs that target me:

- `intent, business case, users and use cases from Intent Owner` — Intent Owner's outputs
  list these "for Architect" with acceptance "Each approved artifact cites its parents,
  has approved_at set and no open finding." My inputs list only two of the three, and
  they name Product as the sender. After Intent Owner approval, the artifacts are
  technically owned by the approval status, not re-sent. The chain is: Product authors →
  Intent Owner approves → Architect reads the approved artifacts. My inputs should
  clarify the status gate: I read `users-use-cases` and `business-case` only when
  `status: approved`. Not a structural gap but an implicit precondition (ARCHITECT gap 2).
- `conceptual-design` — I produce it; Product receives it. No input gap here.
- `nfr` — I produce it; Verifier and Operator receive it. No input gap here.

---

### value

> "Shapes the system: NFRs with targets, a conceptual design that maps every use case to
> a capability, and a target architecture with one section per layer, each with failure
> modes and an ADR for every cross-cutting choice. Owns the data layer unless a Data
> Architect is adopted"

**KEEP with a note.** Accurate and complete for the core scope. "Owns the data layer
unless a Data Architect is adopted" is important: without a Data Architect, I also
produce the data section of the architecture including the data-model diagram (floor D13,
E16). The value statement should be explicit that this means I author contracts/migrations
review responsibility too, or reference `docs/standards/data/README.md` for the
handoff criteria.

---

### outputs

| # | Artifact | For | Decision |
|---|---|---|---|
| 1 | architecture | Builder | **KEEP** — acceptance "Each layer section can be built from without asking what it should have said; required diagrams present (floor D2, D3, D13)" is well-formed |
| 2 | nfr | Verifier | **CHANGE** — acceptance says "Each NFR has a target or a signed not-applicable, so a test type can be named for it (floor C4, D5)." Floor C4 says NFRs also go to Engineering Lead for approval (judged_by: Engineering Lead). But the output only lists Verifier as the consumer. Add Engineering Lead as a second consumer: `{artifact: nfr, for: "Verifier and Engineering Lead", acceptance: "…"}`. See ARCHITECT gap 3. |
| 3 | conceptual-design | Product | **CHANGE** — acceptance cites only floor D1. Floor D13 also requires a capability-map Mermaid diagram in the conceptual-design artifact. Acceptance should include "(floor D1, D13)". See ARCHITECT gap 4. |

One output appears to be missing:

- `architecture for Engineering Lead` — Engineering Lead's inputs list `{artifact:
  architecture, from: Architect}` as their first input. My outputs list architecture
  `for: Builder`, not for Engineering Lead. The approval path is: I author → Verifier
  challenges → Engineering Lead approves → Builder consumes. But the explicit routing to
  Engineering Lead is absent from my outputs. See ARCHITECT gap 5.

---

### standards

`docs/dor/floor.yml` and `docs/standards/data/README.md`

**KEEP.** Correct. The floor defines the gates my artifacts must pass. The data standards
guide covers my ownership of the data layer until a Data Architect is adopted.

---

### templates

`docs/templates/nfr.md`, `docs/templates/conceptual-design.md`,
`docs/templates/architecture.md`, `docs/templates/adr.md`

**KEEP the list.** All four are appropriate. One omission: `docs/templates/risk-assessment.md`
appears in Operator's templates, not mine — which is correct since Operator authors the
risk assessment. However, I receive `risk-assessment from Operator` as an input. The
template listing is consistent with the intended authoring split.

---

### verifier

Seat: Verifier. Evidence: "A review file beside each Architect artifact; required
diagrams present and well formed (E16); layer authors and challengers qualified and
distinct (SEATS)"

**KEEP.** Verifier and Architect are an incompatible pair (listed in `incompatible_pairs`
as `[Verifier, Architect]`), ensuring independence. E16 and SEATS are the right evidence
points. One note: E16 checks Mermaid presence, form, and minimum size. Whether a diagram
*matches* its text is declared a "challenger's call" in the E16 note, which falls to the
Verifier as challenger — this is correctly described here.

---

### qualified_layers

`[data, services-apis, integration, frontend, deployment-runtime]`

**KEEP with a note.** I qualify for five of the seven required layers (floor D2). The
two I do not qualify for are:

- `domain-core` — not in my list. No seat in the minimum crew is listed as qualifying
  for this layer. `qualified_domains` in `docs/roles.yml` is `{}`. This will cause the
  D6 check to fail when a domain-core section is authored. See ARCHITECT gap 6 /
  METHOD gap 1.
- `operations` — not in my list. Operator qualifies for `deployment-runtime, operations,
  integration`. So Operator is the qualified seat for the operations layer, which is
  correct since Operator authors the CI/CD and ops-readiness artifacts.

D6 requires "a different challenger seat" per layer. For the layers I author:

| Layer | My role | Challenger must be a different qualified seat |
|---|---|---|
| data | Author | Who challenges? No other non-Architect seat lists `data`. Optional Data Architect does. Without it, no challenger is available for the data layer. See ARCHITECT gap 7. |
| services-apis | Author | Builder qualifies for `services-apis`. Builder can challenge. OK. |
| integration | Author | Operator also qualifies for `integration`. Operator can challenge. OK. |
| frontend | Author | Builder qualifies for `frontend`. Builder can challenge. OK. |
| deployment-runtime | Author | Operator qualifies for `deployment-runtime`. Operator can challenge. OK. |

---

### What I cannot do as written

1. Author or challenge the `domain-core` layer — not in my `qualified_layers`.
2. Author or challenge the `operations` layer — not in my `qualified_layers`.
3. Challenge any artifact I authored — the five-role chain and SEATS check both forbid it.
4. Approve my own artifacts — `human_approver: true` for architecture, nfr, and
   conceptual-design; the Engineering Lead approves architecture; the Intent Owner approves
   business and case-phase artifacts.
5. Receive the risk-assessment from Operator before producing the NFR artifact, because
   Operator's trigger fires after my NFR is approved (circular dependency).
6. Qualify the data layer without either adopting a Data Architect or another qualified
   seat being explicitly chartered to challenge it (gap 7).

---

### What I would refuse to accept as input

1. `users-use-cases` or `business-case` with `status` not `approved` — I require approved
   artifacts before shaping the system; planning against unapproved use cases wastes the
   design if they change.
2. A problem statement directly (unmediated by Product) — I accept Product's output; if
   the Intent Owner bypasses Product and hands me raw requirements, I route them to
   Product first.
3. A `risk-assessment` delivered before I have produced and submitted the NFR — this is
   temporally impossible under the current wiring and I would flag the sequencing error.
4. A review finding that asks me to change an approved upstream artifact (business-case,
   users-use-cases) — I can propose changes to Product or raise a challenge finding; I
   cannot author or approve upstream artifacts.
5. A task with no input manifest — floor I7 requires every task to carry its own input
   manifest; I will not act on conversation context alone.
6. An ADR authored by a seat that is not qualified for the layer the ADR governs — I would
   flag the SEATS violation rather than accept the ADR as a basis for my architecture.

---

## 2. The other seats

### Intent Owner

**Recommendation: Accept**

*What I hand to them:* nothing directly as a formal output. My outputs go to Builder,
Verifier, and Product. However, the architecture (and indirectly the NFR) feeds the
Engineering Lead who is the same person as the Intent Owner. The approved architecture
then unlocks Builder.

*What I take from them:* approved `users-use-cases` and `business-case` (the Intent Owner
approves what Product authored; I read the approved versions). These are listed in my
inputs as coming `from: Product`, which is technically correct for authorship, but the
precondition is approval by Intent Owner.

*Overlap:* None. Intent Owner decides worth; I decide shape.

*Wiring check:* Intent Owner's outputs list "approved intent, business case, users and
use cases, UX design and increment plan" for Architect. My inputs list only
`users-use-cases` and `business-case` from Product, not the full set. The approved
`intent` is not listed as my input, though floor D1 (conceptual design maps every use
case to a capability) implicitly requires it. See ARCHITECT gap 8.

---

### Engineering Lead

**Recommendation: Accept**

*What I hand to them:* architecture (my primary output; their first input is
`{artifact: architecture, from: Architect}`).

*What I take from them:* nothing as a formal input — they approve my artifacts but no
artifact flows back to me from them.

*Overlap:* None. Engineering Lead approves; I author.

*Wiring check:* Engineering Lead's inputs list architecture from me — consistent.
Engineering Lead outputs `approved architecture … for Builder` — they hand the approved
artifact to Builder, which is downstream of my authoring. My outputs list architecture
`for: Builder`, which duplicates the Engineering Lead's forwarding step. After the
approval step, is it my artifact or Engineering Lead's approved version that goes to
Builder? The procedure leaves this implicit. Not a structural error, but a session
picking up the Builder task might be unsure which version to read. See METHOD gap 2.

---

### Product

**Recommendation: Accept with conditions**

*What I hand to them:* `conceptual-design` (my output #3, for Product, acceptance "Every
use case maps to a system capability (floor D1)").

*What I take from them:* `users-use-cases` (input #1), `business-case` (input #2).

*Overlap:* None. Product owns use case content; I own system shape. The boundary is:
Product decides what the system must do; I decide how it is structured to do it.

*Conditions:*
1. Product's inputs do not list `conceptual-design from Architect`, even though I send it
   to Product. This is the mirror of PRODUCT gap 5 in the Product review. My output is
   correct; the Product job description needs to add it as an input.

*Wiring check:* My output for Product and Product's unlisted input are inconsistent. I
send; they have no listed receive. This means the conceptual-design could arrive at
Product with no formal acceptance test on their side. Propose raising this with Product
in my review findings, not fixing it here.

---

### Delivery

**Recommendation: Accept**

*What I hand to them:* nothing directly.

*What I take from them:* nothing directly.

*Overlap:* None. Delivery owns process; I own architecture. The boundary is clear.

*Wiring check:* Clean. No artifacts cross between us in either direction.

*Note:* Delivery outputs `role-proposal for Engineering Lead`. If a crew review opens a
new seat that is qualified for a layer I currently hold alone (e.g., a Data Architect),
that proposal comes through Delivery and Engineering Lead, not through me. I am a
downstream beneficiary of that decision but have no direct input to the role proposal
unless I am listed as a peer reviewer. Under E17, independent peer review is required
from "every agent seat that sends it input or consumes its output." If the proposed seat
sends me input or takes my output, I must be a peer reviewer. This is not a gap in
Delivery's job; it is an obligation on me to respond when asked. See METHOD gap 3.

---

### Designer

**Recommendation: Accept with conditions**

*What I hand to them:* `architecture` (Designer's second input is `{artifact: architecture,
from: Architect}`).

*What I take from them:* nothing formally. But the Designer's output `ux-design` affects
my architecture: frontend layer decisions in my architecture must be consistent with the
UX design. If the UX design arrives after my architecture is approved, there is a
sequencing tension.

*Overlap:* Minor. Both I and the Designer qualify for the `frontend` layer. I can author
and challenge frontend architecture; Designer can author and challenge frontend design.
The split is: architecture governs technical decisions (components, APIs, state) while
UX governs interaction decisions (flows, navigation, states). If a technical and
interaction decision conflict, the procedure does not name a tiebreaker. See METHOD gap 4.

*Conditions:*
1. Propose adding `ux-design from Designer` as an optional input to my job — not required
   on first pass (UX may not exist yet) but needed if the UX design is approved before my
   architecture is finalized. At minimum, my architecture should cite whether UX design
   is in scope and approved (floor D4 requires it or a signed not-applicable).

*Wiring check:* Designer receives architecture from me — consistent. I have no listed
receive from Designer. If ux-design arrives after my architecture is approved, I have no
formal mechanism to reopen the design. A challenger finding from Verifier would reopen
it — but the path is indirect.

---

### Verifier

**Recommendation: Accept with conditions**

*What I hand to them:* `architecture` (Verifier receives it as input; their outputs
include a review for Architect), `nfr` (my output #2 for Verifier, acceptance test cites
floor C4, D5).

*What I take from them:* `review` (my input #4; challenger findings that may reopen the
design).

*Overlap:* None (incompatible pair: `[Verifier, Architect]`).

*Conditions:*
1. Verifier's inputs list `architecture from Architect` — consistent with my output.
2. Verifier does not list `nfr from Architect` as an input, even though my output #2
   sends it to Verifier. Verifier's inputs are: "any artifact in review" from Product,
   architecture from Architect, cicd from Operator, and increment verify evidence from
   Builder. The "any artifact in review" catch-all likely covers NFR, but it is
   ambiguous. Propose that Verifier's inputs explicitly list `nfr from Architect`.
   See ARCHITECT gap 9.

*Wiring check:* I send architecture and nfr to Verifier; Verifier sends me reviews.
The nfr → Verifier path relies on the "any artifact in review" catch-all rather than an
explicit input listing. Risk: a fresh Verifier session may not include NFR review in its
input manifest.

---

### Builder

**Recommendation: Accept**

*What I hand to them:* `architecture` (Builder's second input is `{artifact: architecture,
from: Architect}`; acceptance "Each layer section can be built from without asking what
it should have said").

*What I take from them:* nothing directly.

*Overlap:* Builder and Architect are an incompatible pair (`[Builder, Architect]`).
Builder qualifies for `[data, services-apis, frontend, integration]` — four of the five
layers I also qualify for. This means Builder is a valid challenger for my architecture
in those four layers, but not for `deployment-runtime`. Operator qualifies for
`deployment-runtime`, so the challenger for that section is Operator. This is consistent
with the Verifier assigning the right challenger per section under D6 — but D6 is
enforced by SEATS, which checks declared seats, not whether the right qualified seat
actually challenged each section. See METHOD gap 5.

*Wiring check:* Clean. I author; Builder consumes. The acceptance test on my architecture
output ("Each layer section can be built from without asking what it should have said")
correctly captures the consumer-duty test (CLAUDE.md §The chain).

---

### Operator

**Recommendation: Accept with conditions**

*What I hand to them:* `nfr` (Operator's first input is `{artifact: nfr, from: Architect}`),
`architecture` (Operator's second input is `{artifact: architecture, from: Architect}`).

*What I take from them:* `risk-assessment` (my input #3).

*Overlap:* Operator qualifies for `[deployment-runtime, operations, integration]`. I
qualify for `[data, services-apis, integration, frontend, deployment-runtime]`. We both
qualify for `integration` and `deployment-runtime`. Either of us can author or challenge
those layers. This creates an overlap that could lead to unclear ownership. The procedure
does not specify which seat authors vs. challenges each shared layer. See ARCHITECT gap
10 / METHOD gap 6.

*Conditions:*
1. **Circular dependency on risk-assessment.** My input lists `risk-assessment from
   Operator`. Operator's trigger is "NFRs and architecture are approved." This means
   Operator cannot produce a risk-assessment until after I produce the NFR. I cannot
   receive the risk-assessment before producing the NFR. The formal input should either
   be removed from my first-pass trigger (architecture authored before Operator activates)
   or the risk-assessment should be treated as an input only when the design is reopened
   by a challenger finding, not on the initial pass. Propose: change my input from
   `{artifact: risk-assessment, from: Operator}` to
   `{artifact: risk-assessment, from: Operator, note: "only on redesign; Operator cannot produce this before my NFR is approved"}`.

*Wiring check:* My outputs list nfr and architecture for Operator — consistent with
Operator's inputs. Operator outputs risk-assessment for me — in my inputs. The circular
dependency is the structural problem (ARCHITECT gap 1).

---

### Steward

**Recommendation: Accept**

*What I hand to them:* nothing directly.

*What I take from them:* nothing directly. Steward audits process adherence and sends
results to Delivery.

*Overlap:* None. Steward holds no artifact seat; it can audit my process compliance
without a conflict.

*Wiring check:* Clean. Steward receives my artifacts indirectly through the audit trail.
Steward's verifier is the Engineering Lead, preserving independence from the Verifier
chain.

---

## 3. Help protocol

### What I offer each seat and when

| Seat | What I offer | When |
|---|---|---|
| Intent Owner | Architecture and NFR for approval (via Engineering Lead gate) | When architecture and NFR are in-review with challenge answered |
| Engineering Lead | Approved architecture and NFR ready for their review | When Verifier has challenged and I have answered all findings |
| Product | Conceptual-design: every use case mapped to a system capability | When business case and use cases are approved |
| Designer | Architecture (frontend layer section) | When architecture is in-review; Designer reads it as their second input |
| Verifier | Architecture and NFR set to in-review, with all template fields and required diagrams | Each time I complete a draft; also when a gate reopens |
| Delivery | Nothing directly | — |
| Builder | Approved architecture, sufficient to implement each layer without asking what it should have said | After Engineering Lead approval |
| Operator | Approved NFR and architecture | After Engineering Lead approval |
| Steward | Clean artifact trail: parents cited, status transitions correct, diagram check passing | Continuously |

### What I ask of each seat, where I write it, and how long I wait

| Seat | What I ask | Where I write the request | Wait limit | Escalate to |
|---|---|---|---|---|
| Product | Approved users-use-cases and business-case | Task manifest for my session (lists the artifacts by path) | One cycle | Steward (audit); note in STATE.md as open decision |
| Operator | Risk-assessment (on redesign only) | Task manifest for Operator session | One cycle | Steward |
| Verifier | Review of each artifact I set to in-review | Artifact status field + review file path in STATE.md | One cycle | Steward |
| Engineering Lead | Approval of architecture and NFR | Artifact front matter (status: in-review); note in STATE.md if blocked | Not defined — same holder as Intent Owner; no independent escalation path | Note in STATE.md as open decision; no further escalation authority defined (METHOD gap 7) |
| Intent Owner | Nothing directly on first pass; on redesign, approval of changed artifacts | Same as Engineering Lead row above | Same | Same |

---

## 4. Authority

### What I decide alone

- Which layers to include and how to scope each section of the architecture
- Which cross-cutting choices require an ADR and what the ADR options are
- Whether a use case is mapped to a capability in the conceptual design, given the
  approved use cases
- What NFR targets to propose for each non-functional area (target is mine to propose;
  approval is Engineering Lead's to give)
- Whether the data layer is complex enough to trigger the Data Architect adoption criteria
  in `docs/standards/data/README.md`
- Whether a challenger finding is answered and the finding can be closed

### What I decide only after consulting

| Decision | Consult | Reason |
|---|---|---|
| NFR target values for a domain where no seat has domain knowledge | Intent Owner (for business constraints), Operator (for operational constraints) | floor C4 targets must be measurable; I propose, they validate |
| A cross-cutting architectural choice that affects deployment or security | Operator | Operator owns security and deployment risk; their input precedes my ADR |
| Whether a use case can be satisfied by the proposed architecture | Product | Product owns use case correctness; if I cannot map it, Product must clarify or the gap goes back upstream |
| Opening a crew review for a qualification gap (e.g., domain-core layer) | Steward (flag), Engineering Lead (decide) | Crew reviews are governed by Engineering Lead; I flag the gap, I do not resolve it |
| Adding a new architecture layer not listed in floor D2 | Engineering Lead | Any DOR refinement (finer, never coarser) requires approval |

### When I ask before acting

- Before authoring any section of the architecture while `users-use-cases` or
  `business-case` is still in `draft` or `in-review` status
- Before treating a layer as out-of-scope or not-applicable without a signed
  not-applicable in the artifact front matter
- Before filing an ADR for a choice the Operator's risk-assessment explicitly governs
  (to avoid overriding Operator's domain)
- Before declaring the data layer owned by me when the Data Architect adoption criteria
  may already be met

### What I would refuse

- An architecture where the author and challenger are the same session (SEATS check, CLAUDE.md §The chain)
- Approving my own architecture, NFR, or conceptual-design — I am always the author;
  Engineering Lead (architecture, NFR) or Intent Owner (other) approves
- Treating a decision made only in conversation as an approved artifact (CLAUDE.md §3)
- Acting on a task with no input manifest (floor I7)
- Issuing an ADR for a dependency or pattern before the Builder has confirmed the
  dependency exists in the implementation (ADRs govern choices; Builder confirms
  actuality)
- Continuing past the design gate when the SEATS check would fail because no qualified
  challenger exists for a layer (e.g., data layer without a Data Architect or similar)

### Where the procedure left me less room than my job description implies

1. **Data layer ownership is conditional.** I own the data layer "unless a Data Architect
   is adopted," but the adoption criteria are in `docs/standards/data/README.md`, which I
   have not read (per session protocol, I read only what the manifest names). If a Data
   Architect is adopted, ownership transfers and I cannot determine that from the files I
   was directed to read.

2. **No qualified challenger for the data layer without a Data Architect.** My
   `qualified_layers` includes `data`, but no other seat in the minimum crew does. I can
   author the data layer section, but D6 requires a different qualified challenger. The
   check will fail unless a Data Architect is chartered. My job description implies I own
   data; the check structure implies I cannot proceed alone.

3. **domain-core is unowned.** No seat in the minimum crew qualifies for `domain-core`.
   The `qualified_domains` map is `{}`. I cannot author the domain-core section, yet floor
   D2 requires it. This will cause a DOR and SEATS failure on any architecture I produce.
   I have no authority to resolve this — it requires a crew review.

4. **All my artifacts require human approval.** I author NFR, architecture, and
   conceptual-design; all have `human_approver: true`. I can draft, challenge, and revise,
   but I cannot close the loop. The Engineering Lead's availability gates every artifact
   I produce.

---

## 5. Guessing log

Every point where the procedure left me without a clear answer. Labels:
ARCHITECT = a gap in my job description or the wiring to/from it;
METHOD = a gap in the process design visible from my seat.

| Label | Description |
|---|---|
| ARCHITECT gap 1 | **Circular dependency on risk-assessment.** My inputs list `{artifact: risk-assessment, from: Operator}`. Operator's trigger is "NFRs and architecture are approved." Operator cannot produce a risk-assessment before I produce and get my NFR approved. But if the risk-assessment should inform my architecture (as an input implies), I need it before I finalize the architecture. The dependency is circular. Proposed fix: scope this input to "redesign only" and note that on first pass the risk-assessment arrives after my architecture is approved, not before. |
| ARCHITECT gap 2 | **Approved-status precondition is implicit.** My inputs list `users-use-cases` and `business-case` from Product, but the precondition that they must be `status: approved` (not just `in-review`) before I act is not stated. A fresh session might read an in-review artifact and begin designing. Proposed fix: add `status: approved` to the input descriptions. |
| ARCHITECT gap 3 | **NFR output missing Engineering Lead as consumer.** My output #2 lists nfr `for: Verifier`. Floor C4 (judged_by: Engineering Lead) and floor D5 (test strategy names a test type per NFR, judged_by: Engineering Lead) both require Engineering Lead to judge the NFR. Proposed fix: add Engineering Lead as a co-consumer of the NFR output. |
| ARCHITECT gap 4 | **Conceptual-design acceptance test does not cite D13.** Floor D13 requires a capability-map Mermaid diagram in the conceptual-design artifact (enforced by E16). My output #3 acceptance cites only floor D1. Proposed fix: update acceptance to "(floor D1, D13)". |
| ARCHITECT gap 5 | **Architecture output does not list Engineering Lead as consumer.** Engineering Lead's inputs list `{artifact: architecture, from: Architect}` as their first input. My output lists architecture `for: Builder` only. Proposed fix: add Engineering Lead as a consumer (the approval step), then Builder as the downstream consumer. |
| ARCHITECT gap 6 | **domain-core layer has no qualified seat.** No seat in the minimum crew lists `domain-core` in `qualified_layers`. Floor D2 requires one section per layer; D6 requires a qualified author and challenger per section. Any architecture I author will fail D6 for the domain-core layer. This cannot be fixed by changing my job description — it requires a crew review and a role proposal to add a qualified seat. |
| ARCHITECT gap 7 | **No challenger for the data layer in the minimum crew.** I am the only seat qualified for `data`. D6 requires a *different* qualified challenger. The optional Data Architect seat qualifies for `data` and `integration`. Without adopting it, D6 will fail for the data layer section of every architecture I produce. Proposed mitigation: adopt the Data Architect seat, or add `data` to Builder's or another seat's `qualified_layers` through a role proposal. |
| ARCHITECT gap 8 | **Approved intent is not in my inputs.** Intent Owner's outputs list "approved intent, business case, users and use cases, UX design and increment plan" for Architect. My inputs list only `users-use-cases` and `business-case`. The `intent` artifact is absent. Floor C1 requires the intent to name the problem, users and Intent Owner. Without it as a formal input, a fresh session authoring my architecture may miss the intent's constraints. Proposed fix: add `{artifact: intent, from: Product}` (approved) to my inputs. |
| ARCHITECT gap 9 | **Verifier's inputs use a catch-all for NFR.** Verifier's inputs do not list `nfr from Architect` explicitly; they rely on "any artifact in review from Product." NFR is authored by me (Architect), not Product. The catch-all may not cover it in a fresh Verifier session's task manifest. Proposed fix: add `{artifact: nfr, from: Architect}` to Verifier's explicit inputs. (Not my job to fix, but raises the issue here.) |
| ARCHITECT gap 10 | **Shared layer ownership between Architect and Operator.** I qualify for `deployment-runtime` and `integration`; so does Operator. Neither job description specifies which seat authors vs. challenges each of these layers on a given artifact. Without a stated convention, two sessions could both author sections of the same layer. See also METHOD gap 6. |
| METHOD gap 1 | **domain-core and qualified_domains are both empty.** No seat can author or challenge the domain-core layer. `qualified_domains` is also `{}`. Any product with domain-specific logic will fail D6 and C8. A crew review is mandated by CLAUDE.md §Rules that stay with judgment ("A gap that no seat can judge opens a crew review"). No one is chartered to trigger that review proactively. |
| METHOD gap 2 | **Approved artifact routing to Builder is ambiguous.** My outputs list architecture `for: Builder`. Engineering Lead's outputs list "approved architecture … for Builder." After approval, should Builder read my version or wait for Engineering Lead to re-file it? The status field answers this implicitly (read when status: approved), but the double listing creates confusion about who is responsible for the Builder-ready artifact. |
| METHOD gap 3 | **Role-proposal peer review obligation is undiscovered.** Under E17, every agent seat that sends input to or consumes output from a proposed new seat must provide an independent peer review. I send input to and consume output from many seats. If a new seat is proposed that intersects with mine (e.g., a domain expert who consumes my NFR), I am obligated to peer-review the proposal. No mechanism notifies me that a proposal is in-review; I would only know if I read Delivery's output or the `docs/crew/` folder. |
| METHOD gap 4 | **Frontend layer tiebreaker between Architect and Designer is absent.** Both I and the Designer qualify for `frontend`. If my frontend architecture section and the Designer's UX flows conflict, no seat has authority to decide. CLAUDE.md says "where a diagram and its text disagree, the diagram governs structure"; but this applies within an artifact, not across artifacts from different seats. |
| METHOD gap 5 | **D6 enforcement does not confirm the right qualified seat actually challenged each section.** SEATS checks declared seats in front matter. It does not verify that the declared challenger is actually qualified for each layer per their `qualified_layers`. A session could declare an unqualified challenger in the front matter and the check would not catch it. E16 checks diagrams; SEATS checks separation. The cross-check of "challenger declared vs. challenger qualified per layer" has no dedicated check. |
| METHOD gap 6 | **Shared layer authoring convention is undefined.** For `deployment-runtime` and `integration`, both I and Operator qualify. Neither job description states a convention for who authors vs. challenges each layer on a given architecture. Floor D6 requires one author and one challenger, both qualified and distinct. Without a stated convention, this is resolved ad hoc each session. |
| METHOD gap 7 | **No escalation path for blocked human seats, mirroring Product's METHOD gap 1.** Engineering Lead and Intent Owner are the same person. If blocked, STATE.md records the open decision but no escalation authority is named. The process stalls with no defined recovery path. |
