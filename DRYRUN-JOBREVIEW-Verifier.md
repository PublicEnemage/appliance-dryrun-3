# DRYRUN-JOBREVIEW — Verifier

## Context visible to this session

### Project instruction files in context

1. **CLAUDE.md** (the Constitution, `/CLAUDE.md`) — mission and principles slots are
   unfilled template placeholders (`{{double braces}}`); bootstrap has not run. Core rules
   in effect: session protocol (read CLAUDE.md + STATE.md + input manifest only; work on
   own branch; no `git stash`; commit before ending; treat conversation as disposable);
   the five-role artifact chain (Consulted → Author → Challenger → Approver → Consumer);
   governance (agents branch and PR only, never push to main); single-principal
   disclosure (Intent Owner and Engineering Lead are one person, no independent review at
   this stage).

2. **STATE.md** (`/STATE.md`) — cycle 1, setup phase. `active_tracks: []`. No open
   decisions. No mid-task work. Product description field is empty (bootstrap has not run).

3. **No task input manifest in the repository.** This session received its task via
   conversation prompt. Per CLAUDE.md §3: "A decision counts only once it is written to a
   named artifact in the repository." I proceed from the files and treat the prompt as
   advisory. This divergence is noted here.

### Notes about the person (from session context)

- Email: imran.canuck@gmail.com (used for authorship and attribution only)
- Git user: PublicEnemage
- Holds: Intent Owner seat and Engineering Lead seat (listed as "Human 1" in
  `docs/roles.yml`; the name substitution that bootstrap performs has not happened yet)
- Single-principal disclosure applies (CLAUDE.md Governance): one person holds both
  human seats; no independent review is available at this stage

---

## 1. My own job (Verifier seat)

Source: `docs/roles.yml` lines 138–159. I review each field and say keep or change.

### trigger

> "An artifact enters review; tests for an increment are committed; an increment is ready
> for validation"

**KEEP with notes.** Three distinct trigger events are correct:

1. Artifact enters review → I challenge it and issue a review file.
2. Tests for an increment are committed → I inspect the tests before implementation starts
   (the red-before-green rule, CLAUDE.md advisory E2).
3. An increment is ready for validation → I produce verification evidence.

**Note 1:** "An artifact enters review" is underspecified. It does not say which seat or
which artifact type triggers me. The notification mechanism is implicit: any seat sets an
artifact's status to `in-review`, and that signals me. No formal dispatch artifact or
status-change hook is described. A session starting fresh has no polling target — it must
be handed a task manifest that names the in-review artifact. See VERIFIER gap 1.

**Note 2:** The three trigger events correspond to three distinct roles (challenger,
test-pre-checker, validation producer), but nothing in my job description separates them
into distinct output pathways. A session that activates on trigger 3 must know not to
produce trigger 1's review format. The one job description covers three operating modes
without labelling them. See VERIFIER gap 2.

---

### inputs

