# DRYRUN-JOBREVIEW — Delivery

## Context visible to this session

### Project instruction files in context

1. **CLAUDE.md** (the Constitution, `/CLAUDE.md`) — mission and principles slots are
   unfilled template placeholders (`{{double braces}}`); bootstrap has not run. Core rules
   in effect: session protocol (read CLAUDE.md + STATE.md + input manifest only; work on
   own branch; no git stash; commit before ending); five-role artifact chain (Consulted →
   Author → Challenger → Approver → Consumer); governance (agents branch and PR only,
   never push to main); single-principal disclosure (Intent Owner and Engineering Lead are
   one person, no independent review at this stage).

2. **STATE.md** (`/STATE.md`) — cycle 1, setup phase. `active_tracks: []`. No open
   decisions. No mid-task work. Product description field is empty; bootstrap has not run.

3. **No task input manifest in the repository.** This session received its task via the
   conversation prompt. Per session protocol rule 1: "Read, in order: this file, STATE.md,
   and the input manifest of your task." No manifest exists as a repository artifact. I
   proceed from the files and treat the prompt as advisory context. Recording this
   deviation here.

### Notes about the person (from session context)

- Email: imran.canuck@gmail.com (used for authorship and attribution only)
- Git user: PublicEnemage
- Holds: Intent Owner seat and Engineering Lead seat (listed as "Human 1" in
  `docs/roles.yml`; bootstrap name substitution has not occurred)
- Single-principal disclosure applies (CLAUDE.md Governance): one person holds both human
  seats; no independent review is available at this governance stage

---

## 1. My own job (Delivery seat)

Source: `docs/roles.yml` lines 80–98. I review each field and state keep or change.

### trigger

> "An increment plan is approved; a cycle starts or exits; a flow metric breaches its
> limit; a seat gap needs a role proposal"

**KEEP with a note.** Four distinct events across two categories: process lifecycle
(plan approved, cycle starts/exits) and exception handling (metric breach, seat gap).
Each maps cleanly to one of my outputs. However, "a flow metric breaches its limit"
presupposes that limits are set. Nothing in `docs/dor/floor.yml`, `docs/artifact-types.yml`,
or my job definition specifies what the metrics are or what constitutes a breach. The
trigger is well formed but depends on content that does not yet exist.
(DELIVERY gap 3)

---

### inputs

| # | Artifact | From | Decision |
|---|---|---|---|
| 1 | increment-plan | Product | **KEEP** — this is my primary input for cutting work |
| 2 | story | Product | **CHANGE** — see below |
| 3 | audit of process adherence | Steward | **KEEP** — needed to close the adherence feedback loop |

**On input 2 (story from Product):** The delivery-system I author sets the story
template, hierarchy and cadence that Product must follow when writing stories. Listing
story as an input I receive, while I am also the one who defines the format stories must
conform to, makes story-writing a shared responsibility that is currently unsettled. Two
coherent models exist:

- *Model A*: Product writes stories using my delivery-system template; I receive and order
  them. Story is an input to me from Product.
- *Model B*: I cut stories from the increment-plan myself, using the delivery-system I own.
  Story is an output from me to Builder, not an input from Product.

Product's job lists story in its templates and Delivery's inputs list story from Product
— this supports Model A. But Product's outputs do not list story as an explicit output
(PRODUCT gap 3, identified by the Product seat review). Until that gap is closed,
this input is partially unanchored. I accept it as stated, on condition that Product's
outputs list `story for Delivery`.

**Missing input:** `delivery-system` is my own output; I do not need it as an input.
No other missing inputs found after checking all other seats' outputs that target
Delivery.

---

### value

> "Owns the delivery process: hierarchy, story template, prioritization rule, cadence,
> track cap and metrics computed from the repository. Cuts and orders work so that every
> task a fresh session pulls carries its own input manifest"

**KEEP the framing; note a scope gap.** "Cuts and orders work so that every task a fresh
session pulls carries its own input manifest" implies that the consumers of my cut work
are builder sessions and other agent sessions. But my outputs list only `delivery-system
for Product` and `role-proposal for Engineering Lead`. Neither output is the cut work
itself (the stories with input manifests). If I produce stories with manifests as part of
my "cuts and orders work" duty, those stories need to appear in my outputs, and their
consumer (Builder or the session that pulls them) needs to be named.
(DELIVERY gap 2)

"Metrics computed from the repository" is technically precise but the metrics themselves
are unspecified — only in the delivery-system artifact I author will they be defined.
(DELIVERY gap 3)

---

### outputs

