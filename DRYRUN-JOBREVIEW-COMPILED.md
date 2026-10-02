# DRYRUN-JOBREVIEW — Compiled

## Context visible to this (Steward / compilation) session

### Project instruction files in context

1. **CLAUDE.md** (`/CLAUDE.md`) — mission and principles slots are unfilled template
   placeholders (`{{double braces}}`); bootstrap has not run. Core rules in effect:
   session protocol (read CLAUDE.md + STATE.md + input manifest only; work on own branch;
   no `git stash`; commit before ending; treat conversation as disposable); five-role
   artifact chain (Consulted → Author → Challenger → Approver → Consumer); governance
   (agents branch and PR only, never push to main); single-principal disclosure (Intent
   Owner and Engineering Lead are one person, no independent review at this stage). All
   nine rules listed under §Rules no check enforces yet are advisory. §Rules that stay
   with judgment includes: consult before framing; near-miss countermeasure is a redesign
   not a reminder; diagram governs structure; gap that no seat can judge opens a crew
   review; prescribe outcomes not steps; never declare a qualification to make a check
   pass.

2. **STATE.md** (`/STATE.md`) — cycle 1, setup phase. `active_tracks: []`. No open
   decisions. No mid-task work left. Product description field is empty (bootstrap has not
   run).

3. **No task input manifest in the repository.** This session received its task via the
   conversation prompt. Per CLAUDE.md §3, a decision counts only once it is written to a
   named artifact. This compiled document is that artifact.

4. **All eight seat review files**, fetched from their branches and read in this session:
   - `DRYRUN-JOBREVIEW-Product.md` on `jobreview-Product` (commit f74dcff)
   - `DRYRUN-JOBREVIEW-Delivery.md` on `jobreview-Product` (commit c28ec30)
   - `DRYRUN-JOBREVIEW-Architect.md` on `jobreview-Architect`
   - `DRYRUN-JOBREVIEW-Builder.md` on `jobreview-Builder`
   - `DRYRUN-JOBREVIEW-Designer.md` on `jobreview-Designer`
   - `DRYRUN-JOBREVIEW-Operator.md` on `jobreview-Operator`
   - `DRYRUN-JOBREVIEW-Verifier.md` on `jobreview-Verifier`
   - `DRYRUN-JOBREVIEW-Steward.md` on `jobreview-Steward`

### Notes about the person

- Email: imran.canuck@gmail.com (authorship and attribution only)
- Git user: PublicEnemage
- Holds: Intent Owner seat and Engineering Lead seat (listed as "Human 1" in
  `docs/roles.yml`; bootstrap name substitution has not occurred)
- Single-principal disclosure applies (CLAUDE.md Governance): one person holds both human
  seats; no independent review is available at this governance stage

---

## Table of contents

