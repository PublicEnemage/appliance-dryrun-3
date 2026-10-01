# DRYRUN-JOBREVIEW — Product

## Context visible to this session

### Project instruction files in context

1. **CLAUDE.md** (the Constitution, `/CLAUDE.md`) — mission and principles slots are
   unfilled template placeholders (`{{double braces}}`); bootstrap has not run. Core
   rules in effect: session protocol (read CLAUDE.md + STATE.md + input manifest only;
   work on own branch; no git stash; commit before ending); the five-role artifact chain
   (Consulted → Author → Challenger → Approver → Consumer); governance (agents branch
   and PR only, never push to main); single-principal disclosure (Intent Owner and
   Engineering Lead are one person, no independent review at this stage).

2. **STATE.md** (`/STATE.md`) — cycle 1, setup phase. `active_tracks: []`. No open
   decisions. No mid-task work. Product description field is empty (bootstrap has not
   run; the description was never written here).

3. **No task input manifest in the repository.** This session received its task via the
   conversation prompt. Per BOOTSTRAP.md §Files on disk are the truth: "If text placed
   in a session's context … differs from the files, the files win. The session records
   the difference in its log." Recorded here. I proceed from the files and treat the
   prompt as advisory context.

### Notes about the person (from session context)

- Email: imran.canuck@gmail.com (used for authorship and attribution only)
- Git user: PublicEnemage
- Holds: Intent Owner seat and Engineering Lead seat (listed as "Human 1" in
  `docs/roles.yml` holders; the name substitution that bootstrap performs has not
  happened yet)
- Single-principal disclosure applies (CLAUDE.md Governance): one person holds both
  human seats; no independent review is available at this stage

---

## 1. My own job (Product seat)

Source: `docs/roles.yml` lines 59–79. I review each field and say keep or change.

### trigger

> "The Intent Owner supplies a problem and discovery starts; an increment plan is due
> before the plan gate; an increment ends and needs a verdict"

**KEEP.** Three distinct trigger events, one per output class: users-and-use-cases on
discovery, increment-plan before the plan gate, validation-verdict after an increment.
Clear enough that a fresh session knows when to activate without reading prior
conversation.

---

### inputs

| # | Artifact | From | Decision |
|---|---|---|---|
| 1 | product description or problem statement | Intent Owner | **KEEP** |
| 2 | review | Verifier | **KEEP** |
| 3 | architecture | Architect | **KEEP** — needed to write increment-intent even though increment-intent is not yet listed in my outputs (see gap below) |
| 4 | increment verify evidence | Builder | **CHANGE** — this artifact flows Builder → Verifier, not Builder → Product. Verifier's outputs list `verification evidence for Product`. My input should read `{artifact: "verification evidence", from: Verifier}` |

Two additional inputs are missing from the list but appear in other seats' outputs
that target Product:

- `delivery-system from Delivery` — Delivery outputs it `for: Product`; absent from my
  inputs (see PRODUCT gap 4 in §5)
- `conceptual-design from Architect` — Architect outputs it `for: Product` with
  acceptance "Every use case maps to a system capability (floor D1)"; absent from my
  inputs (see PRODUCT gap 5 in §5)

---

### value

> "Turns the problem into users, use cases with main, alternate and failure paths, kill
> boundaries and an increment plan that demonstrates use cases, then turns the Verifier's
> evidence into a validation verdict. Owns backlog content"

**KEEP with a note.** Accurate for what it covers, but it is silent on increment-intent
and story, both of which appear in my templates and are consumed from Product by Builder
and Delivery respectively. The value statement understates the scope of my authoring
duties. I propose adding: "…and writes the increment-intent and stories that carry work
to Builder."

---

### outputs

| # | Artifact | For | Decision |
|---|---|---|---|
| 1 | intent, business case, users and use cases | Architect | **KEEP** — acceptance cites floor C3 and C7, which is correct |
| 2 | increment-plan | Delivery | **KEEP** |
| 3 | validation-verdict | Intent Owner | **KEEP** — acceptance says "cites the Verifier's evidence"; correct once input gap 4 is fixed |