| # | Artifact | For | Decision |
|---|---|---|---|
| 1 | delivery-system | Product | **KEEP with a note** — see below |
| 2 | role-proposal | Engineering Lead | **KEEP** |

**On output 1 (delivery-system for Product):** The acceptance test reads "Names
hierarchy, story template, prioritization rule, cadence, track cap and metrics (floor P5)."
Floor P5 is a single gate row covering six distinct things. The delivery-system artifact
is both the tool I use to define the process and the artifact Product reads to know how
to write stories and what cadence to follow. The consumer is listed as Product, but the
primary consumers of the delivery-system are Builder (which needs to know what stories
look like) and all sessions (which need to know track cap and cadence). Listing only
Product as the consumer understates the reach of this artifact.

**Missing output:** As my value statement says I cut work so sessions can pull it, I
should have a `story for Builder` or `story (with input manifest) for [session pulling
it]` output. Currently absent. (DELIVERY gap 2)

---

### standards

`docs/dor/floor.yml` and `docs/artifact-types.yml`

**KEEP.** These are the right references. Floor P5 governs what the delivery-system must
name; `docs/artifact-types.yml` governs its naming, location and required front matter.

---

### templates

`docs/templates/delivery-system.md` and `docs/templates/role-proposal.md`

**KEEP.** Both templates match my outputs. No extra templates are in the list and no
missing templates are apparent.

---

### verifier

Seat: Steward. Evidence: "Cadence, track cap (E9) and story template use audited at each
cycle exit; metrics recomputed from the repository, never self-reported"

**KEEP.** Steward holds no artifact seat by design (`holds_no_artifact_seat: true`),
making it the only seat that can audit Delivery without being an author or approver of
any artifact Delivery produces. The evidence — cadence, track cap (E9 partial),
story template use, metrics from repository — is specific and objective. The constraint
"never self-reported" closes the gap that would let me declare my own metrics compliant.

**Note on E9:** E9 is partial: size and track caps are implemented; shared-state lane
checks ship with E7, which is planned for v0.2. Until E7 ships, the track-cap portion of
my verifier evidence is partially mechanised and partially advisory.

---

### qualified_layers

`[]`

**KEEP.** Delivery works at the process level, not at any architecture layer. This is
correct. Consequence: I cannot author or challenge any layer section, and I cannot sit as
D6 qualified-seat on any architecture artifact.

---

### What I cannot do as written

1. Author or challenge any architecture layer — `qualified_layers` is empty.
2. Trigger myself — the trigger "an increment plan is approved" requires either the
   harness (E7, planned) or a human to start my session. No automatic notification is
   currently wired.
3. Measure my own compliance — verifier is Steward; I must not self-report metrics.
4. Approve my own artifacts — `delivery-system` is `human_approver: true`; I am the
   author, never the approver.
5. Define the metrics I am responsible for computing — metrics are defined inside the
   delivery-system I author, but no baseline metric set exists in any standing document
   before I author the first delivery-system. I am defining and measuring in the same
   artifact.

---

### What I would refuse to accept as input

1. An increment-plan that does not name the use cases each increment demonstrates — floor
   P1 requires this; a plan that omits it cannot feed my story-cutting duty.
2. A story written without a delivery-system in effect — I cannot verify that the story
   format is correct if my delivery-system has not been authored and approved first.
3. An audit from Steward that is self-described rather than backed by file or check
   results — the acceptance test for the audit artifact reads "names each deviation with
   the file or check result that shows it"; a narrative without evidence is not an audit.
4. A task with no input manifest — floor I7 requires every task to carry its own manifest.
   I apply this rule to myself and to every task I cut.
5. A request to approve my own delivery-system — human_approver is true; the Engineering
   Lead is the approver.

---

## 2. The other seats

### Intent Owner

**Recommendation: Accept**

*What I hand to them:* nothing directly.

*What I take from them:* nothing directly — they approve the increment-plan that Product
sends and that I consume, but that approval is implicit in the artifact's status.

*Overlap:* None. Intent Owner approves business artifacts; Delivery owns process shape.

*Wiring check:* Clean. I consume an approved increment-plan; Intent Owner is the approver.
No direct artifact flows in either direction between us.

---

### Engineering Lead

**Recommendation: Accept**

*What I hand to them:* `role-proposal` (when a seat gap is identified). Their inputs list
`{artifact: delivery-system, from: Delivery}` as one of five inputs they approve.

*What I take from them:* approval of the delivery-system (implicit via status) and of any
role-proposal I submit.

*Overlap:* None. Engineering Lead approves engineering and governance artifacts;
I author them.

