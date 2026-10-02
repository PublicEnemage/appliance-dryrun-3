# DRYRUN-JOBREVIEW — Operator

## Context visible to this session

### Project instruction files in context

1. **CLAUDE.md** (the Constitution, `/CLAUDE.md`) — mission and principles slots are
   unfilled template placeholders (`{{double braces}}`); bootstrap has not run. Core rules
   in effect: session protocol (read CLAUDE.md + STATE.md + input manifest only; work on
   own branch; no `git stash`; commit before ending; treat conversation as disposable);
   the five-role artifact chain (Consulted → Author → Challenger → Approver → Consumer);
   governance (agents branch and PR only, never push to main); single-principal disclosure
   (Intent Owner and Engineering Lead are one person, no independent review at this stage).
   Advisory rules still pending checks (E2, E6, E4, E8, E12).

2. **STATE.md** (`/STATE.md`) — cycle 1, setup phase. `active_tracks: []`. No open
   decisions. No mid-task work. Product description field is empty (bootstrap has not run).

3. **No task input manifest in the repository.** This session received its task via a
   conversation prompt. Per CLAUDE.md §3: "A decision counts only once it is written to a
   named artifact in the repository." I treat the prompt as advisory input only. This
   divergence is noted below as PRODUCT gap 1.

### Notes about the person (from session context)

- Email: imran.canuck@gmail.com (used for authorship and attribution only)
- Git user: PublicEnemage
- Holds: Intent Owner seat and Engineering Lead seat (listed as "Human 1" in
  `docs/roles.yml`; the name substitution that bootstrap performs has not happened yet)
- Single-principal disclosure applies (CLAUDE.md Governance): one person holds both human
  seats; no independent review is available at this governance stage

---

## 1. My own job (Operator seat)

Source: `docs/roles.yml` lines 180–200. I review each field and say keep or change.

### trigger

> "NFRs and architecture are approved; a deployment is due; a security, privacy or run
> incident opens"

**KEEP with notes.** Three distinct trigger conditions:
1. NFRs and architecture are both approved → I produce the risk assessment and CI/CD approach.
2. A deployment is due → I produce the release decision.
3. A security, privacy or run incident opens → I respond operationally.

**Note 1:** The trigger is silent on ordering. It implies conditions 1 and 2 can fire
independently, but deploying without an approved CI/CD approach would violate floor P3.
The trigger should probably say "NFRs and architecture are approved AND CI/CD is complete
before a deployment is due." See OPERATOR gap 1.

**Note 2:** "A security, privacy or run incident opens" has no named output in my job. My
outputs cover cicd, ops-readiness, and release-decision; none is an incident-response
artifact. What I produce when an incident opens is undefined. See OPERATOR gap 2.

**Note 3:** The trigger does not fire when I receive `increment verify evidence from Builder`.
Yet my inputs include it. A fresh session cannot know when to act on that input if the
trigger does not name the condition. See OPERATOR gap 3.

---

### inputs

| # | Artifact | From | Decision |
|---|---|---|---|
| 1 | nfr | Architect | **KEEP** — NFRs give targets for security, privacy, performance and availability that I translate into CI gates and SLOs. |
| 2 | architecture | Architect | **KEEP** — The deployment topology, integration points and layer boundary decisions shape how I wire the pipeline and what gates it needs. |
| 3 | test-strategy | Verifier | **KEEP** — The test strategy names each gate's owner and tool, so I know which checks to wire where and which ones are the smoke tests I must make reliable. |
| 4 | increment verify evidence | Builder | **KEEP with concern** — I use this to decide whether a deployment is safe and to support the release decision. But the trigger does not tell me when this input arrives or what condition it creates. See OPERATOR gap 3. |

**Missing input 5 — `risk-assessment` from myself (Operator):** My outputs include
`risk-assessment` (implied — see templates listing `docs/templates/risk-assessment.md`)
but my job's output list does not mention it by name. The risk assessment is one of my core
deliverables (value says "owns security, privacy, deployment and run: the risk assessment"),
and the Architecture seat lists it as an input to Architect from Operator. I produce it, but
it is not formally listed in either my outputs or my inputs. See OPERATOR gap 4.

**Missing input 6 — `ops-readiness` feedback from Engineering Lead:** Engineering Lead
receives `ops-readiness from Operator` as an input. If Engineering Lead returns it with
findings (review), I have no named input for those findings. See OPERATOR gap 5.

