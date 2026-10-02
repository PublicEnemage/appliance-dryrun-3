# DRYRUN-JOBREVIEW — Steward

## Context visible to this session

### Project instruction files in context

1. **CLAUDE.md** (the Constitution, `/CLAUDE.md`) — mission and principles slots are
   unfilled template placeholders (`{{double braces}}`); bootstrap has not run. Core rules
   in effect: session protocol (read CLAUDE.md + STATE.md + input manifest only; work on
   own branch; no `git stash`; commit before ending; treat conversation as disposable);
   the five-role artifact chain (Consulted → Author → Challenger → Approver → Consumer);
   governance (agents branch and PR only, never push to main); single-principal disclosure
   (Intent Owner and Engineering Lead are one person, no independent review at this stage).
   Advisory rules still pending checks (E2, E6, E4, E8, E12). The Steward is explicitly
   described: "Holds no artifact seat. On any artifact, the author, challenger and approver
   are three different seats on three different holders. Check SEATS refuses anything else."

2. **STATE.md** (`/STATE.md`) — cycle 1, setup phase. `active_tracks: []`. No open
   decisions. No mid-task work. Product description field is empty (bootstrap has not run).

3. **docs/roles.yml** — full seat roster read. Steward seat at lines 201–219. All other
   seats read. `holders` section lists Agent E as the Steward.

4. **docs/enforcement.yml** — full enforcement registry read. E3, E9, E10, E11, E14, E15,
   E16, E17, DOR, SEATS are implemented or partial. E1, E2, E4, E5, E6, E7, E8, E12, E13
   are planned.

5. **docs/dor/floor.yml** — partial read (first 50 lines). Gates: case, design, plan,
   increment, release. DOR check is implemented.

6. **docs/templates/registry-entry.md** — template for registry entries (RG-NNN); fields:
   type, date, what happened, what was at risk, what caught it, countermeasure, check.

7. **No task input manifest in the repository.** This session received its task via a
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
- The Engineering Lead is my verifier — meaning the same individual who holds both human
  seats is the only party who checks my work. This is noted as a constraint in every
  section where it is material.

---

## 1. My own job (Steward seat)

Source: `docs/roles.yml` lines 201–219. I review each field and say keep or change.

### trigger

> "Each cycle exit; each pull request to a protected branch; a near-miss or an
> unowned-decision failure is reported"

**KEEP with notes.** Three trigger conditions:

1. **Cycle exit** — I audit process adherence for the completed cycle.
2. **Each pull request to a protected branch** — I check compliance before merge.
3. **Near-miss or unowned-decision failure is reported** — I open a registry entry.

**Note 1:** Condition 2 ("each pull request to a protected branch") implies I hold a role
in the merge gate. But my outputs produce only registry entries and process-adherence
audits; there is no named gate-hold mechanism. I can flag a violation, but I have no
stated authority to block a merge pending my audit. The trigger fires, but the procedural
consequence is undefined. See STEWARD gap 1.

**Note 2:** Condition 3 names "a near-miss or unowned-decision failure is reported" without
saying who reports it or through which channel. No seat has a formal output that sends a
near-miss report to me. I discover near-misses through my own audits or through informal
conversation — neither of which is a named artifact channel. See STEWARD gap 2.

**Note 3:** "Unowned-decision failure" is not defined anywhere in CLAUDE.md, roles.yml,
or the DOR floor. A fresh session will not know what constitutes one or how to recognise
it. See STEWARD gap 3.

**Note 4:** The trigger does not fire when Engineering Lead approves an artifact or merges
a PR. Yet I am Engineering Lead's verifier — I must check merge history and approval order.
If that check only happens at cycle exit, violations may accumulate. The trigger may need
a fourth condition: "each time Engineering Lead signs or merges." See STEWARD gap 4.

---

### inputs

| # | Artifact | From | Decision |
|---|---|---|---|
| 1 | review | Verifier | **KEEP with concern** — I use Verifier's reviews to check that every approved artifact has a review file beside it, findings are answered item by item, and no session authored and challenged the same artifact (my evidence items for verifying Verifier). But Verifier's outputs list review for Product and for Architect, not for Steward. I list it as an input; Verifier does not list me as a consumer. One-sided. See STEWARD gap 5. |
| 2 | delivery-system | Delivery | **KEEP** — I use it to audit cadence, track cap, story template at cycle exit. Delivery sends it to me and I list it as an input. Consistent. |
| 3 | cicd | Operator | **KEEP with concern** — I use it to audit gate structure and smoke-cycle compliance. But Operator's outputs list cicd for Builder only. I list it as an input; Operator does not list me as a consumer. One-sided. See STEWARD gap 6. |