*Wiring check:* My outputs list role-proposal for Engineering Lead. Engineering Lead's
inputs list delivery-system from Delivery. Both are present. Clean.

---

### Product

**Recommendation: Accept with conditions**

*What I hand to them:* `delivery-system` — my primary output, which defines the story
template, hierarchy, prioritization rule, cadence, track cap and metrics Product must
follow.

*What I take from them:* `increment-plan` (listed in my inputs) and `story` (listed in my
inputs; absent from Product's outputs — see PRODUCT gap 3 in the Product job review).

*Overlap:* The boundary between my seat and Product is the line between process ownership
and content ownership. I decide how work is cut and ordered; Product decides what work
exists. Potential confusion arises at story-writing: Product writes stories but must
conform to my template. If Product writes a story that does not meet the delivery-system
template, I must flag it rather than rewrite it — content decisions belong to Product.

*Wiring check:*
- Delivery outputs `delivery-system for Product` → Product does not list
  `delivery-system from Delivery` as an input (PRODUCT gap 4, identified in the Product
  review). This is a gap on Product's side, not mine.
- Product outputs `increment-plan for Delivery` → listed in my inputs. Clean.
- Product lists `story` in its templates; Delivery lists `story from Product` in inputs.
  Product's outputs omit story (PRODUCT gap 3). Gap on Product's side.

*Conditions:*
1. Product must add `story for Delivery` to its outputs.
2. Product must add `delivery-system from Delivery` to its inputs.
Until those fixes land, my input #2 (story from Product) is partially unanchored.

---

### Architect

**Recommendation: Accept**

*What I hand to them:* nothing directly.

*What I take from them:* nothing directly. Architect outputs go to Builder and Product.

*Overlap:* None. Architect shapes the system; Delivery shapes the process.

*Wiring check:* Clean. No direct artifact flows between Delivery and Architect are
declared in either seat's job.

*Note:* The architecture drives the increment structure indirectly — the increment-plan
Product sends me should already be consistent with the architecture. If it is not, that
gap surfaces at the plan gate (floor P2: "Architecture, test and implementation backlogs
trace to increments"), judged by the Engineering Lead. I have no direct recourse to
Architect myself.

---

### Designer

**Recommendation: Accept**

*What I hand to them:* nothing directly.

*What I take from them:* nothing directly. Designer outputs go to Builder.

*Overlap:* None.

*Wiring check:* Clean. No direct flows between Delivery and Designer.

---

### Verifier

**Recommendation: Accept**

*What I hand to them:* nothing directly. Verifier reviews all artifacts in-review,
including my delivery-system when I set it to in-review, but this is triggered by the
artifact status, not by a direct hand-off in my job.

*What I take from them:* the review finding on my delivery-system artifact (findings
answered item by item, per E10). This is not listed in my inputs — it is an implicit
input that arrives through the review cycle.

*Overlap:* Verifier authors the test-strategy; I own the story template and track cap.
These interact when a story's acceptance criteria are written to be testable under the
test-strategy, but the interaction is managed through the template and floor I1, not
through a direct authority overlap.

*Wiring check:* Verifier's outputs do not list a review going to Delivery explicitly.
The review artifacts target Product and Architect by name. Delivery's delivery-system
artifact would need a review file beside it (required by the artifact chain in CLAUDE.md),
but no seat's outputs list `review for Delivery`. This is a process gap: Verifier reviews
all artifacts, but the job description only names review outputs for Product and Architect.
(DELIVERY gap 4)

---

### Builder

**Recommendation: Accept with conditions**

*What I hand to them:* stories with input manifests (per my value statement: "every task
a fresh session pulls carries its own input manifest"). But this is not listed in my
outputs. Builder's inputs do not list any artifact from Delivery; they list
`increment-intent from Product`, `architecture from Architect`, `test-strategy from
Verifier`, `cicd from Operator`.

*What I take from them:* nothing directly.

*Overlap:* I cut and order the work; Builder implements it. The boundary is clear in
principle but the wiring is missing: Builder does not list any Delivery artifact as an
input, and I do not list any output for Builder. If I produce stories with manifests, who
are they for? The value statement implies Builder sessions are the consumers, but no
formal artifact flow names this.

*Conditions:*
1. Add `story (with input manifest) for Builder` to my outputs, or clarify whether
   stories-with-manifests are an output of Delivery or Product.
(DELIVERY gap 2)

---

### Operator

**Recommendation: Accept**

*What I hand to them:* nothing directly.

*What I take from them:* nothing directly.

*Overlap:* None. Operator owns security, deployment and run; Delivery owns process and
flow.

*Wiring check:* Clean. No direct artifact flows between Delivery and Operator.

---

### Steward

**Recommendation: Accept**

*What I hand to them:* nothing explicitly — Steward audits my process adherence
rather than receiving an artifact from me. My delivery-system is what they audit.

*What I take from them:* `audit of process adherence` (listed in my inputs). The
acceptance test reads "Names each deviation with the file or check result that shows it."

*Overlap:* None. Steward audits; Delivery owns process. Steward holds no artifact seat,
preserving the independence needed to audit my artifacts.

*Wiring check:* Steward's outputs list `audit of process adherence for Delivery` →
listed in my inputs. Clean. Steward's inputs list `delivery-system from Delivery` →
Steward's inputs include `{artifact: delivery-system, from: Delivery}`. Clean.

---

## 3. Help protocol

### What I offer each seat and when

| Seat | What I offer | When |
|---|---|---|
| Intent Owner | Nothing directly | — |
| Engineering Lead | delivery-system for review; role-proposals when a seat gap is identified | After I draft the delivery-system; when a crew review is needed |
| Product | Approved delivery-system (story template, cadence, hierarchy, track cap, metrics) | Before Product writes the first story in any increment |
| Architect | Nothing directly | — |
| Designer | Nothing directly | — |
| Verifier | delivery-system artifact set to in-review with all template fields populated | When I complete the delivery-system draft |
| Builder | Stories with input manifests, ordered by priority | After the plan gate is met and an increment begins |
| Operator | Nothing directly | — |
| Steward | Clean process trail: status transitions recorded, artifacts in correct folders, parents cited, metrics from repository not self-reported | Continuously; especially at each cycle exit |

### What I ask of each seat, where I write the request, and how long I wait

| Seat | What I ask | Where I write the request | Wait limit | Escalate to |
|---|---|---|---|---|
| Intent Owner | Approval of delivery-system (human_approver: true) | Artifact set to `in-review`; note in STATE.md if blocked | Not defined — same holder as Engineering Lead; no independent escalation path | STATE.md open decision; record as METHOD gap (see §5, gap 1 from Product review) |
| Engineering Lead | Approval of delivery-system and role-proposals | Artifact front matter; STATE.md if blocked | Same issue | Same |
| Product | Approved increment-plan before I cut stories; stories that conform to the delivery-system template | Task manifest for Product session; review finding if a story does not conform | One cycle | Steward (flag non-conformance in audit trail) |
| Verifier | Review of my delivery-system artifact | Artifact set to in-review; review file path recorded in STATE.md | One cycle | Steward |
| Steward | Audit of process adherence at each cycle exit | No explicit request mechanism — Steward triggers on cycle exit (its own trigger) | — | Engineering Lead if audit is overdue |

---

## 4. Authority

### What I decide alone

- Hierarchy: the work breakdown structure above story level (epic, theme, or equivalent)
- Story template: what fields a story must carry, subject to floor I7 (input manifest)
- Prioritization rule: how stories are ordered in the backlog, given an approved
  increment-plan
- Cadence: cycle length and track cap, within the constraints E9 enforces
- Metrics: which repository-derived metrics to compute and at what frequency
- Whether a story carries a complete input manifest (floor I7 check)
- Whether an increment-plan names use cases per increment (floor P1 check)
- When to open a role-proposal for a seat gap I observe

### What I decide only after consulting

| Decision | Consult | Reason |
|---|---|---|
| Track cap that constrains an active increment | Engineering Lead | Track cap affects merge rules and branch strategy; E9 enforces it, Engineering Lead approves |
| Metrics that require code instrumentation | Architect | If a metric needs a new measurement point in the system, that is an architectural decision |
| Whether a gap in the process requires a new role vs. a new rule or tool | Engineering Lead | CLAUDE.md: "Prefer a rule or a tool to a new role." I identify the gap; Engineering Lead decides the response |
| Changing the story template mid-cycle | Product | Product writes stories to my template; a mid-cycle change affects in-flight work |

### When I ask before acting

- Before opening a role-proposal for a new seat: I ask whether a rule or tool would close
  the gap first (CLAUDE.md: "Prefer a rule or a tool to a new role")
- Before declaring a metric limit breached: I verify the metric from the repository, not
  from a summary
- Before ordering stories in a way that drops a use case from the next increment: I
  confirm with Product that the ordering does not contradict the approved increment-plan
- Before starting any work without an approved delivery-system: I wait or flag the gap
  rather than proceeding on informal conventions

### What I would refuse

- Approving my own delivery-system — human_approver: true; the Engineering Lead approves
- Self-reported metrics — the verifier's evidence states "metrics recomputed from the
  repository, never self-reported"; I apply this to my own outputs too
- A story without an input manifest — floor I7 is a gate-level rule; I will not cut a
  task that a fresh session cannot pull without reading prior conversation
- A "continue" decision backed only by conversation, not by an artifact in the repository
  (CLAUDE.md rule 3: "A decision counts only once it is written to a named artifact")

### Where the procedure left me less room than my job description implies

My job says I "own the delivery process." In practice:

1. The delivery-system must be approved by the Engineering Lead (human_approver: true for
   `docs/plan/DS-*.md`). I cannot define the process unilaterally; I propose it.
2. The story template I define must still produce stories that satisfy floor I7, I1, I4 —
   rows judged by Verifier and Delivery (I7 is judged by Delivery). I have latitude in
   the template's form but not in its required content.
3. The metrics I choose must be computable from the repository. If a metric requires
   instrumentation not yet in the system, I cannot use it until the Architect and Builder
   implement the measurement. I may identify needed metrics but cannot produce them alone.
4. Track cap is enforced by E9 (partial). Until E7 ships, the shared-state lane portion
   of the cap is advisory, not enforced. My authority to set the cap is real; my ability
   to have it mechanically enforced is not yet complete.

---

## 5. Guessing log

Every point where the procedure left me without a clear answer. Labels: DELIVERY = a gap
in my job description or its wiring; METHOD = a gap in the process design visible from my
seat.

| Label | Description |
|---|---|
| DELIVERY gap 1 | **Story authorship is unsettled.** My inputs list `{artifact: story, from: Product}`, and Product's templates include `story.md`. But Product's outputs do not list story as an explicit output (PRODUCT gap 3 from the Product review). Delivery's value says it "cuts and orders work," implying stories are Delivery's output. Both cannot be true without qualification. Proposed resolution: Product writes stories to Delivery's template (Model A); Delivery's role is to receive, verify manifest completeness (floor I7), order and track — not to author stories. But this must be made explicit in both seats. |
| DELIVERY gap 2 | **Stories with input manifests have no named consumer in my outputs.** My value statement says every task a fresh session pulls carries its own input manifest. The consumers of those tasks are Builder sessions and other agent sessions. Yet my outputs list only `delivery-system for Product` and `role-proposal for Engineering Lead`. The cut work — stories with manifests — is not listed as an output. Builder's inputs do not list any artifact from Delivery. Proposed fix: add `{artifact: story (with input manifest), for: Builder, acceptance: "Carries an input manifest; traceable to an approved increment; meets the delivery-system story template"}` to my outputs. |
| DELIVERY gap 3 | **Metrics are undefined before the first delivery-system is authored.** Floor P5 and my value statement require metrics computed from the repository, but no standing document names the metrics or their thresholds before I write the first delivery-system. The trigger "a flow metric breaches its limit" cannot fire until limits exist. The delivery-system artifact is where I define them, but I have no baseline to anchor the first version against. |
| DELIVERY gap 4 | **No seat's outputs name a review directed to Delivery.** The artifact chain (CLAUDE.md) requires a review file beside each artifact. My delivery-system will reach in-review and Verifier will review it, but Verifier's outputs name only `review for Product` and `review for Architect`. A review going to Delivery is implied but not formally declared. Proposed fix: add `{artifact: review, for: Delivery, acceptance: "Each finding has a severity, and open_findings counts what is unanswered"}` to Verifier's outputs. (This is a Verifier job gap, not mine to fix, but I name it here.) |
| METHOD gap 1 | **No automatic trigger mechanism.** E7 (harness hooks: worktree pin, stash filter, commit on stop) is planned for v0.2. Until it ships, Delivery must be started by a human observing that an increment-plan has been approved. The trigger "an increment plan is approved" is correct in intent but requires human initiation in v0.1. |
| METHOD gap 2 | **Metric breach threshold has no agreed floor.** The trigger "a flow metric breaches its limit" requires limits to be set in the delivery-system. Until the first delivery-system is approved, no limit exists. There is a bootstrapping dependency: I cannot trigger on a breach before the delivery-system defines the limits; the delivery-system cannot be authored before an increment-plan is approved; but the delivery-system should logically precede the increment-plan's execution. The trigger order in the procedure is: increment-plan approved → Delivery authors delivery-system → metrics defined. Until that first cycle completes, the metric-breach trigger is dormant. |