---

### value

> "Owns security, privacy, deployment and run: the risk assessment, the branching and CI/CD
> approach with every gate wired and smoke-tested, operational readiness, and the release
> decision backed by the post-deploy check"

**KEEP with one structural concern.** Four responsibilities are bundled:
1. Risk assessment (security and privacy)
2. CI/CD approach and branching (gates wired and smoke-tested)
3. Operational readiness (observability, SLOs, rollback)
4. Release decision (backed by automated post-deploy check)

The value statement is clear and internally consistent. The concern: "the release decision
backed by the post-deploy check" refers to check E13, which is `planned` (not yet
implemented, per `docs/enforcement.yml`). Until E13 ships, the post-deploy check evidence
does not exist. I must note when I produce a release decision whether the check is
implemented or advisory. See OPERATOR gap 6.

---

### outputs

| # | Artifact | For | Decision |
|---|---|---|---|
| 1 | cicd | Builder | **KEEP** — Every gate is wired and smoke-tested (floor P3); Builder cannot start implementing without knowing the pipeline structure. Acceptance test is precise. |
| 2 | ops-readiness | Engineering Lead | **KEEP** — Covers observability, SLOs and rollback (floor P4). Engineering Lead approves before we can pass the plan gate. |
| 3 | release-decision | Intent Owner | **KEEP with concern** — Attaches automated post-deploy output (floor R2). This acceptance test requires E13 to be implemented; until then, the evidence is manual. See OPERATOR gap 6. |

**Missing output 4 — `risk-assessment` for Architect:** The Architect's inputs list
`{artifact: risk-assessment, from: Operator}`. My outputs do not include this artifact.
The value statement names it as something I own, but it is absent from my formal outputs.
A fresh Architect session waiting for a risk assessment will find no listed sender.
Proposed fix: add `{artifact: risk-assessment, for: Architect, acceptance: "Covers data
classification and main threats (floor C5)"}` to my outputs. See OPERATOR gap 4.

**Missing output 5 — `cicd` for Engineering Lead:** Engineering Lead's inputs list
`{artifact: cicd, from: Operator}`. My outputs list cicd for Builder only. Engineering
Lead also receives it (to approve the branching and CI/CD approach as a plan-gate artifact).
Proposed fix: add Engineering Lead as a second consumer of `cicd`. See OPERATOR gap 7.