**Missing input 4 — access to all approved artifacts:** My audit scope covers every
artifact in the repository: approval order, E10 front-matter compliance, SEATS seat
separation, DOR completeness, registry integrity (E11). None of these checks are performed
on just three named inputs. The three listed inputs capture my formal artifact receipts but
not the full read scope my role requires. My job is repository-wide; my inputs list three
artifacts. This is an intent gap: inputs should either be expanded or explicitly noted as
"named receipts; audit reads all artifacts from the repository." See STEWARD gap 7.

**Missing input 5 — near-miss reports from any seat:** My trigger fires when "a near-miss
is reported," but no seat has a formal output that sends near-miss reports to me. I need a
named input channel — either a near-miss report artifact type or a formal escalation
mechanism — so a fresh session knows where to look. See STEWARD gap 2.

---

### value

> "Audits whether the process was followed and keeps the registry. Holds no seat on any
> artifact, so it can judge every seat. Files every near-miss, and the countermeasure is a
> check, never a reminder to be careful"

**KEEP.** This is precise. Three things I do:
1. Audit process compliance — the independence guarantee comes from holding no artifact seat.
2. Keep the registry — every near-miss becomes a registry entry with a check as the
   countermeasure.
3. File every near-miss — "be more careful" is never a countermeasure.

**One structural concern:** The value says "files every near-miss" and "the countermeasure
is a check." But I do not design or implement checks — that is Engineering Lead's domain
(Engineering Lead approves the check after receiving my registry entry). My job is to
identify the near-miss and propose a countermeasure; the Engineering Lead decides whether
the proposed check ships. The value statement elides this approval step, making it read as
though I both file and resolve near-misses. In practice, my registry entry proposes a check
and the Engineering Lead approves or redirects it. See STEWARD gap 8.

---

### outputs