| # | Artifact | From | Decision |
|---|---|---|---|
| 1 | any artifact in review | Product | **CHANGE** — the `from: Product` attribution is wrong. I challenge artifacts from Product, Architect, Designer, Builder, and Operator — every authoring seat. Labelling the catch-all input as `from: Product` means a fresh session reading the manifest would expect only Product artifacts. Proposed: replace with `from: any authoring seat`, or list each source separately. |
| 2 | architecture | Architect | **KEEP** — I need the architecture to write the test strategy (knowing the system's layers, failure modes, and NFR targets). However, this input serves my authoring role, not my reviewing role. The architecture is also covered by input 1's catch-all when it enters review. The dual-purpose is not stated. |
| 3 | cicd | Operator | **KEEP** — I need the CI/CD approach to write the test strategy (knowing what test types the pipeline supports) and to judge whether verification evidence is reproducible from CI. |
| 4 | increment verify evidence | Builder | **KEEP** — correct for trigger 3 (validation). |

**Missing input 5 — `nfr` from Architect:** My test-strategy output must name a test type
for each NFR (floor D5). I cannot do this without receiving the NFR artifact. NFR is not
listed as an input. When I activate to write the test strategy, I have architecture and
cicd but no NFR. A fresh session cannot complete the test strategy from the listed inputs
alone. See VERIFIER gap 3.

**Missing input 6 — `users-use-cases` or `increment-intent` from Product:** My
test-strategy must name an acceptance approach for each use case in scope (floor D5).
Use cases reach me only indirectly through input 1's catch-all when they enter review. I
need the approved use-case artifact before I can author the test strategy, but it is not
listed as a named input. See VERIFIER gap 4.

**Missing input 7 — review responses from authors:** When I issue a review with findings,
the artifact author must respond item by item. My re-review of the answered findings
closes the loop. This second-pass trigger and its artifact are absent from my inputs. A
fresh session handed the initial review task has no description of the reply loop. See
VERIFIER gap 5.

---

### value

> "Finds what is wrong, missing or inconsistent, as a fresh session, and states whether
> the work does what the artifacts say. Authors the test strategy and the standards the
> tests rely on, and never verifies its own work"

**KEEP with one structural concern.** The phrase "never verifies its own work" is the
critical guard. But I *author* the test strategy and the standards — both of which are
my own artifacts. Who challenges the test strategy before Engineering Lead approves it?
No seat is chartered to review the test-strategy as challenger. Engineering Lead approves
it; Steward audits the process trail; neither is chartered as the content challenger of
my output. The value statement's guard is correct in intent but is not enforced for my
own artifacts. See VERIFIER gap 6.

---

### outputs

| # | Artifact | For | Decision |
|---|---|---|---|
| 1 | review | Product | **KEEP** — consistent with Product's inputs (`review from Verifier`). |
| 2 | review | Architect | **KEEP** — consistent with Architect's inputs (`review from Verifier`). |
| 3 | test-strategy | Builder | **CHANGE** — I send test-strategy to three consumers, not one. Engineering Lead's inputs list `test-strategy from Verifier` (they approve it); Operator's inputs list `test-strategy from Verifier` (they wire gates to it). Builder is the correct implementation consumer, but the output entry should also list Engineering Lead (for approval) and Operator. The approval path through Engineering Lead is invisible in my current outputs. See VERIFIER gap 7. |
| 4 | verification evidence | Product | **CHANGE** — Product's inputs do not list `verification evidence from Verifier` as a named input; they list `increment verify evidence from Builder`. My output goes to Product so Product can author the validation-verdict, but the receiving entry in Product's job is missing or mislabelled. See VERIFIER gap 8. |

**Missing output 5 — `review` for Designer:** Designer's verifier is Verifier (evidence:
"A review file beside each UX artifact"). I challenge Designer's ux-design, but my outputs
do not list `review for Designer`. The return path is absent. See VERIFIER gap 9.

**Missing output 6 — `review` for Builder:** I review Builder's implementation and
increment verify evidence. Builder's verifier is Verifier (evidence: "Tests seen red then
green in CI per test; no early-return or blanket skip; merged migrations unedited; an ADR
for every new dependency"). But my outputs do not list `review for Builder`. See VERIFIER
gap 10.

**Missing output 7 — `review` for Operator:** Operator's verifier is Verifier (evidence:
"A review file beside each Operator artifact; the smoke-cycle record in docs/archive").
My outputs do not list `review for Operator`. See VERIFIER gap 11.

**Missing output 8 — `test-strategy` for Operator:** Operator's inputs list
`test-strategy from Verifier`. My outputs list it only for Builder. See VERIFIER gap 7
(mirror).

**Missing output 9 — `test-strategy` for Engineering Lead:** Engineering Lead's inputs
list `test-strategy from Verifier`. Not in my outputs. See VERIFIER gap 7 (mirror).

---

### standards

`docs/dor/floor.yml`, `docs/standards/data/README.md`

**KEEP with one gap.** Both are necessary. However, `docs/enforcement.yml` is absent.
When I raise a review finding, I need to distinguish between enforced checks (a tool will
catch it) and advisory checks (only my judgment catches it). Without enforcement.yml as a
named standard, a fresh session reviewing an artifact may raise findings that are already
enforced or skip findings that are not. See VERIFIER gap 12.

---

### templates

`docs/templates/review.md`, `docs/templates/test-strategy.md`, `docs/templates/standard.md`

**KEEP with one gap.** My fourth output is `verification evidence`, but no template exists
for it. The verification evidence must be reproducible from CI and use exit counts from CI,
not a summary (CLAUDE.md advisory E8). Without a template, each session producing
verification evidence will structure it differently, making it harder to compare across
increments and easier for a session to omit mandatory fields. See VERIFIER gap 13.