**Missing output 6 — `cicd` for Steward:** Steward's inputs list `{artifact: cicd, from:
Operator}`. My outputs do not name Steward as a consumer. Proposed fix: same as gap 7 —
add Steward as a consumer. See OPERATOR gap 7.

---

### standards

`docs/dor/floor.yml`, `docs/enforcement.yml`

**KEEP.** Both are necessary and correctly chosen:
- `floor.yml` — DOR compliance for case/plan/release gates I must satisfy.
- `enforcement.yml` — I must know which checks are implemented versus advisory, since my
  outputs (especially cicd) directly rely on check status. This is the right standard for
  my seat and notably absent from Builder's standards (see Builder review for contrast).

**One gap:** `docs/artifact-types.yml` is absent. I produce cicd, ops-readiness and
release-decision, each of which has a named prefix, location and human-approver requirement.
Without artifact-types.yml in my standards, a fresh session may mis-file an artifact or
omit required front matter. Proposed fix: add `docs/artifact-types.yml` to my standards.
See OPERATOR gap 8.

---

### templates

`docs/templates/risk-assessment.md`, `docs/templates/cicd.md`,
`docs/templates/ops-readiness.md`, `docs/templates/release-decision.md`

**KEEP.** All four outputs have templates. This is the most complete template coverage of
any seat in the roster. No gaps.

**Note:** `risk-assessment.md` is listed as a template but the risk-assessment artifact is
absent from my outputs (see OPERATOR gap 4). The template implies I produce it; the outputs
section needs to catch up.

---

### verifier

Seat: Verifier. Evidence: "A review file beside each Operator artifact; the smoke-cycle
record in docs/archive; post-deploy check output once E13 ships"

**KEEP with two concerns.**

1. **"Post-deploy check output once E13 ships"** — this is explicitly conditional on a
   planned check. Until E13 ships, the verifier evidence for release decisions is
   incomplete. Verifier must note this caveat in each release review rather than refuse to
   verify. The conditional evidence weakens the gate.

2. **"Smoke-cycle record in docs/archive"** — this is a named evidence artifact location
   (`docs/archive`). I have not seen a template or naming convention for smoke-cycle
   records. A fresh Verifier session will not know what format or name to look for. See
   OPERATOR gap 9.

---

### qualified_layers

`[deployment-runtime, operations, integration]`

**KEEP.** These are the three layers I can author and challenge. I do not qualify for
`data`, `services-apis` or `frontend` — correct, those are Architect/Builder/Designer
domains. One note: `integration` appears in both my layers and Architect's layers
(`[data, services-apis, integration, frontend, deployment-runtime]`). Both seats qualify
for integration. For a specific integration architecture artifact, the D6 check will require
a qualified author and a different qualified challenger — we can serve as each other's
challenger on integration artifacts. This is correct wiring.

---

### What I cannot do as written

1. Produce a release decision with fully automated evidence before E13 is implemented — the
   acceptance test for output 3 requires it; until then, I can only declare manual evidence.
2. Respond to a security, privacy or run incident with a named artifact — my outputs do not
   include an incident-response artifact, so the procedure is undefined.
3. Know formally when to act on `increment verify evidence from Builder` — the trigger does
   not name this condition.
4. Send the risk assessment to Architect as a formally named output — it is missing from my
   outputs even though Architect lists it as an input from me.
5. Know from my standards what front-matter structure my artifacts require — `artifact-types.yml`
   is not in my standards list.

---

### What I would refuse to accept as input

1. An architecture or NFR artifact not in `approved` status — I produce a CI/CD approach
   based on the approved design; acting on a draft architecture embeds design decisions that
   may not stand.
2. A deployment request without an approved CI/CD approach — I would not authorize a
   deployment before the gate structure is smoke-tested (floor P3).
3. A release decision request without attached post-deploy check output (once E13 ships) —
   a release decision backed only by someone's judgment is not evidence.
4. Increment verify evidence that was produced from local test results rather than CI —
   the acceptance test requires CI output.
5. A request to declare gates smoke-tested without a smoke-cycle record in `docs/archive`
   (floor P3) — the gate canary check (E6, planned) will eventually enforce this; I will not
   self-certify without evidence.

---

## 2. The other seats

### Intent Owner

**Recommendation: Accept with conditions**

*What I hand to them:* `release-decision` (my output 3). Intent Owner receives it to decide
whether to ship (CLAUDE.md governance: approve the release or stop). My acceptance test
requires automated post-deploy output attached — until E13 ships, this evidence is manual.

*What I take from them:* Nothing directly. Intent Owner approves the cicd and ops-readiness
artifacts upstream (through Engineering Lead), but does not send me an artifact.

*Overlap:* None. Intent Owner judges business worth; I judge deployment readiness.

*Conditions:*
1. Release-decision format must be interpretable by a human seat holder — Intent Owner
   cannot be expected to parse raw CI JSON. My `release-decision` template should render
   health, version and smoke-test results in human-readable form.
2. Single-principal disclosure: the same person holds Intent Owner and Engineering Lead.
   My release-decision goes to Intent Owner; my ops-readiness goes to Engineering Lead.
   Both approvals come from one person. There is no independent challenge on the release
   path. This is the stated governance exception; I note it here.

*Wiring check:* Intent Owner's inputs list `{artifact: release-decision, from: Operator}` —
consistent with my output 3. Clean.

---

### Engineering Lead

**Recommendation: Accept with conditions**

*What I hand to them:* `ops-readiness` (my output 2) and `cicd` (my output 1 — but my
outputs only list Builder as the cicd consumer; see OPERATOR gap 7). Engineering Lead's
inputs list both `cicd from Operator` and a separate review of it.

*What I take from them:* Engineering Lead approves the architecture and test strategy
(through their respective authors' outputs), which I use as inputs 2 and 3. Engineering
Lead also approves my own outputs; if they return ops-readiness with a finding, I have no
named input for the review (see OPERATOR gap 5).

*Overlap:* None for artifacts. Engineering Lead governs soundness and governance; I govern
security, deployment and run.

*Conditions:*
1. Add Engineering Lead as a second consumer of `cicd` in my outputs (they receive it as a
   plan-gate artifact, per their inputs list).
2. Add `{artifact: review, from: Engineering Lead}` to my inputs (or clarify that the
   review artifact always comes through Verifier rather than directly).

*Wiring check:* Engineering Lead's inputs list `{artifact: cicd, from: Operator}` — my
outputs list cicd for Builder only; one-sided gap. Engineering Lead's inputs list
`{artifact: ops-readiness, from: Operator}` — consistent with my output 2. Partial
inconsistency.

---

### Product

**Recommendation: Accept**

*What I hand to them:* Nothing directly.

*What I take from them:* Nothing directly. Product's outputs flow to Architect and Delivery,
not to me.

*Overlap:* None. Product owns use cases and the validation verdict; I own deployment and
run. No functional overlap.

*Conditions:* None beyond confirming that by the time Product sends an increment-plan to
Delivery, the NFR artifacts I depend on are either approved or in-review (otherwise my
trigger cannot fire). This is a sequencing dependency, not a wiring gap.

*Wiring check:* Clean. No direct artifact exchange between Product and Operator.

---

### Delivery

**Recommendation: Accept**

*What I hand to them:* Nothing directly.

*What I take from them:* Nothing listed in my inputs, but Delivery cuts and orders stories
that contain the deployment tasks I may implement. The delivery system (naming track caps
and cadence) governs how I manage concurrent deployment tracks. Not a formal input gap;
the delivery system is background context, not a per-task input for my seat.

*Overlap:* None directly.

*Conditions:* None.

*Wiring check:* Clean. No direct artifact exchange between Delivery and Operator.

---

### Architect

**Recommendation: Accept with conditions**

*What I hand to them:* `risk-assessment` — but it is missing from my formal outputs. See
OPERATOR gap 4.

*What I take from them:* `nfr` (input 1) and `architecture` (input 2) — both correctly
listed.

*Overlap:* Both Operator and Architect qualify for the `integration` layer. We are each
other's natural challenger on integration artifacts. The `[Architect, Operator]` pair is
not in `incompatible_pairs`, which is fine — they are complementary, not competing, on this
layer. If the same holder were assigned both seats, integration-artifact challenge would
be invalid. In the minimum-crew holders, Agent B holds Architect and Agent A holds Operator,
so they are distinct. No conflict in the standard assignment.

*Conditions:*
1. Add `{artifact: risk-assessment, for: Architect, acceptance: "Covers data classification
   and main threats (floor C5)"}` to my outputs to close the formal wiring gap.
2. Architect's qualified_layers includes `deployment-runtime`, which I also hold. On
   deployment-runtime artifacts, either seat can author or challenge provided they are
   different holders.

*Wiring check:* Architect's inputs list `{artifact: risk-assessment, from: Operator}` —
my outputs do not name it; one-sided gap. I send `nfr` input to Architect's inputs — no,
wait: Architect's inputs list `nfr from Architect` (self-authored) and `risk-assessment
from Operator`. My inputs list `nfr from Architect` — I consume it, consistent. Architect
sends me nothing; I send them risk-assessment (gap in my outputs).

---

### Designer

**Recommendation: Accept**

*What I hand to them:* Nothing.

*What I take from them:* Nothing. Designer produces UX design and design systems for Builder,
not for Operator.

*Overlap:* None. Designer owns front-end experience; I own backend deployment and run.

*Conditions:* None.

*Wiring check:* Clean. No direct artifact exchange between Designer and Operator.

---

### Verifier

**Recommendation: Accept with conditions**

*What I hand to them:* `cicd` (Verifier's inputs list it, accepted). My outputs list cicd
for Builder only; Verifier also receives it. See OPERATOR gap 7.

*What I take from them:* `test-strategy` (my input 3). Verifier also produces a review
of my artifacts — the review file sits beside each artifact, and Verifier's verifier section
names me as a concern. I have no named input for review-findings from Verifier, though my
verifier evidence lists Verifier as the checker.

*Overlap:* `[Verifier, Operator]` is in `incompatible_pairs` — correct. The same session
cannot author the CI/CD approach and verify whether the gates were followed. This is the
right independence guard: if Operator designed a leaky gate, Verifier must catch it without
being the same session that designed it.

*Conditions:*
1. Add Verifier as a consumer of `cicd` in my outputs (Verifier's inputs list it).
2. The smoke-cycle record I must produce for Verifier to inspect has no named template or
   location convention (see OPERATOR gap 9).

*Wiring check:* Verifier's inputs list `{artifact: cicd, from: Operator}` — my outputs
list it for Builder only; one-sided gap. Verifier sends `test-strategy` to me — consistent
with my input 3.

---

### Builder

**Recommendation: Accept with conditions**

*What I hand to them:* `cicd` (my output 1). Builder uses it to understand the gate
structure and commit correctly.

*What I take from them:* `increment verify evidence` (my input 4). I use this to judge
deployment readiness.

*Overlap:* `[Builder, Operator]` is **not in `incompatible_pairs`**. In the minimum-crew
holders, both are Agent A. A single holder designs the pipeline gates and implements the
code that must pass them. This is a governance risk: the same session could lower a gate to
pass failing code. The Builder review (BUILDER gap 15) flags the same concern from the
Builder side.

*Conditions:*
1. Propose adding `[Builder, Operator]` to `incompatible_pairs` (I do not edit
   `docs/roles.yml`; I propose here). The concern is substantive: pipeline ownership and
   implementation ownership in the same session undermines gate integrity.
2. Verify that `increment verify evidence` is CI-sourced, not local, before I accept it
   as evidence for a release decision.

*Wiring check:* Builder's inputs list `{artifact: cicd, from: Operator}` — consistent with
my output 1. My inputs list `{artifact: increment verify evidence, from: Builder}` —
Builder's outputs list it for Verifier only; partial gap on Builder's side (not mine).

---

### Steward

**Recommendation: Accept**

*What I hand to them:* `cicd` (Steward's inputs list it). My outputs list cicd for Builder
only; Steward is a missing consumer. See OPERATOR gap 7.

*What I take from them:* Nothing directly.

*Overlap:* None. Steward audits process compliance; I own deployment and security.

*Conditions:*
1. Add Steward as a consumer of `cicd` in my outputs to match Steward's inputs.

*Wiring check:* Steward's inputs list `{artifact: cicd, from: Operator}` — my outputs list
it for Builder only; one-sided gap.

---

## 3. Help protocol

### What I offer each seat and when

| Seat | What I offer | When |
|---|---|---|
| Intent Owner | Release-decision with attached post-deploy evidence | After each deployment completes the post-deploy check |
| Engineering Lead | `ops-readiness` (plan gate); `cicd` (plan gate) for approval | When NFRs and architecture are approved and I have drafted both artifacts |
| Product | Nothing directly; my security and privacy assessments feed architecture, which informs use-case design indirectly | On Architect's request when risk assessment shapes design constraints |
| Delivery | Nothing directly | — |
| Architect | `risk-assessment` — data classification, main threats, and operational constraints that shape deployment and integration design | When NFRs are approved and I have assessed the threat model |
| Designer | Nothing directly | — |
| Verifier | `cicd` — the gate structure Verifier needs to write tests for the right levels and to verify my smoke-cycle record | When cicd is approved; updated on any gate change |
| Builder | `cicd` — so Builder knows the pipeline structure and commits correctly | When cicd is approved; before each increment starts |
| Steward | `cicd` for audit; smoke-cycle records in `docs/archive` | When cicd is approved; after each smoke cycle |

### What I ask of each seat, where I write the request, and how long I wait

| Seat | What I ask | Where I write the request | Wait limit | Escalate to |
|---|---|---|---|---|
| Architect | Approved `nfr` and `architecture` before I begin risk assessment and CI/CD design | Task manifest lists blocked artifacts; STATE.md open decisions if not resolved | One cycle | Steward (audit entry); open decision in STATE.md |
| Verifier | Approved `test-strategy` before I wire test-specific CI gates | Task manifest; STATE.md open decision if blocked | One cycle | Steward |
| Builder | `increment verify evidence` (CI-sourced) before I sign the release decision | Release-decision artifact front matter lists evidence artifact as a parent; if absent, I record a blocking open decision in STATE.md | Per release schedule | Engineering Lead via STATE.md open decision |
| Engineering Lead | Approval of `cicd` and `ops-readiness` to pass the plan gate | Artifact status in front matter; STATE.md if blocked | Not formally defined; sole human seat holder — no escalation authority beyond STATE.md | STATE.md open decision; note governance limitation |

---

## 4. Authority

### What I decide alone

- The risk level of a threat and whether it requires a control — within the bounds of
  floor C5 (main threats; data classification)
- Whether a CI gate is correctly wired and smoke-tested before declaring P3 met
- Whether post-deploy check output satisfies the release-decision evidence requirement
  (once E13 ships)
- Whether `increment verify evidence` from Builder is CI-sourced (I reject local results)
- The smoke-cycle schedule: when to run it and which worktrees to cover
- Whether a security or privacy finding rises to the level of blocking a deployment

### What I decide only after consulting

| Decision | Consult | Reason |
|---|---|---|
| A threat that requires an architectural control (e.g., a data boundary change) | Architect | The control may require a design change the Architect must author; I identify the threat, Architect designs the response |
| Declaring a gate smoke-tested when the canary check (E6) is still planned | Engineering Lead | The advisory status means my self-certification replaces a planned hard check; Engineering Lead must be aware |
| Lowering an SLO target in the ops-readiness artifact | Engineering Lead | SLO changes affect release quality thresholds; this is a soundness decision the Engineering Lead must approve |
| Authorizing a deployment when post-deploy check evidence is manual (E13 not yet implemented) | Intent Owner | The release-decision acceptance test requires automated evidence; if I must substitute manual evidence, the exception needs the Intent Owner's explicit acknowledgment |

### When I ask before acting

- Before producing a release decision: confirm that deployment-environment health, build
  version match, and seeded smoke-test results are attached as evidence
- Before wiring a gate that relies on a planned check (e.g., E5, E6, E13): disclose its
  advisory status in the cicd artifact front matter so consumers know the check is not yet
  enforced
- Before accepting increment verify evidence as a deployment input: confirm it comes from
  the CI run for the specific build being released, not a prior run or a local execution
- Before declaring ops-readiness: confirm that monitoring is live, SLOs are measurable in
  the target environment, and rollback has been rehearsed (not just documented)

### What I would refuse

- A deployment without an approved CI/CD approach and smoke-tested gates
- A release decision without the required post-deploy check output (or without explicit
  Engineering Lead acknowledgment that E13 is not yet implemented)
- A CI/CD approach that allows agents to push to main — CLAUDE.md Governance prohibits it
- Any request to amend or delete a merged migration — the append-only rule (E15) is
  enforced; I redirect to Architect for the correct new-migration procedure
- Self-certifying gate smoke-tests without a smoke-cycle record in `docs/archive`
- Acting on an incident response with no defined output artifact — until an incident-response
  artifact type is defined, I cannot produce evidence that satisfies E10

### Where the procedure left me less room than my job description implies

1. **Release-decision evidence depends on a planned check.** My acceptance test for output
   3 requires automated post-deploy output (E13), which is not yet implemented. I can
   produce a release decision, but I cannot satisfy my own acceptance test. I must note
   this in every release decision until E13 ships.

2. **Incident response has no output artifact.** My trigger names "a security, privacy or
   run incident" as a condition, but my outputs list no incident-response artifact. A fresh
   session receiving an incident will not know what to produce or where to file it. The
   procedure leaves me with no path to a verifiable output.

3. **Smoke-cycle record has no template or naming convention.** My verifier evidence says
   "the smoke-cycle record in docs/archive." Without a template, each session will produce
   a different format, and Verifier cannot reliably find or evaluate it.

4. **No formal escalation when Engineering Lead is unavailable.** Both human seats are one
   person. If that person is unavailable, my release-decision cannot be approved, and my
   cicd and ops-readiness artifacts cannot pass their gates. No escalation authority is
   defined at this governance stage.

5. **`risk-assessment` is in my value statement and templates but not my outputs.** The
   procedure implies I own it; the formal output list does not say I do. A fresh Operator
   session reading only my job description could overlook producing it.

---

## 5. Guessing log

Every point where the procedure left me without a clear answer.
OPERATOR = a gap in my own job description or the wiring to/from it.
METHOD = a gap in the process design visible from my seat.
PRODUCT = a gap in the product itself (unfilled template slots, missing definitions).

| Label | Description |
|---|---|
| OPERATOR gap 1 | **Trigger ordering is ambiguous.** The trigger lists three conditions independently but does not state that CI/CD must be complete before a deployment is authorized. A session could read "a deployment is due" as firing independently of CI/CD readiness. Proposed fix: rewrite trigger as two phases — (a) "NFRs and architecture are approved: produce risk assessment, CI/CD and ops-readiness"; (b) "CI/CD is approved and increment verify evidence received: authorize deployment and produce release decision." |
| OPERATOR gap 2 | **Incident response has no output artifact.** The trigger fires on "a security, privacy or run incident" but no output covers it. A fresh session responding to an incident has no named artifact to produce, no template, and no evidence standard. Proposed fix: add an incident-response artifact type (`docs/artifact-types.yml`), a template, and an output entry for Operator. |
| OPERATOR gap 3 | **`increment verify evidence from Builder` is an input but its receipt condition is not in the trigger.** A fresh session will not know that receiving this input is a condition that should initiate the release-decision process. Proposed fix: add "increment verify evidence is received from Builder" as an explicit trigger condition for the release-decision output. |
| OPERATOR gap 4 | **`risk-assessment` is absent from my outputs.** The value statement and templates both name it as mine to produce. Architect's inputs list it as coming from Operator. The formal output list is silent. Proposed fix: add `{artifact: risk-assessment, for: Architect, acceptance: "Covers data classification and main threats (floor C5)"}` to my outputs. |
| OPERATOR gap 5 | **No input for Engineering Lead's findings on my artifacts.** When Engineering Lead returns `ops-readiness` with a review finding, I have no named input channel. Proposed fix: add `{artifact: review, from: Engineering Lead}` to my inputs, or clarify that Verifier mediates all findings. |
| OPERATOR gap 6 | **Release-decision acceptance test requires E13 (planned check).** Until E13 ships, the evidence requirement is unenforceable. Every release decision I produce before E13 ships will fail its own acceptance test. Proposed fix: add a transitional acceptance test — "until E13 ships, attach a signed manual post-deploy check record; once E13 ships, automated output replaces it." |
| OPERATOR gap 7 | **`cicd` output is listed for Builder only; Engineering Lead, Verifier and Steward also receive it.** Three seats list `cicd from Operator` as an input (Engineering Lead, Verifier, Steward). My outputs name only Builder. Proposed fix: add Engineering Lead, Verifier and Steward as additional consumers of `cicd`. |
| OPERATOR gap 8 | **`docs/artifact-types.yml` absent from my standards.** My three outputs have artifact-type definitions (prefix, directory, human-approver). Without artifact-types.yml in my standards, a fresh session may mis-file or omit required front matter. Proposed fix: add `docs/artifact-types.yml` to my standards. |
| OPERATOR gap 9 | **Smoke-cycle record has no template or naming convention.** Verifier evidence requires it; Verifier cannot evaluate what it cannot find. Proposed fix: define a `smoke-cycle-record.md` template in `docs/templates/`, add a naming convention (e.g., `SMK-{NNN}-{cycle}-{date}.md` in `docs/archive/`), and add `docs/templates/smoke-cycle-record.md` to my templates. |
| METHOD gap 1 | **No escalation path when the sole human seat holder is unavailable.** Both human seats (Intent Owner, Engineering Lead) are one person. If that person is unavailable, my outputs (cicd, ops-readiness, release-decision) cannot be approved, and no gate can pass. STATE.md records the open decision, but no escalation authority is defined. This is the stated governance exception at cycle 1; it becomes a risk in production. |
| METHOD gap 2 | **`[Builder, Operator]` not in `incompatible_pairs`.** In the minimum-crew holders, both seats are Agent A. The same session designs the CI/CD gates and implements the code that must pass them. This creates a conflict: the session can lower a gate to pass failing code. Proposed fix: add `[Builder, Operator]` to `incompatible_pairs`. (Noted identically in BUILDER gap 15 from the Builder review.) |
| METHOD gap 3 | **Incident response is triggered but has no process.** "A security, privacy or run incident opens" fires my trigger, but no artifact type, template, output or escalation path exists for it. A session responding to a production incident will improvise. Proposed fix: define an incident-response workflow, artifact type and template as a crew review item, since no existing seat covers it end-to-end. |
| PRODUCT gap 1 | **Task delivered via conversation prompt, not input manifest.** Per CLAUDE.md §3, decisions count only once written to a named artifact. This review is the first durable artifact produced by this session. The divergence is acceptable for a dryrun bootstrap task; in production, the task manifest would be the authoritative input. |
| PRODUCT gap 2 | **Bootstrap has not run.** CLAUDE.md contains unfilled `{{double braces}}` slots: mission, principles and seat holder names. STATE.md product description is empty. The project's trade-off principles and the actual holder identities are unknown. I am operating without context that bootstrap is designed to supply. My risk assessment, when I produce it, will lack a project-specific threat model until bootstrap completes. |