| # | Artifact | For | Decision |
|---|---|---|---|
| 1 | registry entry | Engineering Lead | **KEEP** — Registry entries capture near-misses with hazard class, cause and proposed countermeasure check. E11 (partially implemented) verifies registry integrity. Engineering Lead receives it and decides whether the countermeasure check ships. |
| 2 | audit of process adherence | Delivery | **KEEP with concern** — Delivery uses this audit to improve its process (Delivery's job lists it as an input). But see below. |

**Missing output 3 — audit of process adherence for Engineering Lead:** Engineering Lead's
verifier evidence says "the Engineering Lead's spot reads of audit records at each cycle
exit." Audit records are records of my audit output. My outputs list Delivery as the sole
consumer of the audit. Engineering Lead must also receive the audit (or a summary) to
perform those spot reads. My outputs are incomplete. See STEWARD gap 9.

**Missing output 4 — registry entry for Delivery:** When the near-miss involves a process
deviation in Delivery's domain (cadence, track cap, story template), Delivery should
receive the registry entry that names the countermeasure. My outputs list Engineering Lead
as the sole consumer of registry entries. See STEWARD gap 10.

**No template for output 2:** The registry-entry template exists; the audit-of-process-
adherence artifact has only an acceptance criterion ("Names each deviation with the file or
check result that shows it") and no template. A fresh session will produce an inconsistent
format. See STEWARD gap 11.

---

### standards

`docs/enforcement.yml`, `docs/dor/floor.yml`

**KEEP with two gaps.**

Both are necessary:
- `enforcement.yml` — tells me which checks are implemented (hard gates I can cite
  definitively) versus planned (advisory I must note as such). Essential for the audit.
- `floor.yml` — tells me which DOR rows apply at each gate and which checks enforce them.
  Essential for the gate-compliance audit.

**Missing standard — `docs/artifact-types.yml`:** I audit artifact naming, location and
front-matter completeness. Artifact types define the naming prefix, directory location and
human-approver requirement for every artifact. Without it in my standards, a fresh Steward
session auditing location and naming has no authoritative reference. See STEWARD gap 12.

**Missing standard — `docs/roles.yml`:** I verify seat separation (SEATS check), seat
holder assignments and incompatible pairs. The roles file is my authoritative source for
this audit. It is not listed in my standards even though it is the primary document I must
consult. See STEWARD gap 12.

---

### templates

`docs/templates/registry-entry.md`

**KEEP with one gap.** The registry-entry template is complete (type, date, what happened,
what was at risk, what caught it, countermeasure, check). Correctly chosen.

**Missing template — `audit-of-process-adherence`:** My second output has no template. A
fresh session auditing the cycle will produce an ad-hoc format, making it harder for
Engineering Lead to spot-read consistently and for Delivery to respond systematically.
Proposed fix: add `docs/templates/audit-of-process-adherence.md` to my templates.
See STEWARD gap 11.

---

### verifier

Seat: Engineering Lead.
Evidence: "Registry integrity (E11); the Engineering Lead's spot reads of audit records at
each cycle exit"

**KEEP with significant concerns.**

1. **Engineering Lead is a human seat AND my verifier.** The same person who holds Intent
   Owner and Engineering Lead is the only party who verifies my work. There is no agent
   seat that cross-checks my audits independently. In a system designed so that every
   artifact has a challenger distinct from its author, the Steward's work has only informal
   verification ("spot reads"). This is the weakest verification relationship in the roster.
   See STEWARD gap 13.

2. **"Spot reads" is informal.** No named frequency, sample size, or pass criterion is
   specified for Engineering Lead's spot reads. The evidence cannot be reproduced
   independently; it rests on Engineering Lead's judgment alone. Compare: every other seat's
   verifier evidence names a check identifier or a file-level artifact (e.g., "a review file
   beside each artifact, answered item by item (E10)"). My verifier evidence does not. See
   STEWARD gap 13.

3. **E11 is partially implemented.** E11 currently checks registry integrity (check
   exists; has the required fields). It does not yet verify that non-required CI jobs are
   healthy. The "non-required job health ships with E6" (planned). Until E11 and E6 are
   fully implemented, registry integrity is only structurally checked, not substantively.

4. **Mutual verification:** I am the verifier for Engineering Lead (their verifier names
   me and specifies what I check: merge history, roles-file changes against approved
   proposals). Engineering Lead is my verifier. We mutually verify each other. This is not
   explicitly prohibited, but it creates a loop: if I fail in my duty, my verifier
   (Engineering Lead) has no independent signal that my audit was incomplete. A third party
   is absent by design (single-principal disclosure). See STEWARD gap 13.

---

### qualified_layers

The Steward seat has no `qualified_layers` field. CLAUDE.md says "Holds no artifact seat."
The SEATS check enforces this. No layer qualification is listed or needed.

**Concern:** If a future project adds layers and the SEATS check enforces that every layer
has a qualified author and challenger, the Steward must never be named as author or
challenger of any layer. The absence of `qualified_layers` is correct and should be
preserved.

---

### What I cannot do as written

1. Block a pull request to a protected branch — I trigger on PRs but have no named
   gate-hold mechanism. I can produce an audit finding; I cannot enforce a hold.
2. Receive near-miss reports through a named artifact channel — no seat outputs a near-miss
   report to me; I discover them through my own audit or informally.
3. Know what "unowned-decision failure" means — the term is in my trigger but undefined.
4. Audit all artifacts systematically using only my three listed inputs — my audit scope
   is repository-wide; my inputs list three artifacts.
5. Produce a consistently formatted audit of process adherence — no template exists.
6. Propose and approve a countermeasure check in one step — I propose; Engineering Lead
   approves. The value statement elides this step.
7. Name the specific frequency or scope for Engineering Lead's spot reads of my work — the
   verifier evidence is "spot reads at cycle exit," which is informal and unreproducible.

---

### What I would refuse to accept as input

1. A near-miss report that proposes "be more careful" as a countermeasure — the value
   statement is explicit: "the countermeasure is a check, never a reminder to be careful."
   I would return it and require a redesign.
2. A request to hold an artifact seat — I am `holds_no_artifact_seat: true`; accepting
   any authorship, challenge or approval role on an artifact would immediately compromise
   my independence as the process auditor.
3. An artifact whose audit I am asked to perform on behalf of the same session that wrote
   it — self-audit is the exact problem my independence is designed to prevent.
4. A registry entry that lacks a hazard class, cause, and a check (existing or proposed)
   as the countermeasure — the acceptance test for my output 1 requires all three; an
   incomplete entry fails E11.
5. An instruction to let a gate pass without verifying the evidence it requires — my role
   is to audit whether the process was followed, not to waive requirements on request.
6. Any task delivered without a formal artifact channel (informal conversation requests)
   unless this is explicitly a dryrun bootstrap task — "a decision counts only once it is
   written to a named artifact in the repository" (CLAUDE.md §3).

---

## 2. The other seats

### Intent Owner

**Recommendation: Accept with conditions**

*What I hand to them:* Nothing formally. Registry entries go to Engineering Lead; audits
go to Delivery. Intent Owner does not appear in my outputs.

*What I take from them:* Nothing directly. Intent Owner does not appear in my inputs.

*Overlap:* None. Intent Owner judges business worth; I audit process compliance.

*Conditions:*
1. **I am Intent Owner's verifier.** Intent Owner's verifier names "Steward" with evidence:
   "Approval order and approved_at on every artifact this seat signs (E10); case-gate rows
   it judges are met in docs/dor/checklist.yml (DOR)." To perform this check, I need to
   read Intent Owner's signed artifacts from the repository. This is not captured in my
   formal inputs; I read the repository directly (STEWARD gap 7).
2. Intent Owner does not directly send me any artifact, yet I am responsible for checking
   their work. The audit is pull-based (I read the repository), not push-based (Intent
   Owner does not send me anything). This is the intended design but leaves the audit
   dependent on me knowing when to look.

*Wiring check:* Intent Owner's verifier names Steward. My inputs do not list Intent Owner
as a sender. The relationship is auditor-to-audited, not artifact-push. No wiring conflict,
but the pull-based audit scope is not stated in my inputs.

---

### Engineering Lead

**Recommendation: Accept with conditions**

*What I hand to them:* `registry entry` (my output 1). Engineering Lead decides whether
the countermeasure check ships (their charter: "approves or declines role proposals, with
docs/roles.yml changes"). The registry-entry acceptance test says the Engineering Lead
receives it; they are the designated approver.

*What I take from them:* Nothing formally. But Engineering Lead is my verifier; their
spot reads of my audit records are the evidence. There is no input artifact channel between
us in either direction — only Engineering Lead reading my outputs and judging their quality.

*Overlap:* I am Engineering Lead's verifier and Engineering Lead is my verifier.
This mutual relationship is the most significant governance constraint on my seat. Neither
of us can credibly claim independent review of the other without a third party, and at this
governance stage no third party is available.

*Conditions:*
1. The mutual-verification loop must be acknowledged as a known governance limitation.
   Until a third seat (or an agent session with a separate holder) can verify one or both
   of us independently, the loop is an accepted risk under single-principal disclosure.
2. Add Engineering Lead as a second consumer of the "audit of process adherence" output to
   match the verifier evidence ("Engineering Lead's spot reads of audit records"). See
   STEWARD gap 9.
3. I must be clear that Engineering Lead approves registry entries — they are not self-
   approving. The E11 check verifies structure; Engineering Lead approves disposition.

*Wiring check:* Engineering Lead's inputs list "approved or declined role proposals, with
docs/roles.yml changes, for Steward" (their output 2). My inputs do not list Engineering
Lead as a sender of anything. One-sided: Engineering Lead sends approved role proposals to
me (but I have no input for them). I should add `{artifact: approved-role-proposal, from:
Engineering Lead}` to my inputs if I am expected to act on them. See STEWARD gap 14.

---

### Product

**Recommendation: Accept with conditions**

*What I hand to them:* Nothing directly. My audit may name Product artifacts as non-
compliant, but the audit goes to Delivery (and Engineering Lead, if STEWARD gap 9 is
fixed), not to Product.

*What I take from them:* Nothing. Product does not appear in my inputs.

*Overlap:* None. Product owns use cases; I audit process compliance.

*Conditions:*
1. Product's verifier is Verifier (not Steward). My audit of Product's artifacts is
   indirect — I check that a Verifier review file exists beside each Product artifact,
   that findings are answered, and that the same session did not author and review the
   same artifact (SEATS). I need the review files (Verifier's output) to do this check,
   but my formal input 1 is "review from Verifier" — which covers this, if the wiring gap
   is resolved.

*Wiring check:* No formal artifact exchange between Product and Steward. My audit is pull-
based. No wiring conflict.

---

### Delivery

**Recommendation: Accept with conditions**

*What I hand to them:* `audit of process adherence` (my output 2). Delivery uses it to
improve cadence, track cap compliance and story template use.

*What I take from them:* `delivery-system` (my input 2). I use it to know what the
agreed cadence, track cap and story template are before I audit against them.

*Overlap:* Delivery's verifier is Steward. I audit: "Cadence, track cap (E9) and story
template use audited at each cycle exit; metrics recomputed from the repository, never
self-reported." This is consistent with my trigger (cycle exit) and my input 2.

*Conditions:*
1. My audit of Delivery requires comparing the actual repository state (metrics from git)
   against the delivery-system's stated standards. "Metrics recomputed from the repository"
   implies I run computations, not just read files. No tool or script is named for this.
   A fresh Steward session will need to derive metrics from git history manually. See
   STEWARD gap 15.
2. Delivery's verifier evidence says metrics are "never self-reported." I enforce this rule;
   but if Delivery has not committed a delivery-system artifact before I audit, I have
   nothing to audit against. My trigger fires at cycle exit, which may be after Delivery's
   audit window. Sequencing is not specified.

*Wiring check:* Delivery sends me `delivery-system` — consistent with my input 2. I send
`audit of process adherence` to Delivery — consistent with my output 2. CLEAN. Best-wired
relationship in my job.

---

### Architect

**Recommendation: Accept**

*What I hand to them:* Nothing directly. My audit may name Architect artifacts as non-
compliant, but audit results go to Delivery (and Engineering Lead via gap fix).

*What I take from them:* Nothing. Architect does not appear in my inputs.

*Overlap:* None. I do not hold an artifact seat; I cannot challenge Architect's design.
My role is to verify that the process around Architect's artifacts was followed: that a
review file exists, findings are answered, the reviewer qualified for the layer (D6), and
the reviewer was a different session.

*Conditions:*
1. Architect's verifier is Verifier. My audit checks that the Verifier review exists and
   the SEATS check was satisfied. No direct artifact exchange is needed.

*Wiring check:* No formal artifact exchange between Architect and Steward. Pull-based
audit. No wiring conflict.

---

### Designer

**Recommendation: Accept**

*What I hand to them:* Nothing directly.

*What I take from them:* Nothing. Designer does not appear in my inputs.

*Overlap:* None. Designer owns UX; I audit process compliance around Designer's artifacts.

*Conditions:*
1. Designer's verifier is Verifier. My audit verifies review presence, findings answered,
   and session independence. Pull-based.

*Wiring check:* Clean. No formal artifact exchange.

---

### Verifier

**Recommendation: Accept with conditions**

*What I hand to them:* Nothing formally. My audit of Verifier's work is the evidence in
Verifier's verifier field, but I produce that evidence in my audit output, not as a named
artifact sent to Verifier.

*What I take from them:* `review` (my input 1). I read review files to check that each
approved artifact has one, findings are answered, and sessions are independent.

*Overlap:* I am Verifier's verifier. My evidence items: "A review file beside each
approved artifact, answered item by item (E10); no session authored and challenged the
same artifact (SEATS)." The SEATS check (implemented) and E10 (partial) support this audit.

*Conditions:*
1. Verifier's outputs list review for Product and for Architect. Neither lists Steward as
   a consumer. I list review from Verifier as my input 1. One-sided: Verifier does not
   name me as a consumer of its review files. Proposed fix: add Steward as a consumer of
   review in Verifier's outputs, or clarify that Steward reads review files from the
   repository (pull-based), not from a push delivery. See STEWARD gap 5.
2. Verifier's outputs do not list review for Builder (noted in both Builder and Operator
   reviews). If I am checking that every Builder artifact has a review file, and that file
   is absent from Verifier's outputs, a fresh Verifier session may not produce one. My
   audit would then report a deviation where the root cause is a wiring gap, not a process
   failure.

*Wiring check:* I list `review from Verifier` as input 1 — Verifier does not list Steward
as consumer; one-sided gap. The gap is real but the practical impact is lower than for
direct artifact delivery, since review files exist in the repository regardless of who is
named as consumer.

---

### Builder

**Recommendation: Accept**

*What I hand to them:* Nothing directly.

*What I take from them:* Nothing. Builder does not appear in my inputs.

*Overlap:* None. Builder's verifier is Verifier. My role is to verify that Verifier
reviewed Builder's work (session independence, review file present, E10 compliance, E3
no-op test lint, E15 append-only migrations). I check the audit trail from the repository.

*Conditions:*
1. I do not evaluate whether Builder's ADRs are sound — that is Architect's concern. I
   check that an ADR exists for each new dependency (floor I3). I can confirm presence;
   I cannot judge quality.
2. I audit that E15 (append-only migrations, implemented) passes on Builder's PRs. This is
   a hard check; any failure blocks the PR. My audit after the fact confirms the check ran
   and passed.

*Wiring check:* No formal artifact exchange between Builder and Steward. Pull-based audit.
No wiring conflict.

---

### Operator

**Recommendation: Accept with conditions**

*What I hand to them:* Nothing directly.

*What I take from them:* `cicd` (my input 3). I use it to audit gate structure and
verify the smoke-cycle record in `docs/archive`.

*Overlap:* None directly. Operator's verifier is Verifier. I audit that Verifier reviewed
Operator's artifacts and that the smoke-cycle record exists in the named location.

*Conditions:*
1. Operator's outputs list `cicd` for Builder only; Steward (and Verifier, Engineering
   Lead) are not listed as consumers. I list it as my input 3; Operator does not list me
   as a consumer. One-sided. See STEWARD gap 6. (Both Builder and Operator reviews
   flagged that `cicd` consumers are under-stated in Operator's outputs.)
2. The smoke-cycle record has no template or naming convention (noted in OPERATOR gap 9).
   My audit requires finding it in `docs/archive`; without a naming convention, I may miss
   it or find stale records. If the Operator review's proposed fix (a `smoke-cycle-record.md`
   template and naming convention) is adopted, my audit procedure becomes deterministic.

*Wiring check:* I list `cicd from Operator` as input 3 — Operator lists cicd for Builder
only; one-sided gap. Proposed fix: add Steward as a consumer of cicd in Operator's outputs.

---

## 3. Help protocol

### What I offer each seat and when

| Seat | What I offer | When |
|---|---|---|
| Intent Owner | A verifier check: approval order and approved_at on their signed artifacts; case-gate DOR rows verified in docs/dor/checklist.yml | At each cycle exit; when my trigger fires on a PR to a protected branch that includes Intent Owner's signatures |
| Engineering Lead | Registry entries naming near-misses with proposed countermeasure checks; audit of process adherence (if gap fix is adopted); verification that merge history shows human merges and roles-file changes match approved proposals | At each cycle exit; when a near-miss or unowned-decision failure fires my trigger |
| Product | Nothing directly; my audit findings that name Product artifacts go into the audit of process adherence (Delivery receives it) | At cycle exit |
| Delivery | Audit of process adherence: cadence, track cap, story template use, metrics from the repository | At each cycle exit |
| Architect | Nothing directly; my audit findings for Architect artifacts appear in the audit of process adherence | At cycle exit |
| Designer | Nothing directly; same as Architect | At cycle exit |
| Verifier | Nothing directly; I check Verifier's work (review files present, findings answered, sessions independent) and the outcome appears in the audit | At cycle exit |
| Builder | Nothing directly; my audit confirms ADRs exist, no blanket skips, migrations append-only | At cycle exit |
| Operator | Nothing directly; my audit confirms cicd is in the repository, smoke-cycle record exists in docs/archive | At cycle exit; when my trigger fires on a deployment PR |

### What I ask of each seat, where I write the request, and how long I wait

| Seat | What I ask | Where I write the request | Wait limit | Escalate to |
|---|---|---|---|---|
| Verifier | Review files for every approved artifact (so I can check E10 and SEATS compliance) | If a review file is absent, I record the deviation in my audit of process adherence; I do not wait — I record the gap and report | None — I record absence as a deviation, I do not block on Verifier | Engineering Lead (via registry entry if the gap is systemic) |
| Delivery | A committed delivery-system artifact before cycle exit, so I have a standard to audit against | If absent, I record an open decision in STATE.md; I note it as a process deviation | One cycle | Engineering Lead (via STATE.md open decision; registry entry if recurring) |
| Operator | Smoke-cycle record in docs/archive naming the cycle and date | If absent, I record the deviation in the audit of process adherence | One cycle | Engineering Lead (via registry entry) |
| Engineering Lead | Approval of my registry entries; acknowledgment of audit findings at cycle exit | Registry entry front matter (approval status); STATE.md open decisions if entries are unacknowledged | One cycle; both human seats are one person, so no further escalation authority | STATE.md open decision; note governance limitation — no independent authority exists at this stage |

---

## 4. Authority

### What I decide alone

- Whether a registry entry has a hazard class, cause and a countermeasure that names
  a check — I judge completeness before filing
- Whether an audit deviation is significant enough to rise to a registry entry versus a
  routine audit note
- Whether a Verifier review file is present and findings are answered item by item —
  I count open findings from the artifact's front matter, not from conversation
- Whether the same holder authored and challenged the same artifact — I check the SEATS
  check output and the front-matter seats fields
- Whether a migration was edited after merge — E15 (implemented) tells me definitively;
  I report its result
- Whether metrics in the audit come from the repository, not from self-reports — I compute
  them from git history myself

### What I decide only after consulting

| Decision | Consult | Reason |
|---|---|---|
| Whether a near-miss rises to a proposed check that changes docs/roles.yml | Engineering Lead | A roles-file change requires an approved role proposal (E17); I cannot propose one alone |
| Whether a gate deviation constitutes a process failure requiring a hold | Engineering Lead | I have no blocking authority on a PR; only Engineering Lead can hold a merge, and only they can decide the severity of a compliance gap at this governance stage |
| Whether a pattern of deviations means a process rule needs to change | Engineering Lead | Changing standing documents (CLAUDE.md rules, the DOR floor) requires Engineering Lead approval; I identify the pattern and propose the change |
| Whether an "unowned-decision failure" has occurred | Engineering Lead | The term is undefined (STEWARD gap 3); until a definition is established, I must consult before filing a registry entry under that category |

### When I ask before acting

- Before filing a registry entry: confirm that the hazard class, cause and proposed check
  are substantive — "be more careful" is not a countermeasure
- Before closing an audit cycle: confirm that my audit covered all active artifacts in the
  cycle, not only the three formally listed in my inputs
- Before marking a gate as compliant: confirm that the required check ran and passed (or
  is advisory with its status noted) — I do not accept an artifact author's assertion that
  a check passed

### What I would refuse

- Holding any artifact seat — "holds_no_artifact_seat: true" is fundamental to my
  independence; accepting even one authorship or approval role invalidates my audit
- Filing a registry entry with "be more careful" as the countermeasure
- Declaring a PR compliant without reading the relevant artifact files from the repository
- Self-auditing any work I produced in the current session — I produce audits and registry
  entries, but I cannot verify my own outputs; only Engineering Lead can (the verifier
  field names them)
- Acting on an informal near-miss report that has not been written to a named artifact
  in the repository — per CLAUDE.md §3, decisions count only when written
- Ignoring a SEATS violation because the check is partial — E10 (partial), SEATS
  (implemented): I report the violation regardless of whether the check caught it, because
  the check may have incomplete coverage

### Where the procedure left me less room than my job description implies

1. **No merge-blocking authority.** My trigger fires on every PR to a protected branch,
   but I have no stated mechanism to hold a PR pending my audit. My output is an audit
   record; the merge decision belongs to Engineering Lead. My "gate" role is therefore
   advisory unless Engineering Lead has committed to waiting for my audit before merging.
   This is not stated anywhere.

2. **Audit scope is repository-wide but inputs are three artifacts.** My job implies I
   check everything; my inputs list three artifacts. In practice I read the repository
   directly, but this is a design intent gap: a fresh session reading my job description
   literally would audit only three artifacts.

3. **No procedure for an "unowned-decision failure."** The term appears in my trigger
   but is undefined. I cannot act on a trigger condition I cannot recognise.

4. **My verifier is the same person I verify.** Engineering Lead is my verifier; I am
   Engineering Lead's verifier. At this governance stage this loop is unavoidable (single-
   principal disclosure), but it means my work has no independent external check.

5. **Near-miss discovery is informal.** I file "every near-miss," but the channel by which
   near-misses reach me is undefined. I must discover them from my own audit — reactive,
   not proactive — or rely on informal conversation, which is explicitly disposable
   (CLAUDE.md §3).

---

## 5. Guessing log

Every point where the procedure left me without a clear answer.
STEWARD = a gap in my own job description or the wiring to/from it.
METHOD = a gap in the process design visible from my seat.
PRODUCT = a gap in the product itself (unfilled template slots, missing definitions).

| Label | Description |
|---|---|
| STEWARD gap 1 | **No merge-blocking mechanism stated.** My trigger fires on each PR to a protected branch, but my outputs do not include a gate-hold artifact or approval. I can audit; I cannot block. A fresh Steward session receiving a PR will not know whether to comment, block, or only report. Proposed fix: define a "compliance hold" output or state explicitly that Steward's audit is advisory and Engineering Lead decides whether to proceed. |
| STEWARD gap 2 | **No named channel for near-miss reports.** My trigger fires when "a near-miss is reported," but no seat has a formal output that sends a near-miss report to Steward. The only way I discover near-misses is through my own audit or informal conversation. Proposed fix: add a near-miss report artifact type (or a designated STATE.md section) and name it as a formal output in any seat that may observe one, with Steward as the consumer. |
| STEWARD gap 3 | **"Unowned-decision failure" undefined.** This term appears in my trigger but is not defined in CLAUDE.md, roles.yml or the DOR floor. A fresh session will not know what constitutes one or how to respond. Proposed fix: define the term in CLAUDE.md or docs/artifact-types.yml; add a template for the resulting artifact. |
| STEWARD gap 4 | **Trigger does not fire on Engineering Lead approvals or merges.** I am Engineering Lead's verifier; my evidence includes checking merge history. But my trigger only fires at cycle exit and on PRs. If Engineering Lead merges a PR without my check, I cannot catch the violation until cycle exit. Proposed fix: add "Engineering Lead merges to a protected branch" as a trigger condition, or note that the post-merge audit at cycle exit is the intended timing. |
| STEWARD gap 5 | **Verifier does not list Steward as a consumer of review.** I list `{artifact: review, from: Verifier}` as my input 1. Verifier's outputs list review for Product and for Architect; Steward is not listed. One-sided. Proposed fix: either add Steward as a consumer of review in Verifier's outputs, or document that Steward reads review files from the repository (pull-based) and update my inputs to reflect this. |
| STEWARD gap 6 | **Operator's cicd output does not list Steward as consumer.** I list `{artifact: cicd, from: Operator}` as my input 3. Operator's outputs list cicd for Builder only. The Builder and Operator reviews (BUILDER gap 7 / OPERATOR gap 7) flagged that Engineering Lead, Verifier and Steward all receive cicd. Proposed fix: add Steward (along with Engineering Lead and Verifier) as additional consumers of cicd in Operator's outputs. |
| STEWARD gap 7 | **Audit scope is repository-wide but inputs list three artifacts.** My job requires me to check every approved artifact's front matter (E10), seat separation (SEATS), DOR completeness (DOR), registry integrity (E11), and merge history. My inputs list only three named artifacts (review, delivery-system, cicd). A fresh Steward session reading only the inputs list would audit three artifacts and miss everything else. Proposed fix: add a note in my inputs: "Steward reads all committed artifacts from the repository; the three listed inputs are formally received; audit scope is repository-wide." |
| STEWARD gap 8 | **Value statement says "files every near-miss" implying resolution, not just proposal.** The value elides the Engineering Lead approval step. I file a registry entry with a proposed check; Engineering Lead decides whether the check ships. A fresh session may believe it has authority to close a near-miss by filing an entry alone. Proposed fix: update the value statement to: "Files every near-miss as a registry entry with a proposed check; the countermeasure ships when Engineering Lead approves it." |
| STEWARD gap 9 | **"Audit of process adherence" goes to Delivery only; Engineering Lead needs it for spot reads.** My output 2 names Delivery as the sole consumer. But Engineering Lead's verifier evidence says "Engineering Lead's spot reads of audit records at each cycle exit." Engineering Lead must also receive the audit. Proposed fix: add Engineering Lead as a second consumer of "audit of process adherence." |
| STEWARD gap 10 | **Registry entries go to Engineering Lead only; Delivery should receive entries affecting its domain.** When a near-miss involves a Delivery process deviation, Delivery should receive the registry entry (or a reference to it) so it can act on the countermeasure. Proposed fix: add Delivery as a conditional consumer of registry entries (when the hazard class covers delivery-process failures). |
| STEWARD gap 11 | **No template for "audit of process adherence."** My second output has only an acceptance criterion, not a template. A fresh session will produce an inconsistent format, making Engineering Lead's spot reads harder and Delivery's response less systematic. Proposed fix: add `docs/templates/audit-of-process-adherence.md` with required sections: cycle, artifacts audited, deviations found (file, check, result), open items, and metrics computed from the repository. |
| STEWARD gap 12 | **`docs/artifact-types.yml` and `docs/roles.yml` absent from my standards.** I audit naming, location and front-matter completeness (artifact-types.yml) and seat assignments, incompatible pairs and holder qualifications (roles.yml). Neither is in my standards list. Proposed fix: add both to my standards. |
| STEWARD gap 13 | **Mutual verification loop with Engineering Lead and informal verifier evidence.** I verify Engineering Lead; Engineering Lead verifies me. "Spot reads" is not reproducible or formally evidenced. No third party exists at this governance stage. This is the most serious governance limitation on my seat. Proposed fix (long-term): introduce a cross-session Steward audit mechanism (a scheduled agent run independent of Engineering Lead's sessions) whose output is filed as a durable artifact. Until E1 ships and identities are bound, this is aspirational. |
| STEWARD gap 14 | **No input for Engineering Lead's approved role proposals.** Engineering Lead's outputs include "approved or declined role proposals, with docs/roles.yml changes, for Steward." I have no input for this. If an approved role proposal changes the roster, I need to know so my next audit checks the updated seats. Proposed fix: add `{artifact: approved-role-proposal, from: Engineering Lead}` to my inputs. |
| STEWARD gap 15 | **No tool or script named for computing delivery metrics from the repository.** Delivery's verifier evidence says metrics must be "recomputed from the repository, never self-reported." I am the verifier. But no tool, script or formula is named. A fresh Steward session will derive metrics differently from the previous one, making the audit non-reproducible. Proposed fix: add a metrics computation script to `tools/checks/` or document the formula (e.g., cycle time computed from first commit on an increment branch to merge date) in a standards document. |
| METHOD gap 1 | **No procedure for a Steward that discovers a violation during a cycle (not at exit).** My trigger fires at cycle exit and on PRs. If I discover a near-miss during routine reading between those events (not part of a formal audit trigger), I have no stated procedure for when and how to raise it. In practice I would file a registry entry immediately, but "a decision counts only once it is written to a named artifact." Without a trigger, I have no authority to act. Proposed fix: add "a violation is discovered by Steward during repository review" as a fourth trigger condition. |
| METHOD gap 2 | **`[Builder, Operator]` not in `incompatible_pairs`.** Both Builder and Operator reviews (BUILDER gap 15, OPERATOR gap 2, METHOD gap 2) flagged this. From my seat, if the same holder designs the CI/CD gates and implements the code that must pass them, no audit I perform can detect gate lowering before it happens — only after the merge. The separation is a structural protection that no post-hoc audit fully replaces. I endorse the proposed fix: add `[Builder, Operator]` to `incompatible_pairs`. |
| METHOD gap 3 | **Single-principal disclosure weakens every gate at this governance stage.** Intent Owner and Engineering Lead are one person. My outputs go to Engineering Lead; my verifier is Engineering Lead. The same person who reviews my work also holds the only human approval seats. Every gate check that requires a human is held by the same individual. No process change I can recommend within the current roster fixes this; it is an accepted governance limitation until E1 ships and additional holders are added. I note it here so a future Steward is not surprised. |
| PRODUCT gap 1 | **Task delivered via conversation prompt, not input manifest.** Per CLAUDE.md §3, decisions count only once written to a named artifact. This review is the first durable artifact produced by this session. The divergence is acceptable for a dryrun bootstrap task; in production, the task manifest would be the authoritative input. |
| PRODUCT gap 2 | **Bootstrap has not run.** CLAUDE.md contains unfilled `{{double braces}}` slots: mission, principles and seat holder names. STATE.md product description is empty. Without a completed bootstrap, the project's principles for trade-off decisions and the actual holder identities are unknown. My audits at this stage cannot fully check that holder names match across CLAUDE.md, docs/roles.yml and artifact front matter, because the name substitution has not happened. |
