# DRYRUN-JOBREVIEW — Builder

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
   named artifact in the repository." I treat the prompt as advisory. This divergence is
   noted here.

### Notes about the person (from session context)

- Email: imran.canuck@gmail.com (used for authorship and attribution only)
- Git user: PublicEnemage
- Holds: Intent Owner seat and Engineering Lead seat (listed as "Human 1" in
  `docs/roles.yml`; the name substitution that bootstrap performs has not happened yet)
- Single-principal disclosure applies (CLAUDE.md Governance): one person holds both human
  seats; no independent review is available at this stage

---

## 1. My own job (Builder seat)

Source: `docs/roles.yml` lines 160–179. I review each field and say keep or change.

### trigger

> "An increment intent is approved and its tests are red in CI; a task with an input
> manifest is pulled"

**KEEP with notes.** Two conditions must hold simultaneously: (a) the increment intent is
approved, and (b) the tests are red in CI — the red state shows the tests were written
first before my implementation. The second clause enforces the test-first rule (CLAUDE.md
advisory E2).

**Note 1:** "A task with an input manifest is pulled" is a second trigger form, not a
condition. It is broader and supersedes the first — if a task manifest is handed to me, I
start regardless of whether the preceding clauses are verified. The manifest must therefore
encode those preconditions. A fresh session cannot verify them independently. See BUILDER
gap 1.

**Note 2:** The trigger does not name who sends the task manifest or how the increment
intent reaches me. No formal dispatch mechanism is described beyond the manifest. A session
starting cold without a manifest has no polling target. See BUILDER gap 1.

**Note 3:** What if the tests are not red in CI? The trigger says "and its tests are red
in CI," which implies I must refuse to start if the tests are green (no tests written) or
absent (tests not yet committed). No explicit refusal procedure is stated. See BUILDER
gap 2.

---

### inputs

| # | Artifact | From | Decision |
|---|---|---|---|
| 1 | increment-intent | Product | **KEEP** — the increment intent scopes the use cases I must implement and names the approved stories I pull from. Without it, I cannot know what to build. |
| 2 | architecture | Architect | **KEEP** — I implement to the approved architecture; each layer section must be buildable from without asking questions (the consumer duty). |
| 3 | test-strategy | Verifier | **KEEP** — I write unit tests for my own code using the test strategy's standards. I do not author acceptance tests, but the test strategy tells me the test types and the CI gate structure. |
| 4 | cicd | Operator | **KEEP** — I commit to a pipeline built to the CI/CD approach; knowing the gate structure determines how I commit, tag and flag tests. |

**Missing input 5 — `ux-design` from Designer:** For increments that include a user
interface, I implement to the UX design and design system. Designer's outputs list both
`ux-design` and `design system` for Builder (acceptance: "Components and tokens a builder
can use without choosing styles itself"). My inputs do not list them. A fresh session
implementing UI will either guess styles or seek the artifact without knowing to expect it.
See BUILDER gap 3.

**Missing input 6 — `nfr` from Architect:** My implementation must meet the NFRs (floor
targets). The architecture references them, but the NFR artifact itself is not listed as a
named input. If the architecture section is silent on a particular NFR target (e.g.,
response-time budget per endpoint), I have no primary source to consult. Architect sends
NFR to Verifier (who writes tests for it), but not explicitly to me. See BUILDER gap 4.

**Missing input 7 — review response from Verifier:** After I commit implementation,
Verifier may return findings. My job does not list `review from Verifier` as an input. A
fresh session receiving a Verifier review on a prior increment has no named input to pull
the review from. See BUILDER gap 5.

---

### value

> "Implements to the approved architecture under the CI/CD approach, and writes the unit
> tests for its own code. Never writes the acceptance tests for its own work, and never
> introduces a dependency or pattern without an ADR"

**KEEP with one structural concern.** Three prohibitions are stated:
1. Never writes acceptance tests for its own work — acceptance tests belong to Verifier.
2. Never introduces a dependency without an ADR.
3. Never introduces a pattern without an ADR.

The second and third are strong: every new dependency and every new cross-cutting pattern
needs an ADR. The Verifier's evidence for me lists "an ADR for every new dependency (floor
I3)." But the value statement adds "or pattern," while floor I3 names only dependency. If
a session adds a new architectural pattern without a dependency (e.g., adopts a coding
convention, introduces a new error-handling strategy), it is unclear whether the ADR
requirement applies. The value statement says yes; the floor citation says only dependency.
See BUILDER gap 6.