Two outputs are missing:

- `increment-intent for Builder` — Builder's first input is `{artifact: increment-intent,
  from: Product}`; the template `docs/templates/increment-intent.md` is in my list. Not
  in my outputs (PRODUCT gap 2).
- `story for Delivery` — Delivery's inputs list `{artifact: story, from: Product}`; the
  template `docs/templates/story.md` is in my list. Not in my outputs (PRODUCT gap 3).

---

### standards

`docs/dor/floor.yml` and `docs/artifact-types.yml`

**KEEP.** Correct. These are the right references for DOR compliance and artifact
naming/location.

---

### templates

`docs/templates/intent.md`, `business-case.md`, `users-use-cases.md`,
`increment-plan.md`, `increment-intent.md`, `story.md`, `validation-verdict.md`,
`benefits-check.md`

**KEEP the list.** All eight are appropriate. The mismatch is that `increment-intent.md`
and `story.md` produce outputs not yet listed in the outputs section, and
`benefits-check.md` has no owner in any seat's outputs (see METHOD gap 5 in §5).

---

### verifier

Seat: Verifier. Evidence: "A review file beside each Product artifact, answered item by
item (E10); every use case lists its failure paths (floor C7)"

**KEEP.** Verifier and Product are an incompatible pair, ensuring independence. E10 and
floor C7 are the right evidence points for my artifact type.

---

### qualified_layers

`[]`

**KEEP.** Product does not qualify to author or challenge any architecture layer. This is
intentional: I work at the problem and use-case level, not the implementation level.
Consequence: I cannot sit as challenger on any architecture artifact (floor D6).

---

### What I cannot do as written

1. Author or challenge any architecture layer — `qualified_layers` is empty.
2. Hold the Verifier seat simultaneously — incompatible pair.
3. Hold the Builder seat simultaneously — incompatible pair.
4. Approve my own artifacts — human_approver is true for all my artifacts; I am always
   the author, never the approver.
5. Judge domain-specific correctness in use cases — `qualified_domains` is empty; no
   seat has domain knowledge listed. I can write use cases but cannot assert their
   domain accuracy, and no challenger can confirm them under floor C8.

---

### What I would refuse to accept as input

1. A problem statement with no user or market evidence — floor C9 requires evidence from
   real users or the market, not agent opinion alone. I will draft use cases but the
   business case will fail the case gate.
2. `increment verify evidence` directly from Builder — that artifact is addressed to the
   Verifier, not to me. I flag the routing error and request the Verifier's
   `verification evidence` instead.
3. An architecture in `draft` or `in-review` as a basis for an increment plan — I
   require an approved architecture to avoid planning against a moving design.
4. A problem statement with no worthwhile conditions or kill boundaries — I cannot
   produce a business case that will pass floor C2 without them, and I will not invent
   thresholds the Intent Owner has not stated.
5. A request to approve my own artifacts — author and approver must be different seats;
   my approver is always the Intent Owner (human, human_approver: true).
6. A task with no input manifest — floor I7 requires every task to carry its own input
   manifest; I will not act on conversation context alone.

---

## 2. The other seats

### Intent Owner

**Recommendation: Accept**

*What I hand to them:* draft intent, business case, users-and-use-cases, increment-plan
(all for approval); validation-verdict after each increment.

*What I take from them:* product description or problem statement; approval of each
artifact I submit in-review.

*Overlap check:* None. Intent Owner approves; Product authors. Intent Owner's outputs
list "approved intent, business case, users and use cases, UX design and increment plan
for Architect" — same content I produce, after approval. Flow is correct: I author →
they approve → they forward (approval status is the signal) to Architect.

*Wiring check:* After Intent Owner approves my artifacts, no formal artifact is sent
back to me confirming approval. I infer approval from the artifact's status field
changing to `approved`. This is implicit (METHOD gap 2 in §5).

---

### Engineering Lead

**Recommendation: Accept**

*What I hand to them:* nothing directly — they approve engineering artifacts (architecture,
test-strategy, cicd, delivery-system) that are not authored by me.

*What I take from them:* nothing directly — their approvals unlock gates, but no artifact
flows to Product.

*Overlap:* None. Engineering Lead approves engineering artifacts; Product authors product
artifacts.

*Wiring check:* Clean. Engineering Lead receives architecture, test-strategy, cicd,
delivery-system, role-proposal — none originated by Product.

---

### Delivery

**Recommendation: Accept with conditions**

*What I hand to them:* increment-plan (listed); story (in my templates and in Delivery's
inputs from Product, but absent from my outputs — gap).

*What I take from them:* delivery-system (Delivery outputs it for Product; absent from my
inputs — gap).

*Overlap:* None. Delivery owns process shape and cadence; Product owns backlog content.
The boundary is: I decide what work exists; Delivery decides how it is cut and ordered.

*Conditions:*
1. Add `story for Delivery` to my outputs.
2. Add `delivery-system from Delivery` to my inputs.

---

### Architect

**Recommendation: Accept with conditions**

*What I hand to them:* approved users-use-cases and business-case (they flow from Intent
Owner to Architect after approval, but I am the author).

*What I take from them:* architecture (listed in my inputs); conceptual-design (Architect
outputs it for Product with acceptance "Every use case maps to a system capability",
floor D1 — absent from my inputs).

*Overlap:* None. Architect shapes the system; Product frames the problem.

*Conditions:*
1. Add `conceptual-design from Architect` to my inputs.

---

### Designer

**Recommendation: Accept**

*What I hand to them:* users-use-cases (Designer's first input from Product).

*What I take from them:* nothing directly — Designer outputs ux-design and design-system
to Builder.

*Overlap:* None. Designer governs visual and interaction decisions; Product governs use
case content.

*Note:* Intent Owner approves "UX design" (listed in their outputs), but the Designer
sends ux-design to Builder. The path by which Intent Owner sees and approves it before
Builder receives it is not traced in any seat's job description. Not my gap to close, but
it affects increment planning if the UX design is approved late (METHOD gap 3 in §5).

---

### Verifier

**Recommendation: Accept with conditions**

*What I hand to them:* every artifact I author, set to in-review, for review — in
particular users-use-cases (Verifier's evidence cites floor C7, failure paths).

*What I take from them:* review for each artifact (findings answered item by item);
verification evidence (basis for my validation-verdict).

*Overlap:* None (incompatible pair).

*Conditions:*
1. Correct my input #4 from `increment verify evidence from Builder` to
   `verification evidence from Verifier`.

---

### Builder

**Recommendation: Accept with conditions**

*What I hand to them:* increment-intent (Builder's first input lists `{artifact:
increment-intent, from: Product}`; absent from my outputs — gap).

*What I take from them:* nothing I should receive directly. Builder sends `increment
verify evidence` to Verifier, not to me.

*Overlap:* None (incompatible pair).

*Conditions:*
1. Add `increment-intent for Builder` to my outputs.
2. Remove `increment verify evidence from Builder` from my inputs.

---

### Operator

**Recommendation: Accept**

*What I hand to them:* nothing directly.

*What I take from them:* nothing directly.

*Overlap:* None. Operator owns security, deployment and run; Product owns use cases and
backlog.

*Note:* At release, Intent Owner receives both my validation-verdict and Operator's
release-decision before making a continue/stop decision. No coordination mechanism
ensures both artifacts are present simultaneously; it is assumed. This is a METHOD gap
(METHOD gap 4 in §5) but it is between Operator and me, not in either of our job
descriptions.

---

### Steward

**Recommendation: Accept**

*What I hand to them:* nothing directly.

*What I take from them:* nothing directly — Steward audits process adherence and sends
results to Delivery.

*Overlap:* None. Steward holds no artifact seat by design, so it can audit every seat
including mine.

*Note:* Steward's verifier is the Engineering Lead, preserving Steward's independence
from the Verifier chain.

---

## 3. Help protocol

### What I offer each seat and when

| Seat | What I offer | When |
|---|---|---|
| Intent Owner | Draft intent, business case, users-and-use-cases for review; validation-verdict | On discovery trigger; after each increment completes |
| Engineering Lead | Nothing directly; artifacts they receive are via the approval chain | — |
| Architect | Approved users-use-cases and business-case as input manifest items | When the case gate is met |
| Designer | Approved users-use-cases | When use cases are approved and a UI is in scope |
| Verifier | Every artifact I author, set to in-review, with all template fields populated | Each time I complete a draft artifact |
| Delivery | Approved increment-plan; stories per increment | After the plan gate is met; at each increment cut |
| Builder | Approved increment-intent with acceptance criteria per use case | When an increment is approved and ready for implementation |
| Operator | Nothing directly | — |
| Steward | Clean process trail: status transitions recorded, artifacts in correct folders, parents cited | Continuously |

### What I ask of each seat, where I write it, and how long I wait

| Seat | What I ask | Where I write the request | Wait limit | Escalate to |
|---|---|---|---|---|
| Intent Owner | Problem statement with evidence; kill boundary thresholds; approval decisions | Artifact set to `in-review`; note in STATE.md if blocked | Not defined — same holder as Engineering Lead; no independent escalation path exists | **METHOD gap** (see §5, gap 1); record in STATE.md as open decision |
| Engineering Lead | Gate approval on engineering artifacts | Artifact front matter; STATE.md if blocked | Same issue | Same |
| Architect | Approved architecture and conceptual-design | Task manifest for Architect session | One cycle | Steward (audit trail entry) |
| Designer | UX design (when in scope) | Task manifest for Designer session | One cycle | Steward |
| Verifier | Review of each artifact I author | Artifact status `in-review`; review file path in STATE.md | One cycle | Steward |
| Delivery | Delivery-system | Task manifest for Delivery session | One cycle | Steward |
| Builder | Implementation via increment-intent | Task manifest for Builder session | One cycle | Steward |

---

## 4. Authority

### What I decide alone

- How to frame use cases: main path, alternate paths, and failure paths, within the scope
  the Intent Owner has set
- Which users to list and what to name each use case, given the problem statement
- Backlog ordering by value, within the approved business case
- Whether Verifier evidence is sufficient to declare accept or reject per use case in a
  validation-verdict
- Whether an artifact meets its own template requirements before I set it to in-review

### What I decide only after consulting

| Decision | Consult | Reason |
|---|---|---|
| Kill boundary is close to being crossed | Intent Owner | Kill boundaries are theirs to set (floor C2); I surface evidence, they decide |
| Architecture constraints narrow a use case | Architect | I cannot judge architectural feasibility alone; `qualified_layers` is empty |
| Acceptance criteria depend on NFR thresholds | Verifier | Verifier authors the test strategy; my criteria must be testable under it |
| A new role is needed to fill a domain gap | Steward (flag), Engineering Lead (decide) | Crew reviews are governed by Engineering Lead; I file the gap, not resolve it |

### When I ask before acting

- Before adding a use case not traceable to the Intent Owner's problem statement
- Before marking any artifact `approved` (I am always the author; the approver is a
  different seat)
- Before reducing scope below what the Intent Owner approved
- Before proceeding past floor C8 when `qualified_domains` is empty and the use cases
  have domain-specific content that no seat can challenge

### What I would refuse

- A validation-verdict without formal verification evidence from the Verifier
- Approving any artifact I authored (author and approver must differ; human_approver is
  true for all my artifacts)
- Treating a prior-conversation decision as an approved artifact ("A decision counts only
  once it is written to a named artifact in the repository," CLAUDE.md §3)
- Acting on a task with no input manifest (floor I7)

### Where the procedure left me less room than my job description implies

My job says I "own backlog content." In practice:

1. The delivery-system (authored by Delivery) sets story format, hierarchy, and cadence.
   I author stories but cannot choose the format — I must follow what Delivery has
   defined.
2. `qualified_domains` is empty. If use cases depend on specialized domain knowledge, no
   seat can challenge them under floor C8. I cannot unilaterally move past the case gate;
   a crew review must open first.
3. All my artifacts require human approval (human_approver: true). I can draft and submit
   for review, but I cannot close the loop — the Intent Owner's availability gates every
   artifact I produce.

---

## 5. Guessing log

Every point where the procedure left me without a clear answer. Labels: PRODUCT = a gap
in my job description or the wiring to/from it; METHOD = a gap in the process design
visible from my seat.

| Label | Description |
|---|---|
| PRODUCT gap 1 | **Input artifact mis-named and mis-sourced.** My inputs list `{artifact: "increment verify evidence", from: Builder}`. Builder's outputs send that artifact `for: Verifier`, not for Product. Verifier's outputs list `{artifact: "verification evidence", for: Product}`. Both the artifact name and the sender are wrong. Proposed fix: change to `{artifact: "verification evidence", from: Verifier}`. |
| PRODUCT gap 2 | **increment-intent absent from outputs.** `docs/templates/increment-intent.md` is in my template list. Builder's inputs list `{artifact: increment-intent, from: Product}` as its first input. Yet increment-intent does not appear in my outputs. Proposed fix: add `{artifact: increment-intent, for: Builder, acceptance: "Acceptance criteria testable without reading code; at least one per failure path (floor I1, I4)"}`. |
| PRODUCT gap 3 | **story absent from outputs.** `docs/templates/story.md` is in my template list. Delivery's inputs list `{artifact: story, from: Product}`. Yet story does not appear in my outputs. Proposed fix: add `{artifact: story, for: Delivery, acceptance: "Uses the delivery system's story template; cites the use case it traces to"}`. |
| PRODUCT gap 4 | **delivery-system absent from inputs.** Delivery outputs `{artifact: delivery-system, for: Product}`. Without it as a formal input, I cannot confirm I am using the correct story template or cadence before I author stories. Proposed fix: add `{artifact: delivery-system, from: Delivery}` to my inputs. |
| PRODUCT gap 5 | **conceptual-design absent from inputs.** Architect outputs `{artifact: conceptual-design, for: Product}` with acceptance "Every use case maps to a system capability (floor D1)". Without it as a formal input, I have no artifact basis for confirming the Architect has covered all use cases before I write an increment-plan. Proposed fix: add `{artifact: conceptual-design, from: Architect}` to my inputs. |
| METHOD gap 1 | **No escalation path for blocked human seats.** Intent Owner and Engineering Lead are held by the same person. If that person is unavailable, the process stalls. No escalation authority is named in the procedure for a situation where the only human seats are simultaneously blocked. Recording in STATE.md is described, but no next step is defined. |
| METHOD gap 2 | **Approval signal is implicit.** After the Intent Owner approves my artifact (status → approved), no formal artifact is sent back to Product confirming it. I infer approval from the status field. The procedure does not specify whether Product re-reads the file to confirm or trusts the transition event. |
| METHOD gap 3 | **UX design approval chain is incomplete.** Designer sends ux-design to Builder. Intent Owner's outputs include "UX design" in what they approve for Architect. No seat job describes the step by which Intent Owner sees and approves ux-design before Builder begins using it. As Product, my increment-plans must be consistent with an approved UX design; if that approval is late, I have no artifact to cite. |
| METHOD gap 4 | **Validation-verdict and release-decision reach Intent Owner independently.** I produce the validation-verdict; Operator produces the release-decision. Both feed the Intent Owner's release gate. No coordination role or timing constraint ensures they arrive before the same gate review. The Intent Owner could act on one without the other. |
| METHOD gap 5 | **benefits-check has no owner.** `docs/templates/benefits-check.md` is in my template list. It appears in `docs/artifact-types.yml` with `human_approver: true` in `docs/release`. No seat's job lists it as an explicit output or input. The artifact type exists and has a template, but no seat is chartered to produce or consume it. |