---

### verifier

Seat: Steward. Evidence: "A review file beside each approved artifact, answered item by
item (E10); no session authored and challenged the same artifact (SEATS)"

**KEEP with a structural concern.** Steward audits *process* compliance: were the right
steps taken, are findings answered, did the same session avoid self-review? Steward does
not audit the *content* of my reviews or my test strategy. If my review is wrong (I mark
a valid artifact as failing) or my test strategy omits an NFR, Steward's evidence items
do not catch it. There is no content challenger for my artifacts. Engineering Lead approves
the test strategy for soundness, which partially fills this gap for that one artifact, but
the content of my review files has no challenge step. See VERIFIER gap 6 (mirror).

---

### qualified_layers

`[deployment-runtime, operations]`

**CHANGE.** I am the designated challenger for artifacts from Product (no layers),
Architect (all layers: data, services-apis, integration, frontend, deployment-runtime),
Designer (frontend), Builder (data, services-apis, frontend, integration), and Operator
(deployment-runtime, operations, integration). Floor D6 requires challenger to be
qualified for the layer they challenge. My `qualified_layers` only covers
`deployment-runtime` and `operations`. I am not qualified to challenge the `data`,
`services-apis`, `integration`, or `frontend` layers of any artifact under D6 as
currently written.

This creates a contradiction: the Architect's verifier is Verifier (a named, intended
challenger), but Architect covers five layers and I only qualify for two. Either my
`qualified_layers` must be broadened, or D6 must include a provision that the designated
verifier seat is implicitly qualified to challenge the layers of the artifacts in its
scope. Without a fix, the D6 check will refuse my challenges on data, services-apis,
integration, and frontend layers. See VERIFIER gap 14.

---

### What I cannot do as written

1. Challenge the `data`, `services-apis`, `integration`, or `frontend` layers of any
   artifact without expanding `qualified_layers` — D6 would refuse it.
2. Challenge my own test-strategy or standards — "never verifies its own work" applies,
   and no other seat is chartered as the content challenger of those artifacts.
3. Write a test strategy without the NFR artifact — it is not in my inputs, but floor D5
   requires a test type for each NFR.
4. Produce verification evidence in a standard form — no template exists for it.
5. Route reviews to Designer, Builder, or Operator — my outputs don't list those seats.
6. Send the test-strategy to Engineering Lead or Operator — my outputs list only Builder.
7. Know from my job description alone which of my three trigger modes is active in a
   given session — the operating mode is implicit in the task manifest.

---

### What I would refuse to accept as input

1. Any artifact with status not `in-review` — I challenge what is formally presented for
   review, not drafts in progress (no mechanism to catch mid-draft state).