1. [Proposed changes to job descriptions](#1-proposed-changes-to-job-descriptions)
2. [Peer ratings per seat](#2-peer-ratings-per-seat)
3. [Wiring mismatches](#3-wiring-mismatches)
4. [Overlaps between seats](#4-overlaps-between-seats)
5. [Help protocols, side by side](#5-help-protocols-side-by-side)
6. [Authority statements vs. descriptions](#6-authority-statements-vs-descriptions)
7. [PRODUCT and METHOD gaps, deduplicated](#7-product-and-method-gaps-deduplicated)
8. [Leak log](#8-leak-log)

---

## 1. Proposed changes to job descriptions

Each row shows who proposed the change and which other sessions independently support it.
"Support" means the other session flagged the same wiring gap from their side; it is not
an endorsement of the proposed fix. Sessions that found the same gap on the receiving end
are listed under "also raised by."

### Product seat

| Proposed change | Proposed by | Also raised by |
|---|---|---|
| Change input #4 from `increment verify evidence from Builder` to `verification evidence from Verifier` | Product (gap 1) | Verifier (gap 8) — receiver side |
| Add `{artifact: increment-intent, for: Builder}` to outputs | Product (gap 2) | Builder — input #1 is listed but has no declared sender |
| Add `{artifact: story, for: Delivery}` to outputs | Product (gap 3) | Delivery (gap 1) — receiver side |
| Add `{artifact: delivery-system, from: Delivery}` to inputs | Product (gap 4) | Delivery — sends it to Product but Product has no receive |
| Add `{artifact: conceptual-design, from: Architect}` to inputs | Product (gap 5) | Architect — output #3 targets Product but Product has no receive |
| Extend value statement: add "…and writes the increment-intent and stories that carry work to Builder" | Product (value) | — |
| Add `{artifact: users-use-cases, for: Designer}` to outputs | Designer (gap 10) | Designer — cannot notify Designer at use-case approval without this |

### Delivery seat

| Proposed change | Proposed by | Also raised by |
|---|---|---|
| Add `{artifact: story (with input manifest), for: Builder}` to outputs; or clarify that story-authorship stays with Product and Delivery orders/verifies manifests | Delivery (gap 2) | Builder (gap 1 partial, gap 14 partial) |
| Clarify story-authorship model: either Product authors to Delivery's template (Model A) or Delivery authors for Builder (Model B); make explicit in both seats | Delivery (gap 1) | Product (value note) |
| Expand `delivery-system` output consumers to include Builder alongside Product | Delivery (value) | Builder (gap 14) |
| Add `{artifact: review, for: Delivery}` to Verifier's outputs to close the Verifier→Delivery review path | Delivery (gap 4) | Verifier (gap 9 partial) |

### Architect seat

| Proposed change | Proposed by | Also raised by |
|---|---|---|
| Change `{artifact: risk-assessment, from: Operator}` to "redesign only; Operator cannot produce this before my NFR is approved" | Architect (gap 1) | Operator — same circular dependency noted |
| Add `status: approved` as explicit precondition on inputs 1 and 2 | Architect (gap 2) | Designer (gap 2), Builder (§Engineering Lead conditions) |
| Add Engineering Lead as co-consumer of `nfr` output | Architect (gap 3) | Verifier (gap 7 partial) — EL also needs it |
| Update `conceptual-design` acceptance to cite "(floor D1, D13)" | Architect (gap 4) | — |
| Add Engineering Lead as consumer of `architecture` output | Architect (gap 5) | — EL's inputs list architecture from Architect but Architect's outputs don't list EL |
| Add `{artifact: intent, from: Product (approved)}` to inputs | Architect (gap 8) | Designer (gap 3) — both sessions flag missing intent as input |
| Add `{artifact: nfr, from: Architect}` explicitly to Verifier's inputs (remove reliance on "any artifact in review" catch-all) | Architect (gap 9) | Verifier (gap 3) — Verifier independently flagged missing nfr input |
| Define authoring convention for `integration` and `deployment-runtime` layers (Architect vs. Operator) | Architect (gap 10) | Operator — same shared-layer ambiguity noted |
| Open crew review for `domain-core` layer (no qualified seat in minimum crew) | Architect (gap 6) | — required by CLAUDE.md §Rules that stay with judgment |
| Adopt Data Architect seat or add `data` layer qualification to another seat (no challenger for Architect's data layer) | Architect (gap 7) | — |
| Add `{artifact: ux-design, from: Designer}` as optional input (when UI in scope) | Architect (§Designer conditions) | Designer — flags that approved ux-design never formally reaches Architect |

### Builder seat

| Proposed change | Proposed by | Also raised by |
|---|---|---|
| Add stated refusal procedure when acceptance tests are absent from CI | Builder (gap 2) | — |
| Add `{artifact: ux-design, from: Designer}` and `{artifact: design system, from: Designer}` to inputs (conditional on UI increments) | Builder (gap 3) | Designer (gap 12) — receiver side |
| Add `{artifact: nfr, from: Architect}` to inputs | Builder (gap 4) | — |
| Add `{artifact: review, from: Verifier}` to inputs | Builder (gap 5) | Verifier (gap 10) — output side |
| Clarify whether ADR obligation covers "patterns" as well as dependencies; update floor I3 or add a new floor row | Builder (gap 6) | — |
| Clarify routing of `increment verify evidence`: either add Operator and Product as explicit consumers in Builder's outputs, or update Operator's and Product's inputs to say `from: Verifier` | Builder (gap 7) | Operator — same gap from receive side; Verifier (gap 8) |
| Fix output 1 acceptance test phrasing to say "acceptance tests committed by Verifier pass in CI" | Builder (gap 8) | — |
| Add `docs/enforcement.yml` to Builder's standards | Builder (gap 9) | Verifier (gap 12) — same gap |
| Clarify whether story template is for reading or writing; if writing, add challenge path | Builder (gap 10) | — |
| Add implementation-design template | Builder (gap 11) | — |
| Add PR approval as named artifact step in outputs or a PR template | Builder (gap 12) | — |
| Consider adding `[Builder, Delivery]` to incompatible_pairs | Builder (gap 13) | — |
| Add `{artifact: delivery-system, from: Delivery}` to inputs | Builder (gap 14) | Delivery (gap 2 partial) |
| Add `[Builder, Operator]` to incompatible_pairs | Builder (gap 15) | Operator (method gap 2), Steward (method gap 2) |

### Designer seat

| Proposed change | Proposed by | Also raised by |
|---|---|---|
| Require `has_ui` flag in intent/business-case artifact; or require Intent Owner to sign floor D4 not-applicable before Designer's trigger is skipped | Designer (gap 1) | — |
| State that trigger requires both use-cases AND architecture to be approved, not use-cases alone | Designer (gap 2) | — |
| Add `{artifact: intent, from: Product (approved)}` to inputs | Designer (gap 3) | Architect (gap 8) |
| Add `{artifact: review, from: Verifier}` to inputs | Designer (gap 4) | Verifier (gap 9) |
| Verify that ux-design template includes an experience-intent section | Designer (gap 5) | — |
| Rewrite ux-design output consumer chain: Intent Owner first (for approval), then Builder and Architect as downstream consumers | Designer (gap 6) | — |
| Add `design-system` artifact type to `docs/artifact-types.yml` with prefix, dir, human_approver, and template | Designer (gap 7) | Builder (gap 3) — Builder needs the artifact type to receive it |
| Add `[Designer, Verifier]` to incompatible_pairs | Designer (gap 8) | Verifier (gap 15) — same proposal from Verifier side |
| State frontend authoring convention: Architect authors technical frontend section; Designer authors interaction section; each challenges the other | Designer (gap 9) | Architect (method gap 4) |
| Add `{artifact: users-use-cases, for: Designer}` to Product's outputs | Designer (gap 10) | — same as Product proposed change above |
| Add `{artifact: review, for: Designer}` to Verifier's outputs | Designer (gap 11) | Verifier (gap 9) |
| Add `{artifact: ux-design, from: Designer}` and `{artifact: design system, from: Designer}` to Builder's inputs | Designer (gap 12) | Builder (gap 3) |

### Operator seat

| Proposed change | Proposed by | Also raised by |
|---|---|---|
| Rewrite trigger as two phases: (a) NFRs+architecture approved → produce risk assessment, cicd, ops-readiness; (b) cicd approved + verify evidence received → authorize release | Operator (gap 1) | — |
| Add incident-response artifact type and template; add output entry for Operator | Operator (gap 2) | Steward (method gap 1 partial) |
| Add "increment verify evidence received from Builder" as explicit trigger condition | Operator (gap 3) | — |
| Add `{artifact: risk-assessment, for: Architect, acceptance: "covers data classification and main threats (floor C5)"}` to outputs | Operator (gap 4) | Architect (gap 1) — Architect's inputs list it but Operator's outputs don't |
| Add `{artifact: review, from: Engineering Lead}` to inputs, or clarify that Verifier mediates all findings | Operator (gap 5) | — |
| Add transitional acceptance test for release-decision until E13 ships | Operator (gap 6) | — |
| Add Engineering Lead, Verifier and Steward as consumers of `cicd` | Operator (gap 7) | Builder, Verifier (gap 7), Steward (gap 6) |
| Add `docs/artifact-types.yml` to Operator's standards | Operator (gap 8) | — |
| Add `smoke-cycle-record.md` template and naming convention; add to Operator's templates | Operator (gap 9) | Steward (gap 15 proposed fix) |

### Verifier seat

| Proposed change | Proposed by | Also raised by |
|---|---|---|
| Change input #1 `from: Product` to `from: any authoring seat` (or list each authoring seat separately) | Verifier (gap 1 input note) | — |
| Add `{artifact: nfr, from: Architect}` to Verifier's inputs | Verifier (gap 3) | Architect (gap 9) |
| Add `{artifact: users-use-cases, from: Product (approved)}` to Verifier's inputs | Verifier (gap 4) | — |
| Define review-response artifact type (or convention in the review template) and add second-pass input | Verifier (gap 5) | Steward (method gap 3) |
| Designate Architect or Operator as content challenger for test-strategy before EL approves it | Verifier (gap 6) | Steward (gap 13 partial) |
| Add Engineering Lead and Operator as consumers of `test-strategy` | Verifier (gap 7) | Operator — inputs list it from Verifier |
| Add `{artifact: verification-evidence, from: Verifier}` to Product's inputs | Verifier (gap 8) | — receiver-side gap in Product |
| Add `{artifact: review, for: Designer}` to Verifier's outputs | Verifier (gap 9) | Designer (gap 11) |
| Add `{artifact: review, for: Builder}` to Verifier's outputs | Verifier (gap 10) | Builder (gap 5) |
| Add `{artifact: review, for: Operator}` to Verifier's outputs | Verifier (gap 11) | Operator |
| Add `docs/enforcement.yml` to Verifier's standards | Verifier (gap 12) | Builder (gap 9) |
| Add verification-evidence template | Verifier (gap 13) | — |
| Expand `qualified_layers` to all layers, or add D6 "designated verifier" exception | Verifier (gap 14) | — structural contradiction |
| Add `[Designer, Verifier]` to incompatible_pairs | Verifier (gap 15) | Designer (gap 8) |

### Steward seat

| Proposed change | Proposed by | Also raised by |
|---|---|---|
| Define "compliance hold" output or state explicitly that Steward audit is advisory at merge time | Steward (gap 1) | — |
| Add near-miss report artifact type; name it as a formal output in any seat observing a near-miss | Steward (gap 2) | — |
| Define "unowned-decision failure" in CLAUDE.md or artifact-types.yml | Steward (gap 3) | — |
| Add "Engineering Lead merges to protected branch" as a trigger condition (or document post-merge audit timing) | Steward (gap 4) | — |
| Either add Steward as consumer of review in Verifier's outputs, or document pull-based audit and update Steward's inputs | Steward (gap 5) | Verifier |
| Add Steward as consumer of `cicd` in Operator's outputs | Steward (gap 6) | Operator (gap 7) |
| Add note in Steward's inputs: audit scope is repository-wide; the three listed inputs are formally received receipts | Steward (gap 7) | — |
| Update value statement: "Files every near-miss as a registry entry with a proposed check; the countermeasure ships when Engineering Lead approves it" | Steward (gap 8) | — |
| Add Engineering Lead as second consumer of "audit of process adherence" | Steward (gap 9) | — |
| Add Delivery as conditional consumer of registry entries (when hazard class covers delivery-process failures) | Steward (gap 10) | — |
| Add `audit-of-process-adherence.md` template | Steward (gap 11) | — |
| Add `docs/artifact-types.yml` and `docs/roles.yml` to Steward's standards | Steward (gap 12) | — |
| Add `{artifact: approved-role-proposal, from: Engineering Lead}` to Steward's inputs | Steward (gap 14) | — Engineering Lead's outputs list it for Steward but Steward has no receive |
| Add metrics computation script or formula to tools/checks/ or a standards document | Steward (gap 15) | — |

---

## 2. Peer ratings per seat

Each session rated the other seats. Ratings: **Accept** / **Accept with conditions** / not stated.
"Conditions" are wiring or description gaps; they do not indicate rejection.

The eight reviewing seats are across the top; the rated seat is in the left column.

| Rated seat | Product | Delivery | Architect | Builder | Designer | Operator | Verifier | Steward |
|---|---|---|---|---|---|---|---|---|
| Intent Owner | Accept | Accept | Accept | Accept + cond | Accept + cond | Accept + cond | Accept + cond | Accept + cond |
| Engineering Lead | Accept | Accept | Accept | Accept + cond | Accept | Accept + cond | Accept + cond | Accept + cond |
| Product | — | Accept + cond | Accept + cond | Accept + cond | Accept + cond | Accept | Accept + cond | Accept + cond |
| Delivery | Accept + cond | — | Accept | Accept + cond | Accept | Accept | Accept | Accept + cond |
| Architect | Accept + cond | Accept | — | Accept + cond | Accept + cond | Accept + cond | Accept + cond | Accept |
| Designer | Accept | Accept | Accept + cond | Accept + cond | — | Accept | Accept + cond | Accept |
| Verifier | Accept + cond | Accept | Accept + cond | Accept + cond | Accept + cond | Accept + cond | — | Accept + cond |
| Builder | Accept + cond | Accept + cond | Accept | — | Accept + cond | Accept + cond | Accept + cond | Accept |
| Operator | Accept | Accept | Accept + cond | Accept + cond | Accept | — | Accept + cond | Accept + cond |
| Steward | Accept | Accept | Accept | Accept | Accept | Accept | Accept + cond | — |

**Notes on conditions (by rated seat, summarised from all reviewers):**

- **Intent Owner (5 sessions add conditions):** Single-principal disclosure: one person holds Intent Owner and Engineering Lead; no independent review or escalation path. All sessions that noted conditions cited this.
- **Engineering Lead (5 sessions add conditions):** Same single-principal issue. Builder also notes that PR merges are not a named artifact in any job description.
- **Product (6 sessions add conditions):** Missing outputs (increment-intent, story); missing inputs (delivery-system, conceptual-design, verification evidence from Verifier); mis-named input (increment verify evidence from Builder).
- **Delivery (3 sessions add conditions):** Unsettled story-authorship model; stories-with-manifests not in formal outputs; no explicit output to Builder.
- **Architect (5 sessions add conditions):** Circular dependency on risk-assessment; domain-core and data-layer challenger gaps; shared-layer convention missing; intent and ux-design not in inputs.
- **Designer (4 sessions add conditions):** ux-design consumer chain broken; design-system has no artifact type; [Designer, Verifier] not in incompatible_pairs; review from Verifier not in inputs.
- **Verifier (7 sessions add conditions):** qualified_layers contradicts challenge scope; test-strategy consumers under-declared; missing review outputs for Builder, Designer, Operator; no template for verification evidence.
- **Builder (6 sessions add conditions):** Missing inputs (ux-design, design system, nfr, review from Verifier, delivery-system); [Builder, Operator] not in incompatible_pairs.
- **Operator (4 sessions add conditions):** risk-assessment absent from formal outputs; cicd consumers under-declared; E13 not implemented; incident-response undefined.

---

## 3. Wiring mismatches

Each row is an artifact where the sender's output declaration and the receiver's input declaration are inconsistent.
"Fix" is the union of proposals across all sessions that raised the gap; conflicts between proposals are shown.

### Product / Delivery wiring

| Artifact | Sender declares | Receiver declares | Sessions | Proposed fix |
|---|---|---|---|---|
| `story` | Product (template only; not in outputs) | Delivery input #2: `from: Product` | Product (gap 3), Delivery (gap 1) | Product adds `{artifact: story, for: Delivery}` to outputs. Authorship model (Model A vs. B) must be resolved first. |
| `delivery-system` | Delivery output #1: `for: Product` | Product has no input for it | Product (gap 4), Delivery | Product adds `{artifact: delivery-system, from: Delivery}` to inputs. |
| `increment-plan` | Product output #2: `for: Delivery` | Delivery input #1: `from: Product` | — | Clean. No mismatch. |

### Product / Architect wiring

| Artifact | Sender declares | Receiver declares | Sessions | Proposed fix |
|---|---|---|---|---|
| `conceptual-design` | Architect output #3: `for: Product` | Product has no input for it | Product (gap 5), Architect | Product adds `{artifact: conceptual-design, from: Architect}` to inputs. |
| `intent` | Product (template only) | Architect has no input for it; Intent Owner outputs list it for Architect | Architect (gap 8), Designer (gap 3) | Architect and Designer both add `{artifact: intent, from: Product (approved)}` to inputs. |
| `users-use-cases` | Product output #1: `for: Architect` — Designer not listed | Designer input #1: `from: Product` | Designer (gap 10) | Product adds `{artifact: users-use-cases, for: Designer}` as a second consumer (or broadens existing output). |

### Verify-evidence routing

| Artifact | Sender declares | Receiver declares | Sessions | Proposed fix — conflict |
|---|---|---|---|---|
| `increment verify evidence` | Builder output #2: `for: Verifier` only | Operator input #4: `from: Builder`; Product input #4 (mis-named): `from: Builder` | Builder (gap 7), Operator, Verifier (gap 8) | **Conflict:** Builder proposes either adding Operator and Product as consumers in Builder's outputs, or changing Operator's and Product's inputs to `from: Verifier`. Verifier proposes they already synthesise this into `verification evidence` and that `verification evidence from Verifier` should replace the Builder input in Product. The correct resolution depends on whether Operator and Product receive raw CI output or Verifier's synthesis — this is an unresolved design decision. |
| `verification evidence` | Verifier output #4: `for: Product` | Product has no input for it (has `increment verify evidence from Builder` instead) | Verifier (gap 8) | Add `{artifact: verification-evidence, from: Verifier}` to Product's inputs; clarify that it replaces or supplements `increment verify evidence from Builder`. |

### Architect / Operator wiring

| Artifact | Sender declares | Receiver declares | Sessions | Proposed fix |
|---|---|---|---|---|
| `risk-assessment` | Operator (in templates, value; absent from formal outputs) | Architect input #3: `from: Operator` | Architect (gap 1, gap 10), Operator (gap 4) | Operator adds `{artifact: risk-assessment, for: Architect, acceptance: "covers data classification and main threats (floor C5)"}` to outputs. Timing note: on first pass, Operator cannot produce this before Architect's NFR is approved — scope to redesign only. |
| `nfr` | Architect output #2: `for: Verifier` | Verifier has no named input for it (catch-all only); Builder has no input for it | Architect (gap 9), Verifier (gap 3), Builder (gap 4) | Add `{artifact: nfr, from: Architect}` explicitly to Verifier's inputs. Consider adding to Builder's inputs too. |

### Architecture consumers

| Artifact | Sender declares | Receiver declares | Sessions | Proposed fix |
|---|---|---|---|---|
| `architecture` | Architect output #1: `for: Builder` — Engineering Lead not listed | Engineering Lead input #1: `from: Architect` | Architect (gap 5) | Architect adds Engineering Lead as first consumer (for approval), then Builder as downstream consumer. |

### Designer / Builder wiring

| Artifact | Sender declares | Receiver declares | Sessions | Proposed fix |
|---|---|---|---|---|
| `ux-design` | Designer output #1: `for: Builder` | Builder has no input for it; Intent Owner's outputs say they forward it to Architect but neither Designer's outputs nor Architect's inputs confirm this | Designer (gap 6, 12), Builder (gap 3), Architect (§Designer conditions) | Designer rewrites output to: Intent Owner first (for approval), then Builder and Architect as downstream consumers. Builder adds `{artifact: ux-design, from: Designer}` to inputs. Architect adds it as optional input. |
| `design system` | Designer output #2: `for: Builder` | Builder has no input for it; no artifact type defined | Designer (gap 7, 12), Builder (gap 3) | Add `design-system` artifact type. Builder adds input. Designer adds template. |

### Verifier review outputs

| Artifact | Sender declares | Receiver declares | Sessions | Proposed fix |
|---|---|---|---|---|
| `review for Designer` | Not in Verifier's outputs | Designer verifier is Verifier; Designer needs review as input | Verifier (gap 9), Designer (gap 4, gap 11) | Verifier adds `{artifact: review, for: Designer}`. Designer adds `{artifact: review, from: Verifier}` to inputs. |
| `review for Builder` | Not in Verifier's outputs | Builder verifier is Verifier; Builder (gap 5) flags missing input | Verifier (gap 10), Builder (gap 5) | Verifier adds `{artifact: review, for: Builder}`. Builder adds to inputs. |
| `review for Operator` | Not in Verifier's outputs | Operator verifier is Verifier | Verifier (gap 11), Operator | Verifier adds `{artifact: review, for: Operator}`. |
| `review for Delivery` | Not in Verifier's outputs | Delivery artifact chain requires review beside delivery-system | Delivery (gap 4) | Verifier adds `{artifact: review, for: Delivery}`. |
| `review for Steward` | Not in Verifier's outputs (Verifier lists Product and Architect only) | Steward input #1: `from: Verifier` | Steward (gap 5) | Either Verifier adds Steward as consumer, or Steward changes input to be explicit that it reads review files from the repository (pull-based). |

### Test-strategy and cicd consumers

| Artifact | Sender declares | Receiver declares | Sessions | Proposed fix |
|---|---|---|---|---|
| `test-strategy` | Verifier output #3: `for: Builder` only | Engineering Lead input: `from: Verifier`; Operator input: `from: Verifier` | Verifier (gap 7), Operator | Verifier adds Engineering Lead (for approval) and Operator as consumers. |
| `cicd` | Operator output #1: `for: Builder` only | Engineering Lead, Verifier, Steward all list `cicd from Operator` as input | Operator (gap 7), Builder, Verifier, Steward (gap 6) | Operator adds Engineering Lead, Verifier and Steward as consumers. |

### Steward inputs

| Artifact | Sender declares | Receiver declares | Sessions | Proposed fix |
|---|---|---|---|---|
| `approved-role-proposal` | Engineering Lead output: `for: Steward` | Steward has no input for it | Steward (gap 14) | Steward adds `{artifact: approved-role-proposal, from: Engineering Lead}` to inputs. |

---

## 4. Overlaps between seats

### Overlap A: Story authorship (Product vs. Delivery)

**Description:** Delivery's value statement says it "cuts and orders work so that every task a fresh session pulls carries its own input manifest." Product's templates include `story.md` and Delivery's inputs list `story from Product`. Both models (Product authors stories to Delivery's template; Delivery authors stories from the increment-plan) can be derived from the current job descriptions.

**Sessions that flagged this:** Product (value note), Delivery (gap 1), Builder (gap 1 partial).

**Conflict:** The two models assign authorship differently; whichever is chosen, both jobs must be updated simultaneously.

**No proposed winner.** Show the conflict; Engineering Lead decides.

---

### Overlap B: Frontend layer (Architect vs. Designer)

**Description:** Both seats list `frontend` in `qualified_layers`. D6 requires a different author and challenger per layer. The convention for who authors vs. challenges the frontend section of the architecture vs. the frontend flows in the UX design is unstated.

**Sessions that flagged this:** Architect (method gap 4), Designer (gap 9, method gap 3).

**Conflict:** Designer proposes "Architect authors technical frontend section; Designer authors interaction section; each challenges the other." Architect proposes this as a condition but does not specify the split. No agreed convention.

---

### Overlap C: Integration and deployment-runtime (Architect vs. Operator)

**Description:** Both seats list `integration` in `qualified_layers`. Architect also lists `deployment-runtime`. Without a stated convention, either seat could author or challenge those layers.

**Sessions that flagged this:** Architect (gap 10, method gap 6), Operator (§Architect conditions, §qualified_layers).

**No proposed winner.** Two possibilities: (a) Operator owns both by default; Architect can challenge. (b) Authoring seat is decided per artifact. No agreement across sessions.

---

### Overlap D: Builder and Operator (incompatible pair absent)

**Description:** `[Builder, Operator]` is not in `incompatible_pairs`. In the minimum-crew holders, Builder and Operator are both Agent A. A single holder designs the CI/CD gates and implements the code that must pass them.

**Sessions that flagged this:** Builder (gap 15), Operator (method gap 2), Steward (method gap 2).

**Agreement across three sessions:** All three propose adding `[Builder, Operator]` to `incompatible_pairs`.

---

### Overlap E: Builder and Delivery (incompatible pair absent)

**Description:** `[Builder, Delivery]` is not in `incompatible_pairs`. A single holder could control their own task prioritization.

**Sessions that flagged this:** Builder (gap 13) only.

**No agreement.** Builder raises it as a concern but acknowledges the minimum-crew size may make it impractical.

---

### Overlap F: Verifier qualified_layers vs. challenge scope

**Description:** Verifier's `qualified_layers` covers only `[deployment-runtime, operations]` but Verifier is the designated challenger for Architect (five layers) and Builder (four layers). D6 requires challenger to be qualified for the layer being challenged.

**Sessions that flagged this:** Verifier (gap 14) — from within; implied by Architect (noting Verifier challenges their artifacts) and Builder.

**Conflict:** Either Verifier's `qualified_layers` must be expanded to all layers, or D6 must include a "designated verifier seat" exception. No agreement on which change is correct.

---

## 5. Help protocols, side by side

Each seat's help protocol is shown as two sub-tables: what it offers each other seat, and what it asks of each other seat. Only seats where the offer/ask is non-empty are shown.

### What each seat offers (non-empty rows only)

| Seat offering → | Product | Delivery | Architect | Builder | Designer | Operator | Verifier | Steward |
|---|---|---|---|---|---|---|---|---|
| To Intent Owner | Validation-verdict after each increment | Nothing | Nothing | Nothing | ux-design (in-review) for approval | Release-decision with post-deploy evidence | Nothing | Check: approval order and approved_at on their signed artifacts |
| To Engineering Lead | Nothing directly | delivery-system and role-proposals for review | NFR and architecture ready for review | Nothing formally | Nothing directly | ops-readiness; cicd | test-strategy (in-review) | Registry entries; audit of process adherence |
| To Product | Nothing | delivery-system (story template, cadence, etc.) | conceptual-design | Increment verify evidence (raw CI) | Nothing formally | Nothing | review; verification evidence | Nothing |
| To Delivery | approved increment-plan; stories per increment | — | Nothing | Task-pull signal | Nothing | Nothing | Nothing | audit of process adherence |
| To Architect | approved use-cases and business-case | Nothing | — | Consumer feedback if arch fails | approved ux-design (after IO approval) | risk-assessment | review of each Architect artifact | Nothing |
| To Designer | approved users-use-cases | Nothing | architecture (frontend section) | Nothing | — | Nothing | review of each ux-design artifact | Nothing |
| To Verifier | Every Product artifact in-review | delivery-system in-review | architecture and nfr in-review | Implementation + verify evidence | ux-design in-review | cicd in-review | — | Clean review files: format, answered, no self-review |
| To Builder | approved increment-intent | stories with input manifests (ordered) | approved architecture | — | approved ux-design and design system | cicd | approved test-strategy; review of implementation | Nothing |
| To Operator | Nothing | Nothing | approved nfr and architecture | increment verify evidence | Nothing | — | test-strategy (after EL approval); review of Operator artifacts | Nothing |
| To Steward | Clean process trail: status transitions, artifacts in correct folders, parents cited | Clean process trail | Clean artifact trail: parents cited, status transitions, diagram check passing | Audit trail: ADRs filed, no blanket skips, migrations unedited | Clean artifact trail | cicd; smoke-cycle records in docs/archive | Process-compliant review files | — |

### What each seat asks of others (non-empty rows, summarised)

| Asking seat | Asks of Product | Asks of Delivery | Asks of Architect | Asks of Builder | Asks of Designer | Asks of Operator | Asks of Verifier | Asks of EL / IO |
|---|---|---|---|---|---|---|---|---|
| Product | — | Delivery-system | Approved architecture; conceptual-design | Nothing | UX design (when in scope) | Nothing | Review of each artifact; verification evidence | Problem statement with evidence; approval decisions |
| Delivery | Approved increment-plan; conforming stories | — | Nothing | Nothing | Nothing | Nothing | Review of delivery-system | Approval of delivery-system |
| Architect | Approved use-cases and business-case | Nothing | — | Nothing | ux-design (optional, when UI in scope) | Risk-assessment (redesign only) | Review of each artifact | Approval of architecture and NFR |
| Builder | increment-intent | Nothing formally | Approved architecture | — | Approved ux-design and design system (UI increments) | Approved cicd | Approved test-strategy; red acceptance tests in CI before implementation | Approved architecture and test-strategy (through EL) |
| Designer | Approved users-use-cases | Nothing | Approved architecture | Nothing | — | Nothing | Review of ux-design | Approval of ux-design; UI-in-scope determination |
| Operator | Nothing | Nothing | Approved nfr and architecture | Increment verify evidence (CI-sourced) | Nothing | — | Approved test-strategy | Approval of cicd and ops-readiness |
| Verifier | Approved use-cases | Nothing | Approved architecture and nfr | Increment verify evidence | Nothing | Approved cicd | — | Approval of test-strategy |
| Steward | Nothing | Committed delivery-system before cycle exit | Nothing | Nothing | Nothing | Smoke-cycle record in docs/archive | Review files for every approved artifact | Approval of registry entries; acknowledgment of audit at cycle exit |

---

## 6. Authority statements vs. descriptions

Each entry shows where a seat's authority statement claims more latitude than its job description provides.

### Product: "Owns backlog content"

*Claim:* Product decides what work exists and how it is ordered.
*Narrowing from the description:*
1. `delivery-system` (authored by Delivery) sets story format, hierarchy and cadence — Product writes stories but cannot choose their format.
2. `qualified_domains` is empty — Product cannot assert domain accuracy for domain-specific use cases; no challenger can confirm them under floor C8.
3. All Product artifacts have `human_approver: true` — Product can draft and submit but cannot close any artifact loop.
4. Intent Owner approves use cases; Product cannot move past the case gate without approval.
*(Source: Product §4 "Where the procedure left me less room.")*

---

### Delivery: "Owns the delivery process"

*Claim:* Delivery decides hierarchy, story template, cadence, track cap and metrics.
*Narrowing from the description:*
1. `delivery-system` must be approved by Engineering Lead (`human_approver: true`) — Delivery proposes, Engineering Lead approves.
2. Story template must produce stories satisfying floor I7, I1, I4 — form is flexible, required content is not.
3. Metrics must be computable from the repository — if a metric requires instrumentation not yet built, Delivery cannot produce it alone.
4. Track cap is only partially enforced by E9 (E7 not shipped) — authority to set the cap is real; mechanical enforcement is incomplete.
*(Source: Delivery §4 "Where the procedure left me less room.")*

---

### Architect: "Owns the data layer unless a Data Architect is adopted"

*Claim:* Architect is sole data-layer authority in the minimum crew.
*Narrowing from the description:*
1. No other seat in the minimum crew qualifies for `data` — Architect can author the data layer but D6 requires a different qualified challenger; none exists.
2. `domain-core` is unowned by any seat — Architect cannot author that layer either; floor D2 requires it.
3. Adoption criteria for Data Architect are in `docs/standards/data/README.md` which Architect's session was not permitted to read (not in manifest).
4. All Architect artifacts have `human_approver: true` — Engineering Lead must approve NFR and architecture before they reach any downstream consumer.
*(Source: Architect §4 "Where the procedure left me less room.")*

---

### Designer: "Designs how the product looks and behaves... so that interface decisions are drawn and not left to be read many ways"

*Claim:* Designer resolves interface ambiguity.
*Narrowing from the description:*
1. `design system` has no artifact type — it cannot be versioned, checked, or formally approved; decisions embedded in it are not auditable.
2. Designer cannot activate without an Intent Owner determination that the product has a UI — that determination has no named artifact channel.
3. `ux-design` must be approved by Intent Owner (`human_approver: true`) before Builder receives it — Designer does not decide when Builder sees the work.
4. No formal mechanism routes the approved ux-design to Architect — the downstream consistency check is undescribed.
*(Source: Designer §4 "Where the procedure left me less room.")*

---

### Verifier: "Finds what is wrong, missing or inconsistent, as a fresh session"

*Claim:* Verifier is the universal challenger for all artifact content.
*Narrowing from the description:*
1. `qualified_layers` covers only `[deployment-runtime, operations]` — under D6, Verifier cannot formally challenge the `data`, `services-apis`, `integration` or `frontend` layers of any architecture or implementation artifact.
2. Verifier authors the test-strategy and standards — "never verifies its own work" means no seat challenges Verifier's most important output for content accuracy.
3. Three trigger modes (challenger, test-pre-checker, validation producer) are in one job description with no mode selector — the task manifest must specify mode; the job description does not.
*(Source: Verifier §4 "Where the procedure left me less room.")*

---

### Operator: "Owns... the release decision backed by the post-deploy check"

*Claim:* Operator is the authority for deployment readiness.
*Narrowing from the description:*
1. E13 (post-deploy check) is `planned`, not implemented — Operator cannot satisfy its own acceptance test for release decisions until E13 ships.
2. Incident response has no output artifact — when an incident fires Operator's trigger, Operator has no named artifact to produce and no evidence standard to meet.
3. `risk-assessment` is in the value statement and templates but absent from formal outputs — a fresh session reading only the outputs section could miss producing it.
*(Source: Operator §4 "Where the procedure left me less room.")*

---

### Steward: "Files every near-miss, and the countermeasure is a check, never a reminder to be careful"

*Claim:* Steward closes near-misses by filing a check as the countermeasure.
*Narrowing from the description:*
1. Steward proposes the check; Engineering Lead approves it — the value statement elides this approval step.
2. No merge-blocking authority — Steward triggers on each PR to a protected branch but has no stated mechanism to hold a merge pending audit.
3. Near-miss discovery channel is undefined — Steward discovers near-misses through its own audit, not through a named artifact channel.
4. Mutual verification loop — Steward verifies Engineering Lead; Engineering Lead verifies Steward. No independent third party at this governance stage.
*(Source: Steward §4 "Where the procedure left me less room.")*

---

### Builder: "Never introduces a dependency or pattern without an ADR"

*Claim:* Builder's ADR obligation covers both dependencies and cross-cutting patterns.
*Narrowing from the description:*
1. The verifier evidence cites floor I3 for "every new dependency" only — patterns are in the value statement but not in the floor citation or the verifier's evidence check.
2. A session can satisfy the Verifier's evidence check without satisfying the value statement's broader prohibition on undocumented patterns.
*(Source: Builder (gap 6).)*

---

## 7. PRODUCT and METHOD gaps, deduplicated

### Notes on labelling

Sessions used "PRODUCT gap" labels differently:
- Product session: used for wiring gaps in the Product seat's job.
- Other sessions (Builder, Operator, Steward): used for meta-level gaps about bootstrap state and task manifest.

The table below deduplicated by substance. Bootstrap/manifest gaps are listed once regardless of how many sessions labelled them PRODUCT.

### PRODUCT-substance gaps (gaps in job descriptions or artifact wiring)

| Gap | Description | Sessions |
|---|---|---|
| P-1 | `increment verify evidence` in Product's inputs names Builder as the source and uses Builder's artifact name; should be `verification evidence from Verifier` | Product (gap 1), Verifier (gap 8) — **2 sessions** |
| P-2 | `increment-intent` is in Product's templates and Builder lists it as a required input, but it is absent from Product's outputs | Product (gap 2) — **1 session** |
| P-3 | `story` is in Product's templates and Delivery lists it as an input from Product, but it is absent from Product's outputs | Product (gap 3), Delivery (gap 1) — **2 sessions** |
| P-4 | `delivery-system` is sent by Delivery to Product but absent from Product's inputs | Product (gap 4), Delivery (implicit) — **2 sessions** |
| P-5 | `conceptual-design` is sent by Architect to Product but absent from Product's inputs | Product (gap 5), Architect (§Product conditions) — **2 sessions** |
| P-6 | Bootstrap has not run: mission, principles and seat holder names are unfilled; `qualified_domains` is `{}` | Product, Builder, Operator, Steward — **4 sessions** |
| P-7 | Task was delivered via conversation prompt, not an input manifest; no manifest artifact exists in the repository | All 8 sessions — **8 sessions** |

### METHOD gaps (process design gaps visible from across seats)

| Gap | Description | Sessions |
|---|---|---|
| M-1 | **No escalation path for blocked human seats.** Intent Owner and Engineering Lead are one person. If that person is unavailable, no gate can pass, no artifact can be approved, and no escalation authority exists. STATE.md records the open decision; no further action is defined. | Product (gap 1), Architect (gap 7), Builder (gap 2), Designer (gap 5), Operator (gap 1), Verifier (gap 2), Steward (gap 3) — **7 sessions** |
| M-2 | **[Builder, Operator] not in incompatible_pairs.** Builder implements code; Operator designs the CI/CD gates that code must pass. The same holder could lower a gate to pass failing code. | Builder (gap 15), Operator (method gap 2), Steward (method gap 2) — **3 sessions** |
| M-3 | **UX design approval chain is incomplete.** Designer outputs ux-design for Builder; Intent Owner's outputs say they approve and forward it to Architect; Architect's inputs don't list it. No seat's job describes the full three-hop chain end-to-end. | Product (gap 3), Designer (gap 6, method gap 1), Architect (§Designer conditions) — **3 sessions** |
| M-4 | **Approval signal is implicit.** After a human approver changes an artifact's status to `approved`, no formal artifact confirms this to the authoring seat. Sessions infer approval from the status field. | Product (gap 2), Architect (gap 2), Builder (§EL conditions) — **3 sessions** |
| M-5 | **Frontend layer tiebreaker is absent.** Both Architect and Designer qualify for `frontend`. When their decisions conflict across artifacts, no seat has authority to adjudicate. The diagram-governs rule applies within an artifact, not across artifacts. | Architect (method gap 4), Designer (gap 9, method gap 3) — **2 sessions** |
| M-6 | **Shared layer authoring convention undefined for `integration` and `deployment-runtime`.** Both Architect and Operator qualify. Neither job states who authors vs. challenges each of these layers on a given artifact. | Architect (method gap 6), Operator (§qualified_layers) — **2 sessions** |
| M-7 | **No gate prevents Builder from starting before test-strategy is approved.** Delivery cuts stories from the increment-plan; Builder triggers when "increment intent is approved and its tests are red in CI." The test-strategy may not yet be approved at that point. | Verifier (method gap 1), Delivery (value note) — **2 sessions** |
| M-8 | **No defined artifact type for author review responses.** When Verifier issues a finding, the author must respond item by item. No artifact type, prefix, directory or template is defined for the response. | Verifier (method gap 3), Steward (§Verifier conditions) — **2 sessions** |
| M-9 | **`verification evidence` (from Verifier) and `increment verify evidence` (from Builder) may be conflated.** Two artifacts with similar names flow to the same consumer (Product). Without a clear type distinction, sessions may treat them as the same artifact. | Verifier (method gap 4) — **1 session** |
| M-10 | **No automatic trigger mechanism.** E7 (harness hooks) is planned for v0.2. Until it ships, session dispatch requires human initiation for each trigger event. | Delivery (method gap 1) — **1 session** |
| M-11 | **Metric breach threshold has no agreed floor before first delivery-system is authored.** The Delivery trigger "a flow metric breaches its limit" cannot fire until limits are set, but limits are set inside the delivery-system artifact that must be authored first. | Delivery (method gap 2), Delivery (gap 3) — **1 session** |
| M-12 | **domain-core layer and `qualified_domains` both empty.** No seat can author or challenge the domain-core layer. Floor D2 requires it. No seat is chartered to proactively open the crew review that CLAUDE.md requires. | Architect (method gap 1, gap 6) — **1 session** |
| M-13 | **Approved artifact routing to Builder is ambiguous.** Architect's outputs list architecture `for: Builder`; Engineering Lead's outputs also list "approved architecture for Builder." After approval, it is unclear whether Builder should read Architect's version or wait for Engineering Lead to re-file it. | Architect (method gap 2) — **1 session** |
| M-14 | **Role-proposal peer-review obligation is undiscovered.** E17 requires every agent seat that sends input to or consumes output from a proposed new seat to provide independent peer review. No mechanism notifies those seats that a proposal is in-review. | Architect (method gap 3) — **1 session** |
| M-15 | **D6 enforcement does not confirm the right qualified seat challenged each section.** SEATS checks declared seats in front matter; it does not verify that the declared challenger is actually qualified for the layer they challenged. | Architect (method gap 5) — **1 session** |
| M-16 | **No formal procedure for Builder to report that an architecture section fails the consumer duty.** "The artifact goes back" (CLAUDE.md) but no named artifact, seat to notify, or recording location is specified. | Builder (method gap 1) — **1 session** |
| M-17 | **No gate prevents Builder from starting a use case before its UX design is approved.** Builder's trigger does not require an approved ux-design; Delivery does not gate the increment plan on ux-design approval. | Designer (method gap 2) — **1 session** |
| M-18 | **Operator's risk assessment may arrive after UX design is approved.** If Designer's ux-design is approved first, it may include interaction patterns that Operator later flags as security/privacy risks, with no artifact-level mechanism to reopen the design. | Designer (method gap 4) — **1 session** |
| M-19 | **Validation-verdict and release-decision reach Intent Owner independently.** No coordination ensures both are present before the same gate review. Intent Owner could act on one without the other. | Product (gap 4) — **1 session** |
| M-20 | **benefits-check has no owning seat.** The template and artifact type exist; no seat's job lists it as an output or input. | Product (gap 5) — **1 session** |
| M-21 | **Product's `qualified_layers: []` may limit validation-verdict quality for technically-defined use cases.** For use cases with NFR-based pass criteria, Product relies entirely on Verifier's synthesis with no independent layer judgment. | Builder (method gap 3) — **1 session** |
| M-22 | **No procedure for Steward discovering a violation between formal trigger events.** CLAUDE.md §3 requires decisions to be written to a named artifact; without a trigger, Steward has no defined authority to act on an inter-cycle discovery. | Steward (method gap 1) — **1 session** |
| M-23 | **Single-principal disclosure weakens every gate at this governance stage.** One person holds Intent Owner and Engineering Lead; every approval, every gate, every human verifier trace back to the same individual. | Steward (method gap 3) explicitly; all 8 sessions by implication — **1 explicit + 7 implicit** |
| M-24 | **Incident response is triggered but has no process, output artifact or escalation path.** "A security, privacy or run incident opens" fires Operator's trigger, but no artifact type, template, or workflow covers it. | Operator (gap 2, method gap 3) — **1 session** |

---

## 8. Leak log

This section records each session's stated context (what files the session reported reading)
and any evidence that the session read another seat's review before writing its own.
No judgment is made about whether cross-reading affected the content. Conflicts between
proposals are documented in §3 above; this section records only the fact of the reading.

### Session contexts as reported

| Session | Files stated as read | Notes |
|---|---|---|
| Product | CLAUDE.md, STATE.md | Explicitly stated no task input manifest; task received via conversation prompt |
| Delivery | CLAUDE.md, STATE.md | Explicitly stated no task input manifest; deviation recorded in review |
| Architect | CLAUDE.md, STATE.md | Explicitly stated no task input manifest; deviation noted |
| Builder | CLAUDE.md, STATE.md | Explicitly stated no task input manifest; deviation noted |
| Designer | CLAUDE.md, STATE.md | Explicitly stated no task input manifest; deviation noted |
| Operator | CLAUDE.md, STATE.md | Explicitly stated no task input manifest; deviation noted |
| Verifier | CLAUDE.md, STATE.md | Explicitly stated no task input manifest; deviation noted |
| Steward | CLAUDE.md, STATE.md, docs/roles.yml (full), docs/enforcement.yml (full), docs/dor/floor.yml (partial), docs/templates/registry-entry.md | Only session that reported reading beyond the two mandatory files. Reported no input manifest; deviation noted. |

### Evidence of cross-reading

#### Delivery session — confirmed

**Mechanism:** Both the Product review and the Delivery review were committed on the same
branch (`jobreview-Product`). The Product review (commit f74dcff) predates the Delivery
review (commit c28ec30) on that branch. When the Delivery session ran, `DRYRUN-JOBREVIEW-Product.md` was already in the working tree.

**Text evidence:** In `DRYRUN-JOBREVIEW-Delivery.md` §1 input #2 (story from Product):

> "But Product's outputs do not list story as an explicit output (**PRODUCT gap 3, identified
> by the Product seat review**)."

This phrase directly names the other review document and its gap label. No other session
uses this cross-referential formulation.

**Also in Delivery §2 (Product conditions):** The two conditions listed — "Product must add
`story for Delivery` to its outputs" and "Product must add `delivery-system from Delivery`
to its inputs" — match exactly the gap numbers and proposed fixes in the Product review
(PRODUCT gap 3 and PRODUCT gap 4). While these gaps could be independently discovered,
the explicit citation ("identified by the Product seat review") confirms the reading.

#### Steward session — cross-references present; mechanism unclear

**Mechanism:** The Steward review is on `jobreview-Steward`. No other review file was
in that branch's working tree at commit time (only `DRYRUN-JOBREVIEW-Steward.md` was
added). However, the Steward review cites other reviews by their gap labels.

**Text evidence:**

In `DRYRUN-JOBREVIEW-Steward.md` §2 (Verifier section):
> "Verifier's outputs do not list review for Builder (noted in both Builder and Operator
> reviews)."

In §2 (Operator section):
> "The Builder and Operator reviews (BUILDER gap 7 / OPERATOR gap 7) flagged that
> Engineering Lead, Verifier and Steward all receive cicd."

In STEWARD gap 6:
> "Both Builder and Operator reviews flagged that Engineering Lead, Verifier and Steward
> all receive cicd."

**Assessment:** The Steward review names other reviews by their exact gap labels. The
stated context section does not list those reviews as files read. Either:
(a) The Steward session read the other branches without recording the reads in the context
section, violating the session protocol rule "Read nothing else unless the manifest names
it"; or
(b) The Steward session independently arrived at the same gap and retroactively labelled it
by the gap number it expected to appear in the other reviews.

The phrasing "noted in both Builder and Operator reviews" in the present tense, citing
specific gap numbers, is most consistent with (a). The deviation from stated context
is recorded here. No determination of cause is made.

#### All other sessions — no evidence found

Product, Architect, Builder, Designer, Operator, and Verifier reviews contain no explicit
references to other seat reviews, no citations of other gap labels by name, and no phrasing
that implies awareness of another review's specific content. Each independently identifies
the wiring gaps from its own side.