**Note:** The value statement does not say whether I can challenge the architecture or the
test strategy if I discover a problem while implementing. The consumer duty (CLAUDE.md)
says "if it must ask what the artifact should have said, the artifact goes back." This
implies I report the gap as a challenge finding, but my job does not state this explicitly.
See METHOD gap 1.

---

### outputs

| # | Artifact | For | Decision |
|---|---|---|---|
| 1 | implementation and implementation design | Verifier | **KEEP** — Verifier challenges my implementation and the design decisions embedded in it. The acceptance test ("Committed acceptance tests pass in CI, and a fresh reader explains the behaviour, failures included, to match the intent (floor I5)") is clear. |
| 2 | increment verify evidence | Verifier | **KEEP** — Verifier uses this to produce verification evidence for Product. The acceptance test ("Test results come from CI; no new skip without an expiry entry (floor I6)") is clear. |

**Missing output 3 — `increment verify evidence` for Product:** Product's inputs list
`{artifact: increment verify evidence, from: Builder}`. My outputs only name Verifier as
the consumer. Product receives it directly (as named in Product's inputs), but it is not
listed in my outputs as a second consumer. Whether Product receives this artifact from me
directly or only through Verifier is ambiguous. See BUILDER gap 7.

**Missing output 4 — `increment verify evidence` for Operator:** Operator's inputs list
`{artifact: increment verify evidence, from: Builder}`. Same issue — not in my outputs.
See BUILDER gap 7.

**Note on output 1:** "Committed acceptance tests pass in CI" — the acceptance tests are
committed by Verifier before I implement (per the red-before-green rule, CLAUDE.md advisory
E2). I commit the implementation that turns those tests green. The phrasing "committed
acceptance tests" may mislead a fresh session into thinking I commit the acceptance tests
myself, which contradicts the "never writes the acceptance tests for its own work" rule.
See BUILDER gap 8.

---

### standards

`docs/dor/floor.yml`, `docs/standards/data/README.md`

**KEEP with one gap.** Both are necessary — floor.yml for DOR compliance, data/README.md
for data layer standards (relevant when I implement data-layer code). However:

`docs/enforcement.yml` is absent. When I implement a feature, I need to know which checks
are hard gates (enforced by a tool) and which are advisory. Without enforcement.yml, I may
spend effort satisfying an advisory check while missing that a hard check blocks my PR.
More critically, my ADR and skip-expiry obligations are enforced by checks E3 and E15
(from the Verifier's evidence items); I cannot know their enforcement status without
enforcement.yml. See BUILDER gap 9.

---

### templates

`docs/templates/adr.md`, `docs/templates/story.md`

**KEEP with one gap.** ADR template is correct — every new dependency or pattern needs one.
Story template is unexpected: I am a consumer of stories, not an author. The story template
in my job suggests I may write stories (perhaps task breakdowns within an increment). If I
am an author of stories, I need a verifier, and no story-review step appears in any seat's
job description. See BUILDER gap 10.

**Missing template — `implementation-design`:** Output 1 includes "implementation design,"
but no template exists for it. A fresh session making structural choices during
implementation (e.g., how to decompose a service, which pattern to adopt within the
architecture's boundaries) has no canonical form for recording those decisions beyond ADRs.
See BUILDER gap 11.

---

### verifier

Seat: Verifier. Evidence: "Tests seen red then green in CI per test; no early-return or
blanket skip (E3); merged migrations unedited (E15); an ADR for every new dependency (floor
I3)"

**KEEP with two concerns.**

1. **Evidence items tie to advisory rules.** E3 and E15 are listed as check identifiers.
   `docs/enforcement.yml` shows their enforcement status. If E3 and E15 are not yet shipped,
   the evidence items are aspirational. Verifier must know the difference before raising a
   finding versus noting an advisory gap.

2. **"An ADR for every new dependency (floor I3)" covers dependency but not pattern** (see
   BUILDER gap 6 above). If I add a new pattern without a dependency, the evidence item
   does not catch it. The value statement's broader ADR requirement is not matched by the
   verifier's evidence.

---

### qualified_layers

`[data, services-apis, frontend, integration]`

**KEEP.** These are the four layers I can build and challenge (floor D6). I do not qualify
for `deployment-runtime` and `operations` — correct, those are Operator's domain. No
concern.

---

### What I cannot do as written

1. Start an increment if the acceptance tests are absent from CI — but my job has no stated
   procedure for this refusal: no escalation path, no artifact to file. I must infer the
   action from CLAUDE.md advisory E2 (still advisory, not enforced).
2. Choose styles for a user interface without the UX design and design system — those
   artifacts are not in my inputs.
3. Verify what target an NFR sets (e.g., response time budget) without the NFR artifact —
   it is not in my inputs.
4. Respond to a Verifier review without a named input for it — my inputs do not list
   `review from Verifier`.
5. Know from my templates what form an "implementation design" should take — no template
   exists.
6. Determine whether a new pattern (without a new dependency) requires an ADR — the value
   statement says yes, but the floor citation and verifier evidence say only dependency.
7. Know from my standards alone which checks are currently enforced and which are advisory
   — enforcement.yml is not in my standards list.

---

### What I would refuse to accept as input

1. A task with no input manifest — floor I7 requires every task to carry its own input
   manifest; I will not act on a task described only in conversation.
2. An increment intent that is not in `approved` status — I implement only approved work.
3. An increment where the acceptance tests are not yet committed and red in CI — the
   red-before-green rule (CLAUDE.md advisory E2) is my precondition; absent confirmed red
   tests, I would note the gap and wait for Verifier to commit them first.
4. A request to write acceptance tests for my own increment — "never writes the acceptance
   tests for its own work."
5. A request to introduce a dependency or pattern without filing an ADR — this is a named
   prohibition in my value statement.
6. An architecture or test strategy whose consumer duty is not met (I must ask what it
   should have said) — the artifact must go back to its author, not prompt me to improvise.
7. Increment verify evidence that I am asked to produce using local test results rather than
   CI output — the acceptance test for output 2 requires CI results.

---

## 2. The other seats

### Intent Owner

**Recommendation: Accept with conditions**

*What I hand to them:* Nothing directly. My increment verify evidence goes to Verifier and
Product; Product turns it into a validation verdict, which Intent Owner receives.

*What I take from them:* Nothing directly.

*Overlap:* None. Intent Owner judges business worth; I judge implementation correctness.

*Conditions:*
1. Single-principal disclosure: Intent Owner and Engineering Lead are one person. Both
   artifacts that gate my work (architecture from Architect, approved by Engineering Lead;
   test strategy from Verifier, approved by Engineering Lead) must be approved by the same
   person. If that person is unavailable, I cannot start. See METHOD gap 2.

*Wiring check:* Clean. No artifacts cross directly between us.

---

### Engineering Lead

**Recommendation: Accept with conditions**

*What I hand to them:* Nothing formally named in Engineering Lead's inputs or my outputs.
Indirectly, my merged implementations are what Engineering Lead governs via merge history
and CI checks (their verifier evidence).

*What I take from them:* The approved architecture (via Architect) and approved test
strategy (via Verifier) — Engineering Lead approves both before they reach me, but the
approval hop is invisible in my inputs.

*Overlap:* None for artifacts. Engineering Lead approves soundness; I implement.

*Conditions:*
1. My inputs list `architecture from Architect` and `test-strategy from Verifier`. Both
   must carry Engineering Lead's approval before they reach me (see output acceptance tests
   for Engineering Lead: "Builder can implement from them without asking what they should
   have said"). The approval status is checked by the SEATS/E10 mechanism, but my job does
   not state that I verify approval status before starting — I should verify.
2. Engineering Lead never pushes to main (CLAUDE.md Governance). This means every merge
   of my branch goes through a PR opened by me (an agent) and approved by Engineering
   Lead (the human approver). The PR approval step is not listed in my outputs or in
   Engineering Lead's inputs as a named artifact. It lives implicitly in the governance
   section. See BUILDER gap 12.

*Wiring check:* Engineering Lead's outputs list "approved architecture, test strategy and
CI/CD approach for Builder" — consistent with my inputs 2, 3, 4. Clean.

---

### Product

**Recommendation: Accept with conditions**

*What I hand to them:* `increment verify evidence` (Product's inputs list it, though my
outputs name only Verifier as consumer — see BUILDER gap 7). Indirectly, my implementation
passes or fails use-case scenarios that Product uses when writing the validation verdict.

*What I take from them:* `increment-intent` (my input 1) — the approved stories and
use-case scope for this increment.

*Overlap:* `[Builder, Product]` is in `incompatible_pairs` — correct. The same session
cannot author the use cases and implement them; this prevents implementation from
diverging from stated requirements while maintaining plausible deniability.

*Conditions:*
1. Product's inputs list `{artifact: increment verify evidence, from: Builder}`. My outputs
   name only Verifier as the consumer of this artifact. If Product receives it directly
   from my branch rather than through Verifier's synthesis, the naming implies two distinct
   artifacts — Builder's raw CI output and Verifier's verdict — are being conflated in
   Product's inputs. This should be clarified. See BUILDER gap 7.
2. Product's `qualified_layers: []` means Product holds no layer qualification, yet it
   consumes my implementation artifacts indirectly and passes judgment (validation verdict)
   on them. Product's judgment is business-functional, not technical; but for use cases
   with technically-defined pass criteria (e.g., response time under threshold), Product
   may not be equipped to judge. See METHOD gap 3.

*Wiring check:* Product's inputs list `increment verify evidence from Builder` — my
outputs list it only for Verifier; partial inconsistency. Product sends increment-intent
to me — I list it as input 1; consistent.

---

### Delivery

**Recommendation: Accept with conditions**

*What I hand to them:* Nothing directly.

*What I take from them:* Nothing listed in my inputs, but Delivery cuts and orders the
stories that my increment-intent is drawn from.

*Overlap:* `[Builder, Delivery]` is **not in `incompatible_pairs`**. In the minimum-crew
holders, Builder is Agent C and Delivery is Agent A. A single holder could hold both seats.
Builder implementing code and Delivery setting the delivery process are non-competitive
concerns on the surface, but if Builder also holds Delivery, it controls its own task
prioritization. This is a mild governance risk: Builder could deprioritize review-blocking
tasks. See BUILDER gap 13.

*Conditions:*
1. Delivery's output `delivery-system` (naming hierarchy, story template, prioritization
   rule, cadence, track cap and metrics) is not listed in my inputs. However, this
   document governs how my work is organized (what hierarchy stories live in, how I pull
   tasks). I need to know the delivery system to pull tasks correctly, but it is not
   named as a formal input. See BUILDER gap 14.

*Wiring check:* Delivery does not name Builder as a consumer of any artifact; Builder does
not name Delivery as a source. No crossing wires, but the implicit dependency (I build
from stories that Delivery cuts) is unrepresented.

---

### Architect

**Recommendation: Accept with conditions**

*What I hand to them:* Nothing formally. My implementation may trigger a review of the
architecture if the consumer duty is not met (I discover a gap). But this is an informal
escalation path, not a named artifact.

*What I take from them:* `architecture` (my input 2), and implicitly `nfr` (missing from
my inputs — see BUILDER gap 4). Architect's outputs list `architecture for Builder`
(acceptance: "Each layer section can be built from without asking what it should have
said"). The consumer duty is clearly stated.

*Overlap:* `[Builder, Architect]` is in `incompatible_pairs` — correct. The same session
cannot design the architecture and implement against it; this prevents the implementation
from quietly redefining the design.

*Conditions:*
1. Architect sends `nfr` to Verifier (acceptance test names "a test type can be named for
   it"). The NFR targets are what I must meet at runtime. If the architecture references
   NFR targets inline, I can read them there; if they are only in a separate NFR artifact,
   I may miss them. Proposed: add `{artifact: nfr, from: Architect}` to my inputs.
2. Architect's qualified layers are `[data, services-apis, integration, frontend,
   deployment-runtime]`. My qualified layers are `[data, services-apis, frontend,
   integration]`. I can challenge the architecture on four of the five layers but not on
   `deployment-runtime`. If an architecture section for that layer contains an
   implementable error, I can raise it informally (consumer duty) but may not be able to
   formally challenge it under D6.

*Wiring check:* Architect's outputs list `architecture for Builder` — I list it as
input 2; consistent. Architect's outputs list `nfr for Verifier` — no corresponding input
on my side; partial gap.

---

### Designer

**Recommendation: Accept with conditions**

*What I hand to them:* Nothing.

*What I take from them:* `ux-design` and `design system` (Designer's outputs for Builder)
— but these are absent from my inputs list. See BUILDER gap 3.

*Overlap:* `[Builder, Designer]` is in `incompatible_pairs` — correct. The same session
cannot design the UX and implement it; this prevents implementation from quietly overriding
design decisions.

*Conditions:*
1. Add `{artifact: ux-design, from: Designer, acceptance: "Every use case maps to a flow;
   I can implement without choosing states or transitions myself"}` and `{artifact: design
   system, from: Designer, acceptance: "Components and tokens are sufficient for me to
   implement UI without choosing styles"}` to my inputs.
2. Designer's trigger fires only "if the product has a user interface." My inputs should
   mark both Designer artifacts as conditional (applies only to increments with a UI).

*Wiring check:* Designer's outputs list both artifacts for Builder — neither appears in my
inputs. One-sided.

---

### Verifier

**Recommendation: Accept with conditions**

*What I hand to them:* `implementation and implementation design` (output 1),
`increment verify evidence` (output 2).

*What I take from them:* `test-strategy` (my input 3), and implicitly `review` (findings
on my implementation — not in my inputs).

*Overlap:* `[Builder, Verifier]` is in `incompatible_pairs` — the most critical
separation in the project. The same session cannot implement and verify; this is the
core independence guard.

*Conditions:*
1. Add `{artifact: review, from: Verifier}` to my inputs. Verifier's verifier section
   says "tests seen red then green in CI per test; no early-return or blanket skip (E3);
   merged migrations unedited (E15); an ADR for every new dependency." When Verifier raises
   findings on my work, I need a named input for the review to action them.
2. The test-strategy comes from Verifier but must carry Engineering Lead's approval before
   I act on it. My input 3 does not note the approval hop; I should verify the status.
3. Verifier's outputs do not list `review for Builder` (a gap noted in the Verifier job
   review). My inputs similarly don't list it. Both sides have the same gap.

*Wiring check:* Verifier's inputs list `increment verify evidence from Builder` —
consistent with my output 2. Verifier's outputs list `test-strategy for Builder` —
consistent with my input 3. Verifier's outputs do not list `review for Builder` — my
inputs do not list `review from Verifier`; both sides gap consistently. The gap is
symmetric — real but not a wiring conflict.

---

### Operator

**Recommendation: Accept with conditions**

*What I hand to them:* `increment verify evidence` — Operator's inputs list it. My outputs
name only Verifier as consumer; this is a gap (see BUILDER gap 7).

*What I take from them:* `cicd` (my input 4).

*Overlap:* `[Builder, Operator]` is **not in `incompatible_pairs`**. In the minimum-crew
holders, Builder is Agent C and Operator is Agent A. A single holder could hold both seats.
If the same session designs the CI/CD pipeline and implements the code that must pass it,
it controls the gates and the code simultaneously. This is a governance risk: Builder-as-
Operator could lower a gate to pass failing code. See BUILDER gap 15.

*Conditions:*
1. Add `[Builder, Operator]` to `incompatible_pairs` as a proposed change (I do not edit
   `docs/roles.yml`; I propose here).
2. Operator's outputs list `cicd for Builder` — consistent with my input 4.
3. My outputs should add `increment verify evidence for Operator` to close the wiring gap.

*Wiring check:* Operator sends `cicd` to me — consistent. I send `increment verify
evidence` to Operator (per Operator's inputs) — my outputs don't list Operator as a
consumer; one-sided gap.

---

### Steward

**Recommendation: Accept**

*What I hand to them:* An audit trail — ADRs for every new dependency, no blanket skips,
unedited migrations. These are not artifacts I hand to Steward; they are evidence Steward
reads from the repository.

*What I take from them:* Nothing directly.

*Overlap:* None. Steward holds no artifact seat; it audits the process trail.

*Note:* Steward audits whether the process was followed. My Verifier (Verifier seat) checks
my artifacts' content. Steward can confirm that an ADR exists; it cannot judge whether the
ADR is sound. That is Architect's concern, which is served by Architect's challenge review
of my ADRs when they affect the architecture.

*Wiring check:* Clean. Steward reads the repository; no direct artifact exchange needed.

---

## 3. Help protocol

### What I offer each seat and when

| Seat | What I offer | When |
|---|---|---|
| Intent Owner | Nothing directly; my evidence feeds Product's verdict which Intent Owner receives | After each validation cycle |
| Engineering Lead | A merged PR with all gates green; ADRs for new dependencies on the PR | After each increment; on any new dependency or pattern |
| Product | Increment verify evidence (raw CI output showing which tests pass or fail) | After each increment is built and tested in CI |
| Delivery | Task pull signal (I pull a task and it moves to in-progress) | When I start work on a story |
| Architect | Consumer feedback if an architecture section cannot be built from without asking questions | During implementation; I raise a formal finding rather than improvise |
| Designer | Consumer feedback if a UX design or design system component is missing or ambiguous for implementation | During implementation; I raise a formal finding |
| Verifier | Implementation and implementation design committed on my branch; increment verify evidence | When I consider an increment ready for verification |
| Operator | Increment verify evidence (per Operator's inputs) | After each increment |
| Steward | A process-compliant audit trail: ADRs filed, no blanket skips, migrations unedited | Continuously, through every commit |

### What I ask of each seat, where I write the request, and how long I wait

| Seat | What I ask | Where I write the request | Wait limit | Escalate to |
|---|---|---|---|---|
| Architect | Approved architecture (including data layer if Data Architect seat is not adopted) before I can start | Task manifest lists blocked artifact; STATE.md open decisions if not resolved | One cycle | Steward (audit entry); open decision in STATE.md |
| Verifier | Approved test strategy before I write unit tests; red acceptance tests in CI before I write implementation | Task manifest; STATE.md open decision if blocked | Per increment schedule | Steward |
| Operator | Approved CI/CD approach before I commit | Task manifest; STATE.md open decision if blocked | One cycle | Steward |
| Designer | Approved UX design and design system before I implement any UI | Task manifest; STATE.md open decision if blocked | One cycle | Steward |
| Engineering Lead | Approved architecture and test strategy (through their respective authors' outputs) | Artifact status check (both must be `approved` before I pull); STATE.md if blocked | Not formally defined; sole human seat holder | STATE.md open decision; no further escalation authority defined (see METHOD gap 2) |

---

## 4. Authority

### What I decide alone

- Which unit tests to write for my own code (within the test strategy's framework and
  test types)
- Whether to file an ADR for a new dependency or pattern — the rule is: I must; the
  judgment call is what constitutes "new"
- How to structure my implementation within the approved architecture — choices that fall
  below the layer-level decisions that needed an ADR
- Whether a CI run's exit counts represent my increment verify evidence (CI output is
  authoritative, not my local run)
- Whether an architecture section or test strategy meets the consumer duty — if it does
  not, I return it rather than guess what it should have said
- Whether the acceptance tests are red in CI before I start writing implementation (my
  precondition check)

### What I decide only after consulting

| Decision | Consult | Reason |
|---|---|---|
| Introducing a new cross-cutting pattern (not a dependency) | Architect | The pattern may need an ADR; Architect decides whether it fits within the approved architecture or constitutes a design change |
| Deciding that an architecture section is insufficient to build from | Architect | The consumer duty obligates me to return the artifact; I confirm the gap with Architect before formally filing a finding so the artifact author understands the cause |
| Deciding to skip a test (with expiry entry) | Verifier | A skip affects verification evidence; Verifier's evidence items check skip expiry (floor I6); I consult before marking any test skipped |
| Deciding that a migration needs amending | Operator | Migrations must be append-only (E15); if I believe a migration has an error, I do not amend it; I consult Operator on the correct procedure (a new migration) |

### When I ask before acting

- Before starting any increment: confirm that acceptance tests are committed and red in CI
  (I will not implement speculatively)
- Before introducing a new dependency: check whether an ADR already covers the dependency;
  if not, file one before the commit that introduces the dependency
- Before producing increment verify evidence: confirm that test results come from the CI
  run, not a local execution
- Before submitting a PR: confirm no open Verifier finding on the current increment is
  unaddressed (I do not seek final approval — that is Verifier's role — but I do not
  submit work I know to have open findings)

### What I would refuse

- Writing acceptance tests for my own increment — "never writes the acceptance tests for
  its own work"
- Introducing a dependency or cross-cutting pattern without an ADR
- Amending a merged migration — instead, a new migration must be filed
- Producing increment verify evidence from local test results rather than CI output
- Merging to main — agents open PRs, Engineering Lead merges
- Pushing to main — CLAUDE.md Governance is explicit; agents work on branches
- Acting on a task with no input manifest

### Where the procedure left me less room than my job description implies

1. **No explicit refusal procedure when acceptance tests are absent.** My trigger
   requires tests to be red in CI before I start. If a session receives a task manifest
   for an increment with no tests committed, my job does not state what I do. I infer
   from advisory E2 that I should decline and wait, but the procedure is not written.

2. **No stated procedure for returning an insufficient architecture.** The consumer duty
   (CLAUDE.md) says the artifact "goes back" if I must ask what it should have said. But
   my job description does not name a procedure (which artifact to file, who to notify,
   where to record the gap). I infer from the review template, but it is not linked.

3. **ADR requirement for "patterns" is stated in value but not in verifier evidence.**
   I am bound by both (value: "never introduces a pattern without an ADR"; verifier
   evidence: "an ADR for every new dependency"). The floor citation (I3) covers only
   dependency. A session could satisfy the verifier evidence without satisfying the value
   statement's broader rule. The scope of the ADR requirement is ambiguous.

4. **Story template in my templates list implies I author stories.** If I author stories,
   I need a challenger; no story-review path exists in any seat's job. I cannot tell from
   my job description whether the story template is for reading or writing.

5. **Increment verify evidence has no template.** My second output is critical (it feeds
   Verifier and Product), but no template defines its structure. Each session will produce
   a different format, making CI reproducibility harder to confirm.

6. **No procedure for disagreeing with a Verifier finding.** If Verifier raises a finding
   I believe is wrong, my job does not describe a formal dispute path. The five-role chain
   says the author responds item by item to findings; I am the author of the implementation.
   The dispute escalates through the review artifact's answered-findings mechanism, but this
   is not stated in my job description.

---

## 5. Guessing log

Every point where the procedure left me without a clear answer.
BUILDER = a gap in my own job description or the wiring to/from it.
METHOD = a gap in the process design visible from my seat.
PRODUCT = a gap in the product itself (unfilled template slots, missing definitions).

| Label | Description |
|---|---|
| BUILDER gap 1 | **No formal trigger dispatch mechanism.** My trigger says "a task with an input manifest is pulled." No document describes who creates that manifest, how it is formatted, or where it lives in the repository. A fresh Builder session starting without a manifest cannot verify the preconditions (approved increment intent, tests red in CI) independently. Proposed fix: define a task manifest template and name the seat responsible for creating it (Delivery is the most natural choice). |
| BUILDER gap 2 | **No stated refusal procedure when acceptance tests are absent from CI.** My trigger requires tests to be red in CI. If they are not (tests not yet committed), my job does not name the action. Proposed fix: add "If tests are not red in CI, Builder notifies Verifier and records a blocked task in STATE.md; implementation does not begin." |
| BUILDER gap 3 | **`ux-design` and `design system` missing from my inputs.** Designer's outputs for Builder are not listed in my inputs. A session implementing a UI feature has no named input to pull from. Proposed fix: add `{artifact: ux-design, from: Designer}` and `{artifact: design system, from: Designer}` to my inputs, marked as conditional (UI increments only). |
| BUILDER gap 4 | **`nfr` from Architect missing from my inputs.** I must implement to the NFR targets (floor rows C4, D5). The NFR artifact is sent from Architect to Verifier only; I have no formal receive for it. If the architecture does not embed the NFR targets inline, I cannot verify compliance. Proposed fix: add `{artifact: nfr, from: Architect}` to my inputs. |
| BUILDER gap 5 | **`review from Verifier` missing from my inputs.** When Verifier reviews my implementation, I must respond item by item. My inputs do not list this artifact. Proposed fix: add `{artifact: review, from: Verifier, acceptance: "I respond to each finding with a named artifact response"}` to my inputs. |
| BUILDER gap 6 | **ADR requirement scope differs between value statement and verifier evidence.** Value says "never introduces a dependency or pattern without an ADR." Verifier evidence cites floor I3 for "every new dependency." The floor citation covers only dependency. A session could pass the Verifier's evidence check while introducing an undocumented pattern. Proposed fix: update floor I3 to include "or new cross-cutting pattern," or add a separate floor row for patterns, and update the Verifier's evidence accordingly. |
| BUILDER gap 7 | **`increment verify evidence` is named as going to Verifier only in my outputs, but Operator and Product both list it as an input from Builder.** Either (a) I send it to three consumers and my outputs are incomplete, or (b) Operator and Product receive it through Verifier's synthesis (and their input entries should say `from: Verifier`). The naming is ambiguous. Proposed fix: clarify which route is intended; update outputs or the receiving seats' inputs accordingly. |
| BUILDER gap 8 | **Output 1 acceptance test ("committed acceptance tests pass in CI") may be read as requiring me to commit acceptance tests.** My value statement says I never write acceptance tests for my own work. The acceptance test on output 1 should say "acceptance tests committed by Verifier pass in CI" to remove ambiguity. |
| BUILDER gap 9 | **`docs/enforcement.yml` missing from my standards.** I need to distinguish enforced checks (hard gates) from advisory rules. Without it, I may treat an advisory as a hard failure or vice versa. Proposed fix: add `docs/enforcement.yml` to my standards. |
| BUILDER gap 10 | **Story template in my templates implies I author stories, but no story-review path exists.** If I use the story template to author stories, I need a challenger and an approver. No seat has a job description that includes "challenge story authored by Builder." Proposed fix: clarify whether the story template in my templates list is for reading (consuming stories) or writing (authoring breakdowns); if writing, add a challenge path. |
| BUILDER gap 11 | **No template for `implementation design`.** Output 1 includes "implementation design" as part of what I send to Verifier. No template defines its form. A fresh session making architectural choices within an increment has only the ADR template for cross-cutting decisions; finer-grained design decisions have no standard form. Proposed fix: define an implementation-design template or clarify that implementation design is conveyed through ADRs and code structure alone. |
| BUILDER gap 12 | **PR approval as an artifact step is invisible in my outputs and Engineering Lead's inputs.** I open a PR; Engineering Lead approves and merges it. This is the main governance gate for my work, but it does not appear as a named artifact in any job description. The PR is the de facto approval artifact. Proposed fix: consider adding `{artifact: pull-request, for: Engineering Lead, acceptance: "All gates green; ADRs filed for new dependencies; no blanket skips"}` to my outputs, or document it in a PR template. |
| BUILDER gap 13 | **`[Builder, Delivery]` not in `incompatible_pairs`.** Builder could control its own task prioritization if the same holder holds both seats. Proposed fix: consider adding `[Builder, Delivery]` to `incompatible_pairs` if self-prioritization is a governance concern; accept the risk if the minimum crew's small size makes it impractical. |
| BUILDER gap 14 | **`delivery-system` from Delivery not in my inputs.** The delivery system defines how stories are organized and how I pull tasks. I need to know it to use the task hierarchy correctly. Proposed fix: add `{artifact: delivery-system, from: Delivery}` to my inputs as a reference input (consumed once at cycle start, not per increment). |
| BUILDER gap 15 | **`[Builder, Operator]` not in `incompatible_pairs`.** Builder implementing code and Operator designing the gates that code must pass is a conflict: the same holder could lower a gate to pass failing code. Proposed fix: add `[Builder, Operator]` to `incompatible_pairs`. |
| METHOD gap 1 | **No formal procedure for Builder to report that an architecture section fails the consumer duty.** When I cannot build from an architecture section without asking what it should have said, the artifact "goes back" (CLAUDE.md). But no step in my job names the artifact to file, the seat to notify, or where to record the gap. I must infer from the review template. |
| METHOD gap 2 | **No escalation path when the sole human seat holder is unavailable.** Both human seats (Intent Owner, Engineering Lead) are one person. If that person is unavailable, approved artifacts cannot reach me, and my PRs cannot be merged. STATE.md records the open decision, but no escalation authority exists at this governance stage. |
| METHOD gap 3 | **Product's `qualified_layers: []` may limit its ability to judge validation verdicts for technically-defined use cases.** For a use case with an NFR-based pass criterion (e.g., latency under threshold), Product must judge whether my verify evidence satisfies it. With no layer qualification, Product relies entirely on Verifier's synthesis. The validation-verdict artifact's acceptance test says "states accept or reject per use case in scope" — it does not require layer expertise. The risk is subtle, not a wiring gap. |
| PRODUCT gap 1 | **Bootstrap has not run.** CLAUDE.md contains unfilled `{{double braces}}` slots: mission, principles, and seat holder names. The State.md product description field is empty. This means my qualified domain, the project's principles for trade-off decisions, and the actual holder identities are all unknown. I am operating without the context that bootstrap is designed to supply. |