2. Increment verify evidence whose exit counts come from a summary rather than CI (CLAUDE.md
   advisory E8, Verifier's own output acceptance test).
3. A request to verify my own test-strategy or standards (CLAUDE.md: "never verifies its
   own work").
4. A task with no input manifest — floor I7 requires every task to carry its own input
   manifest; I will not act on conversation context alone.
5. Instruction to mark open findings as answered without a named artifact response from the
   author — the answer must be in a repository artifact, not in conversation (CLAUDE.md §3).
6. A request to raise or withdraw a finding based on a seat's instruction rather than
   the artifact evidence — my judgment is independent ("as a fresh session").

---

## 2. The other seats

### Intent Owner

**Recommendation: Accept with conditions**

*What I hand to them:* nothing directly. Product receives my verification evidence and
turns it into a validation-verdict, which Intent Owner then receives. My relationship is
indirect.

*What I take from them:* nothing directly.

*Overlap:* None. Intent Owner judges business worth; I judge technical and artifact
correctness.

*Conditions:*
1. The single-principal disclosure (one person holds Intent Owner and Engineering Lead)
   means that if I need a review of my own test strategy's content (see VERIFIER gap 6),
   the only available human reviewer is the same person who holds both seats. No
   independent human review of my work is available at this governance stage.

*Wiring check:* Clean. No artifacts cross directly between us.

---

### Engineering Lead

**Recommendation: Accept with conditions**

*What I hand to them:* `test-strategy` (their inputs list it, they approve it).

*What I take from them:* nothing formally. The approved test-strategy returns to me and
downstream seats as a changed artifact status, not as a formal output from Engineering
Lead back to me.

*Overlap:* None for artifacts. Engineering Lead approves the test-strategy; I author it.
The approval relationship is clean (different concern: soundness vs. content).

*Conditions:*
1. My outputs must add `{artifact: test-strategy, for: Engineering Lead, acceptance:
   "Names a test type for each NFR and an acceptance approach for each use case (floor
   D5); Engineering Lead approves before Builder receives it"}`. Without this, a fresh
   Engineering Lead session has no formal receive path from me.

*Wiring check:* Engineering Lead inputs list `test-strategy from Verifier` — consistent
with the intended flow. My outputs list `test-strategy for Builder` only. One-sided.

---

### Product

**Recommendation: Accept with conditions**

*What I hand to them:* `review` (output 1) and `verification evidence` (output 4).

*What I take from them:* "any artifact in review" (my input 1, mislabelled as
`from: Product`). Product is one of the authoring seats whose artifacts I challenge
(users-use-cases, business-case, increment-plan, validation-verdict).

*Overlap:* `[Verifier, Product]` is in `incompatible_pairs` — correct. The same session
cannot hold both seats. This prevents a session from reviewing its own use cases.

*Conditions:*
1. Product's inputs list `review from Verifier` — consistent. But Product's inputs do not
   list `verification evidence from Verifier` as a named input. Product uses my evidence
   to author the validation-verdict, but the receive entry is missing or collapsed into
   the `increment verify evidence from Builder` entry. See VERIFIER gap 8.
2. Product's inputs list `increment verify evidence from Builder` — that is Builder's
   raw output. My `verification evidence` is a synthesised judgment on top of that
   evidence. The two are different artifacts serving different purposes. They should be
   named separately in Product's inputs.

*Wiring check:* I send review to Product; Product's inputs list `review from Verifier` —
consistent. I send verification evidence to Product; Product's inputs do not list it —
inconsistent.

---

### Delivery

**Recommendation: Accept**

*What I hand to them:* nothing directly.

*What I take from them:* nothing directly.

*Overlap:* None. Delivery owns process and cadence; I own artifact and increment
correctness.

*Wiring check:* Clean. No artifacts cross between us.

*Note:* If Delivery cuts an increment that includes a use case before my test strategy
is approved, Builder may start implementing without knowing which acceptance tests to
write. No coordination gate in Delivery's job prevents this. See METHOD gap 1.

---

### Architect

**Recommendation: Accept with conditions**

*What I hand to them:* `review` (output 2) — findings on each Architect artifact.

*What I take from them:* `architecture` (my input 2), and implicitly `nfr` (missing from
my inputs — see VERIFIER gap 3).

*Overlap:* `[Verifier, Architect]` is in `incompatible_pairs` — correct.

*Conditions:*
1. Architect's outputs include `nfr for Verifier` (acceptance: "Each NFR has a target or
   a signed not-applicable, so a test type can be named for it"). I need NFR as a named
   input to write the test strategy, but it is not listed in my inputs. I must add
   `{artifact: nfr, from: Architect}` to my inputs.
2. My `qualified_layers` do not cover the full range of layers Architect documents. D6
   will refuse my challenge of the data, services-apis, integration, or frontend layer
   sections until `qualified_layers` is expanded. See VERIFIER gap 14.

*Wiring check:* Architect's inputs list `review from Verifier` — consistent with my
output 2. Architect's outputs list `nfr for Verifier` — no corresponding input on my
side. Inconsistent.

---

### Designer

**Recommendation: Accept with conditions**

*What I hand to them:* `review` — findings on each ux-design artifact.

*What I take from them:* `ux-design` (in-review), covered by input 1's catch-all.

*Overlap:* `[Designer, Verifier]` is **not in `incompatible_pairs`**. In the minimum-crew
holders, Designer is Agent B and Verifier is Agent D — separated in practice, but not
by a structural rule. A single holder could hold both seats and challenge their own UX
artifacts without the SEATS check refusing it. This is the same gap Designer gap 8
identified from the other side. See VERIFIER gap 15.

*Conditions:*
1. Add `{artifact: review, for: Designer, acceptance: "Each finding has a severity, and
   open_findings counts what is unanswered"}` to my outputs. The return path is absent.
2. Add `[Designer, Verifier]` to `incompatible_pairs` in `docs/roles.yml`. (Proposed here;
   I do not edit that file.)

*Wiring check:* Designer's verifier is Verifier (per `docs/roles.yml` lines 135–137),
but my outputs list no review for Designer. One-sided.

---

### Builder

**Recommendation: Accept with conditions**

*What I hand to them:* `test-strategy` (after Engineering Lead approves it); `review`
of their implementation and increment verify evidence.

*What I take from them:* `increment verify evidence` (my input 4).

*Overlap:* `[Builder, Verifier]` is in `incompatible_pairs` — correct. The same session
that implements the code cannot verify it.

*Conditions:*
1. My outputs do not list `review for Builder`. Builder's verifier is Verifier (evidence:
   "Tests seen red then green in CI per test; no early-return or blanket skip; merged
   migrations unedited; an ADR for every new dependency"). I review Builder's artifacts
   and produce findings, but the routing is absent. Add `{artifact: review, for: Builder,
   acceptance: "Each finding has a severity, and open_findings counts what is unanswered"}`
   to my outputs. See VERIFIER gap 10.
2. Builder's inputs list `test-strategy from Verifier` — consistent with my output 3,
   but output 3 does not note the Engineering Lead approval hop that happens first.

*Wiring check:* Builder's inputs list `test-strategy from Verifier` — consistent. Builder
lists no input for `review from Verifier` — inconsistent, since Builder's verifier is me
and I produce review findings on their work.

---

### Operator

**Recommendation: Accept with conditions**

*What I hand to them:* `review` (not listed in my outputs) and `test-strategy` (listed
in Operator's inputs but not in my outputs).

*What I take from them:* `cicd` (my input 3).

*Overlap:* `[Verifier, Operator]` is in `incompatible_pairs` — correct. The same session
cannot own the CI/CD approach and independently verify whether it is correctly wired.

*Conditions:*
1. Operator's inputs list `test-strategy from Verifier` and `increment verify evidence
   from Builder`. Neither `test-strategy` nor `review` appear in my outputs as going to
   Operator. Both must be added. See VERIFIER gap 7 and gap 11.
2. Operator's verifier is Verifier (evidence: "A review file beside each Operator artifact;
   the smoke-cycle record in docs/archive; post-deploy check output once E13 ships"). My
   outputs must list `review for Operator` to close this wiring.

*Wiring check:* Operator's inputs list `test-strategy from Verifier` — no corresponding
output on my side. Operator's inputs list `cicd` going *to* me — consistent with my
input 3. Operator's verifier is me — no review output on my side to Operator. Two
inconsistencies.

---

### Steward

**Recommendation: Accept with conditions**

*What I hand to them:* clean audit trail — review files beside each artifact, answered
item by item (E10); no session self-reviewing. My outputs don't list Steward as a
consumer, but Steward receives the review artifacts indirectly by auditing the repository.

*What I take from them:* Steward is my verifier. They inspect whether my review files
exist, are answered, and whether the SEATS check confirms no self-review occurred. This
is process compliance verification, not content review.

*Overlap:* None. Steward holds no artifact seat. It cannot be my content challenger.

*Conditions:*
1. Steward's verifier for me (the Steward's evidence items) covers process compliance but
   not content quality. If my review findings are wrong or my test strategy is incomplete,
   Steward's evidence items do not catch it. This is a structural gap, not a wiring gap
   — the current design simply has no seat designated to challenge the content of my work
   (only Engineering Lead approves the test strategy). See VERIFIER gap 6.

*Wiring check:* Steward's inputs include `review from Verifier` — Steward receives my
review artifacts for audit. My outputs list `review for Product` and `review for Architect`
but not `for Steward` — Steward reads what I put in the repository, so a separate named
output may not be needed. But the audit trail depends on my review files being correctly
placed and formatted; I should confirm this is covered by the review template. Acceptable.

---

## 3. Help protocol

### What I offer each seat and when

| Seat | What I offer | When |
|---|---|---|
| Intent Owner | Nothing directly; my verification evidence feeds Product's validation-verdict which Intent Owner receives | After each validation cycle |
| Engineering Lead | test-strategy set to in-review for approval | Once architecture, NFR, and CI/CD approach are all approved and I have authored the test strategy |
| Product | review (findings with severity, open_findings count) on each Product artifact; verification evidence after increment validation | When a Product artifact enters in-review; when an increment passes validation |
| Delivery | Nothing directly | — |
| Architect | review (findings with severity, open_findings count) on each Architect artifact | When an Architect artifact enters in-review |
| Designer | review on each ux-design artifact | When a Designer artifact enters in-review |
| Builder | Approved test-strategy (after Engineering Lead approval); review of implementation and verify evidence | Before Builder starts implementing (test strategy); after Builder submits verify evidence (review) |
| Operator | review on each Operator artifact; test-strategy (after Engineering Lead approval) | When an Operator artifact enters in-review; after test-strategy is approved |
| Steward | Process-compliant review files: correct format, all findings answered, no self-review | Continuously |

### What I ask of each seat, where I write the request, and how long I wait

| Seat | What I ask | Where I write the request | Wait limit | Escalate to |
|---|---|---|---|---|
| Architect | Approved architecture and NFR artifacts before I can write the test strategy | Task manifest for my session (lists blocked artifact path); note in STATE.md open decisions if blocked | One cycle | Steward (audit entry); open decision in STATE.md |
| Operator | Approved CI/CD approach before I can write the test strategy | Task manifest; STATE.md open decisions note if blocked | One cycle | Steward |
| Engineering Lead | Approval of test-strategy in-review | Artifact set to `in-review`; STATE.md note if blocked | Not formally defined — Engineering Lead and Intent Owner are one person; no independent escalation path | Note in STATE.md as open decision; no further escalation authority defined (see METHOD gap 2) |
| Builder | Increment verify evidence when an increment is ready for validation | Task manifest for my validation session; STATE.md note if blocked | Per increment cadence | Steward |
| Product | Approved users-use-cases (for test strategy acceptance approaches) | Task manifest; STATE.md note | One cycle | Steward |

---

## 4. Authority

### What I decide alone

- Whether a finding is valid, based solely on the artifact evidence and the floor,
  standards, and templates in effect — no seat may instruct me to withdraw a finding
  without a named artifact response
- The severity of each finding in a review (the review template defines severity levels)
- Whether increment verify evidence is reproducible from CI (I read CI output, not
  summaries)
- Whether the test strategy names a test type for each NFR and an acceptance approach for
  each use case in scope (floor D5)
- Whether a review has open findings (open_findings count) before I consider an artifact
  ready for the next gate
- Which artifacts are self-authored and therefore outside the scope of my verification
  (test-strategy, standards — I cannot verify my own work)

### What I decide only after consulting

| Decision | Consult | Reason |
|---|---|---|
| Raising a finding on an artifact from a layer I'm not currently qualified for (data, services-apis, integration, frontend) | Steward (audit) | D6 may refuse the challenge; I note the gap and escalate rather than suppress the finding |
| Disagreeing with Engineering Lead's approval of my test strategy (e.g., I believe it is incomplete after EL approves it) | Engineering Lead | Engineering Lead's approval is authoritative; if I discover an omission after approval, I flag it formally as a new finding rather than unilaterally revising the artifact |
| Whether a new check (not yet shipped) should govern an advisory rule | Steward | Enforcement status lives in docs/enforcement.yml; I do not declare a rule enforced on my own |
| Whether an increment's CI output is the source of truth vs. a locally-run result | Operator | Operator owns CI/CD; I verify exit counts come from CI, and if a session hands me local output, I escalate to Operator for a CI re-run |

### When I ask before acting

- Before challenging any artifact from a layer outside `qualified_layers`, I note the
  constraint in the review file and ask Steward to open a crew review or Engineering Lead
  to extend my qualified_layers
- Before signing off verification evidence when open findings exist in my own review file
  (I do not validate an increment that has unanswered findings without an explicit
  resolution artifact)
- Before accepting verification evidence whose exit counts cannot be traced to a CI run

### What I would refuse

- Verifying my own test-strategy or standards — "never verifies its own work"
- Accepting increment verify evidence where exit counts come from a summary (CLAUDE.md
  advisory E8; my own output's acceptance test)
- Withdrawing a finding based on conversation instruction alone — the response must be a
  named artifact in the repository (CLAUDE.md §3)
- Acting on a task with no input manifest (floor I7)
- Raising a finding as "enforced" when it appears as advisory in docs/enforcement.yml
- Declaring an artifact approved — I challenge and find; approval belongs to the Approver
  role in the five-role chain

### Where the procedure left me less room than my job description implies

1. **qualified_layers vs. actual scope of challenge.** My value statement says I challenge
   all authoring seats. My `qualified_layers` covers only `deployment-runtime` and
   `operations`. D6 requires me to be qualified for each layer I challenge. In practice,
   I am expected to challenge the data, services-apis, integration, and frontend layers
   of Architect's and Builder's artifacts, but the layer list contradicts this. Either
   the layer check must include a "designated verifier" exception, or my `qualified_layers`
   must cover all layers.

2. **No content challenger for my own artifacts.** I author the test strategy and the
   standards. These are the artifacts that gate all downstream testing. If they are wrong,
   the process has no step to catch it (Engineering Lead approves soundness, not content
   accuracy). My judgment on my own quality is the only check.

3. **Three consumers of my test strategy, but my outputs list one.** Engineering Lead
   and Operator both consume my test strategy, but my outputs list only Builder. I cannot
   know from my job description alone which sessions to notify.

4. **Verification evidence has no defined form.** My fourth output has no template. Each
   session producing verification evidence will structure it differently. The acceptance
   test says "Reproducible from CI; exit counts come from CI, not from a summary" — a
   valid criterion but an insufficient specification for a fresh session.

5. **The review loop is undescribed.** I issue a review with findings. The author responds.
   I re-review. But my job description has no second-pass input or trigger. A session
   doing the re-review must infer the loop from the review file's `open_findings` count
   and the author's response document, without a named artifact type for the response.

---

## 5. Guessing log

Every point where the procedure left me without a clear answer.
VERIFIER = a gap in my own job description or the wiring to/from it.
METHOD = a gap in the process design visible from my seat.

| Label | Description |
|---|---|
| VERIFIER gap 1 | **No formal notification artifact for "artifact enters review."** My trigger fires when any artifact enters in-review, but no dispatch artifact or hook is described. A fresh session must be handed a task manifest naming the in-review artifact. Without a formal mechanism, sessions may start late or be skipped. Proposed fix: define a status-change convention (e.g., a Delivery task record) that routes the in-review artifact path to a Verifier session's task manifest. |
| VERIFIER gap 2 | **Three trigger modes in one job description with no mode selector.** Trigger events 1 (challenge), 2 (test pre-check), and 3 (validation) correspond to different outputs and different session scopes. A fresh session's task manifest must name the mode explicitly; otherwise the session risks producing the wrong output type. Proposed fix: label the three modes in the job description and state which inputs and outputs apply to each. |
| VERIFIER gap 3 | **`nfr` from Architect is missing from my inputs.** Floor D5 requires the test strategy to name a test type for each NFR. I cannot satisfy D5 without receiving the NFR artifact. Proposed fix: add `{artifact: nfr, from: Architect}` to my inputs. |
| VERIFIER gap 4 | **`users-use-cases` or `increment-intent` missing from my inputs.** Floor D5 also requires an acceptance approach for each use case in scope. A fresh session writing the test strategy needs the approved use-case list as a named input. Proposed fix: add `{artifact: users-use-cases, from: Product}` to my inputs (the approved version, as a precondition). |
| VERIFIER gap 5 | **Review reply loop has no artifact-level description.** When I issue a review, the author responds item by item. My re-review of the answered findings is a second pass. No artifact type for the author's reply exists, and my inputs list no second-pass trigger. Proposed fix: define a review-response artifact type (or a convention in the review template) and add a second-pass input to my job. |
| VERIFIER gap 6 | **No content challenger for my own artifacts (test-strategy, standards).** I author the test strategy and the standards. "Never verifies its own work" protects against self-verification, but no seat is chartered to challenge the content of my test strategy before Engineering Lead approves it. Steward checks process; Engineering Lead checks soundness; neither checks accuracy against the NFRs and use cases. Proposed fix: designate a seat (Architect or Operator, as subject-matter counterparts) to challenge the test strategy before Engineering Lead approves it, or add this duty explicitly to Engineering Lead's role. |
| VERIFIER gap 7 | **test-strategy outputs list only Builder; three consumers exist.** Engineering Lead inputs and Operator inputs both list `test-strategy from Verifier`. My outputs list it only for Builder. Proposed fix: add `{artifact: test-strategy, for: Engineering Lead, acceptance: "EL approves; test types cover every NFR and acceptance approach covers every use case in scope (floor D5)"}` and `{artifact: test-strategy, for: Operator, acceptance: "Gates match the named test types and can be wired in CI/CD"}`. |
| VERIFIER gap 8 | **`verification evidence` output has no receiving input in Product's job.** Product's inputs list `increment verify evidence from Builder` and `review from Verifier`, but not `verification evidence from Verifier`. My fourth output has no corresponding receive. Proposed fix: add `{artifact: verification-evidence, from: Verifier}` to Product's inputs (not my job to fix, but flagged here). |
| VERIFIER gap 9 | **`review for Designer` missing from my outputs.** Designer's verifier is Verifier, but my outputs list no review for Designer. Proposed fix: add `{artifact: review, for: Designer, acceptance: "Each finding has a severity, and open_findings counts what is unanswered"}` to my outputs. |
| VERIFIER gap 10 | **`review for Builder` missing from my outputs.** Builder's verifier is Verifier, but my outputs list no review for Builder. Proposed fix: add `{artifact: review, for: Builder, acceptance: "Each finding has a severity, and open_findings counts what is unanswered"}` to my outputs. |
| VERIFIER gap 11 | **`review for Operator` missing from my outputs.** Operator's verifier is Verifier, but my outputs list no review for Operator. Proposed fix: add `{artifact: review, for: Operator, acceptance: "Each finding has a severity, and open_findings counts what is unanswered"}` to my outputs. |
| VERIFIER gap 12 | **`docs/enforcement.yml` absent from my standards.** When I raise findings, I must distinguish enforced checks from advisory ones. Enforcement status is in enforcement.yml, but it is not in my standards list. A fresh session may raise findings on advisory checks as if they were hard failures, or suppress findings thinking a check is already enforced when it is not. Proposed fix: add `docs/enforcement.yml` to my standards. |
| VERIFIER gap 13 | **No template for `verification evidence`.** My fourth output has no corresponding template. Each session producing this artifact will structure it differently, making it harder to compare across increments and easier to omit CI-sourced exit counts. Proposed fix: add `docs/templates/verification-evidence.md` and add it to my templates list. |
| VERIFIER gap 14 | **`qualified_layers` covers only deployment-runtime and operations, but I must challenge artifacts across all layers.** D6 requires challenger to be qualified for the layer they challenge. Architect covers five layers; Builder covers four. I qualify for two. Without a fix, D6 will refuse my challenges on data, services-apis, integration, and frontend layers — precisely the layers where most implementation defects occur. Proposed fix: either expand `qualified_layers` to include all layers, or add a D6 exception for the designated verifier seat. |
| VERIFIER gap 15 | **`[Designer, Verifier]` not in `incompatible_pairs`.** Designer's verifier is me. If a single holder held both seats, they could challenge their own ux-design without the SEATS check refusing it. Proposed fix: add `[Designer, Verifier]` to `incompatible_pairs`. |
| METHOD gap 1 | **No gate prevents Builder from starting before the test-strategy is approved.** Delivery sets the increment plan and cuts stories before the test strategy is necessarily approved. Builder's trigger fires when "an increment intent is approved and its tests are red in CI." If the test strategy is not yet approved, Builder has no acceptance-test spec to write from. The process advisory (E2, v0.3) says tests land before implementation, but no hard gate enforces that the test strategy precedes the first test. |
| METHOD gap 2 | **No escalation path when the Engineering Lead (sole human seat holder) is unavailable.** Both human seats are one person. If that person is unavailable to approve my test strategy, the process stalls. STATE.md records the open decision, but no escalation authority is named. The single-principal disclosure in CLAUDE.md acknowledges this for approvals generally; it applies equally to test-strategy approval. |
| METHOD gap 3 | **No defined artifact type for author review responses.** When I issue a review, the author must respond item by item. The response is a named document (it lives beside the artifact), but no artifact type, prefix, directory, or template is defined for it. A fresh authoring session answering my findings has no canonical form to use. |
| METHOD gap 4 | **`verification evidence` and `increment verify evidence` may be conflated.** Builder sends `increment verify evidence` to Product and to me. I produce `verification evidence` for Product. Two artifacts with similar names flow to the same consumer (Product) and serve related but distinct purposes (raw CI output vs. synthesised verdict). Without a clear artifact-type distinction, sessions may treat them as the same artifact and skip one. |
