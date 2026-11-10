# Workplan: Matters Arising from brawlaphant (Brandon Kelly / Eco Wealth): vision and contributions

**Prepared:** 2026-11-10 · **For:** Gregory Landua (RND) · **Status:** draft for human review. No agent in this plan merges, posts, or submits anything on its own (see §6 Guardrails).

---

## 1. Quick summary

- **Who.** `brawlaphant` is Brandon Kelly, who works through Eco Wealth / Eco Wealth Safety in LA. He has the most commits in `regen-network/agentic-tokenomics`: 87 of 226. He has attended the $REGEN Tokenomics WG since mid-2025 and sometimes hosts it.
- **Contribution.** Between Feb and Apr 2026 he wrote:
  - CosmWasm contracts for M001-ENH and M008–M015
  - cadCAD simulations for M012–M015
  - AGENT-001…004 character definitions and runtimes
  - governance drafts for the 7 NEEDS_GOVERNANCE questions
  - PoA triage, test vectors, and the CI repairs
  - RFC-0001, the first RFC filed under the new process

  Gregory merged most of it in large batches on Mar 25, Apr 10, and Apr 25.
- **What is stuck.** At least 3 PRs are probably open: regen-network/agentic-tokenomics#108, #111, and #112. Another ~10 are unmerged with unknown status. RFC-0001 has no human sponsor. Brandon has said three times on the record that he is "waiting for maintainers to decide direction" or needs "someone to write out the plan".
- **Quality.** The merged contracts are labelled "v0 advisory", but they contain real defects. Two were confirmed by hand:
  - The fee-router credits pools without receiving funds.
  - The service-escrow pays out more than was deposited.
- **Coherence.** Merged docs give four different M013 fee splits. The governance drafts cite a 221M cap, which is below current supply of about 239.8M. The `dynamic-supply` contract cannot be instantiated in that state.
- **Unkept promises (RND side).** Several commitments to Brandon are still open:
  - the Oct 6 forum post on the data module, anchoring, the claims engine, and a repo map
  - the claims-engine contributor-group invite
  - the Jun 2 Foundation pitch
  - the Jan 13 Eliza onboarding
- **Strategic tension.** Part of Brandon's vision is agent "users" that accumulate and trade REGEN to absorb sell pressure. He has called the retirement-driven transactions "essentially wash trading". That carries market-integrity and regulatory risk, and RND should not endorse it or encode it in the repo. His labour-verification and "ecological work" vision fits the claims engine and VSH closely.

**The core decision.** Gregory needs to decide how RND relates to a high-velocity outside contributor whom RND cannot review fast enough. The recommended answer, in §5, is to formalise a scoped co-maintainer lane and redirect his energy to the claims engine and VSH. The multi-agent workflow (§4) exists to clear the backlog and prepare that decision. It does not replace the decision.

---

## 2. Sources and coverage

| Source | Coverage | Gaps / confidence |
|---|---|---|
| Git history of `regen-network/agentic-tokenomics` (226 commits). All PR heads #1–#112 fetched anonymously and diffed against `main`. | Full | The GitHub API was blocked for the upstream repo, so PR open/closed state, review comments, issues, and CI results were **inferred, not read**. "Probably open" means the PR still has a `refs/pull/N/merge` ref. |
| Contract source (static read) | All 10 crates | Not executed. Two findings were confirmed by hand (§3, MA-02). The rest were seen in code but not run. |
| Otter transcripts, 2025 Tokenomics WG | 10 meetings, Jun 24 to Dec 9 2025 | Read in full. Otter's speaker labels are sometimes wrong. |
| Otter transcripts, 2026 Tokenomics WG | 13 meetings, Jan 13 to Jun 2 2026 | Read in full. The WG went quiet after Jun 9 2026. |
| Otter, "Brandon, Gregory, Dave" 1:1 | Oct 6 2026 | Read in full. This is the most recent primary source. |
| forum.regen.network | **Blocked by the session network policy** | Only search-engine snippets were available. Topics #602, #616, #617, #618, #567, and #19 were identified, but their authorship and content are **unverified**. |
| Regen Ledger REST (proposal #79/#80 status) | **Blocked** | Brandon's "#79 = VSH, approved" conflicts with the anchor doc, which lists the VSH credit type as **#75**. Needs verification. |

**Local repo note.** This checkout, `glandua/agentic-tokenomics`, is a stale fork: 5 commits on `main` against 226 upstream. All findings refer to upstream.

---

## 3. What we learned

### 3.1 Brandon's vision, in his own framing (fact unless marked)

| Period | What he was building or saying |
|---|---|
| Jun–Aug 2025 | Hands-on DeFi stewardship. He ran community concentrated-liquidity positions (ETH/REGEN on Base, Osmosis USDC bids about 70% below price). "Everyone can make a token, but very few can create an eco credit." |
| Sep–Dec 2025 | Automation: scheduled posts and transactions, then a Gelato bot, then an hourly "banker bot" DCA. He brought in the Hydrex venue and worked on a registry-first business story with Klima/CFC as a demand channel. He drafted the Commons proposal to Monty. |
| Jan–Mar 2026 | "Push the intelligence… before engineering has time": AI-generated specs ready for engineers. His proposals in this period: <ul><li>an economic-reboot framework (supply cap, mint/burn, inflation off)</li><li>quarterly executor reports acknowledged on-chain</li><li>an agent "REGEN ops desk" paid through x402</li></ul> He produced the agentic-tokenomics PR wave. His own diagnosis: "no one has the capacity to absorb what I'm putting out." |
| Apr–Jun 2026 | Agent "spawns" that each make a micro-retirement on every trade. He wants to "print… an army of agents that are only interested in accumulating the coin… offload the sell pressure". He built a Living Building Challenge x402 API, `velf.net` (packets, receipts, simulated proof-of-stewardship credits), and a REGEN Market Monitor agent. He pushed for a Base migration and asked whether the repos are "meant to be full ham." |
| Oct 2026 | An ecological work protocol on Regen and Robinhood Chain that routes funders and labourers to scoped jobs. Hours are verified on Regen Ledger to "anchor the value of money to labour". He is seeking Metro certification for LA construction safety. He experimented with the Verified Stewardship Hour (VSH) and drafted a contribution-pay proposal. He is open to becoming a validator. |

**Through-line (inference).** He wants to replace manual coordination with programmatic, agent-run flows, and to make REGEN the settlement asset for verified ecological labour. The labour-verification thread is closely aligned with RND's claims-engine thesis. The agent-trading thread is not aligned.

### 3.2 Contribution ledger (repo, fact)

- **Merged:**
  - specs and reference implementations hardening M010, M012–M015
  - 10 CosmWasm crates
  - cadCAD M012–M015 with stress scenarios
  - AGENT-003/004 characters and the AGENT-001 CI wiring
  - 7 NEEDS_GOVERNANCE drafts (`docs/governance/needs-governance-proposals.md`)
  - PoA open-questions triage
  - edge-case vectors for M001, M008–M014
  - integration test M013→M012
  - licensing (Apache-2.0 + CC-BY-SA-4.0)
  - CI fix #106
- **Probably open:**
  - #111 RFC-0001: M013 split 28/25/45/2 → 15/30/50/5. Draft, "HUMAN SPONSOR REQUIRED".
  - #112 AGENT-003 market-monitor runtime.
  - #108 earlier RFC-0001 stack, likely redundant with #111/#112.
- **Unmerged, status unknown:**
  - AGENT-004 runtime (#81, #100, #104, #105), never re-filed
  - integrator guides #97/#98 (`docs/integrators/README.md:21-26` still lists them as TODO)
  - M010/M011 coexistence test #101
  - the larger per-contract test suites #72–#76 (for example 51 vs 19 tests for credit-class-voting, 42 vs 7 for attestation-bonding)
  - ToknWrks #68 (321M cap)
- **Recognition gap.** None of this work is discussed by name in any WG meeting. Gregory mentions the repo once (Apr 21).

### 3.3 Commitments ledger

| # | Who → whom | Commitment | Source | Status |
|---|---|---|---|---|
| C1 | Gregory → Brandon | Forum post pulling together data-module anchor/sign, the claims engine, and GitHub links | Oct 6 [0:11:10] | **Open** |
| C2 | Gregory → Brandon | Invite to the claims-engine contributor group (conditional-use / commercial-reciprocity licence) | Oct 6 [0:14:00] | **Open** |
| C3 | Gregory → Brandon | Share the Foundation pitch "in the next month" | Jun 2 2026 | **Open** (5 months) |
| C4 | Gregory → Brandon | Eliza onboarding and hackathon sprint | Jan 13 2026 | Never mentioned again (likely lapsed) |
| C5 | Gregory → WG | Claims-engine and BD demo "next week" | Apr 21 2026 | Not held |
| C6 | Gregory → Brandon | "Happy to make other maintainers" | Feb 24 2026 | Not acted on |
| C7 | Christian → Brandon | Look at the outstanding PRs, "no promises" | Jun 2 2026 | Unknown |
| C8 | Dave → Brandon / validators | Better upgrade comms and a tighter validator loop | Oct 6 [0:23:25] | Open |
| C9 | Brandon → RND | Repost the governance proposal in a "more digestible" form (~3 days) | Oct 6 [0:24:22] | Unknown (forum blocked) |
| C10 | Brandon → WG | Liquid-staking review; Hydrex vetting; resubmit the stablecoin props | Aug–Nov 2025 | Never reported back. Close or re-scope. |
| C11 | Max → Brandon | Integrate the Market Monitor repo | Apr 21 2026 | Not mentioned again |

---

## 4. Matters arising register

Owner = the human accountable. Lane = the agent lane in §5 that prepares the work.

| ID | Matter | Evidence | Owner | Lane | Priority |
|---|---|---|---|---|---|
| **MA-01** | **Review backlog and single-maintainer bottleneck.** Probably-open PRs #108, #111, #112, plus about 10 unmerged PRs. Gregory is the only reviewer. | Feb 24 [0:25:42] "I'm the only one who's been doing [review]"; May 26 [0:14:57]; Mar 31 [0:22:34] | Gregory | L1 | P0 |
| **MA-02** | **Contract defects in merged v0 contracts.** *Confirmed by hand:* <ul><li>(a) `contracts/fee-router/src/contract.rs:101-134`: `CollectFee` is permissionless, never reads `info.funds`, and the crate has no `BankMsg`. Pool balances are fiction that anyone can inflate.</li><li>(b) `contracts/service-escrow/src/contract.rs:444`: the completion fee is `escrow_amount × fee_bps`, charged **on top of** the per-milestone fees already deducted at `:410`. That over-disburses against the deposit.</li></ul> *Seen in code, not run:* <ul><li>contribution-rewards distribution is unfunded</li><li>reputation-signal never enforces its min stake (`state.rs:160` against `contract.rs:187-250`) and strands the challenger bond</li><li>credit-class-voting is one-address-one-vote, open to sybils (`:378-392`), and sends slashes to admin when no community pool is set (`:419-424`)</li><li>attestation-bonding lets admin resolve challenges (`:287`) and floors an odd bond (`:350`)</li><li>no contract has admin rotation or a `migrate` entry point</li></ul> | Upstream code | Gregory (or a delegated Rust reviewer) | L2 | P0 if any contract is deployed or slated for testnet; otherwise P1 |
| **MA-03** | **Parameter incoherence across merged docs.** <ul><li>M013 split: 30/40/25/5 (`mechanisms/m013…/SPEC.md:183`), 28/25/45/2 (`phase-2/2.6`, synthesis), 15/30/50/5 (`needs-governance-proposals.md:80-86`).</li><li>Burn: 30% (`phase-4/4.2:307`) against the live 15% (#66).</li><li>Cap: 221M placeholder against ~239.8M supply against 321M (#68).</li><li>`dynamic-supply/src/contract.rs:43-48` rejects cap < supply, so it cannot represent today's chain.</li></ul> | `docs/governance/monetary-policy-anchor.md` (canonical since #109) | Gregory | L3 | P1 |
| **MA-04** | **RFC-0001 (#111) is stalled.** <ul><li>No human sponsor.</li><li>It cites a non-existent "M013 SPEC Appendix C".</li><li>It relies on the 221M cap, which the anchor rule §71 forbids.</li><li>`rfcs/GRADUATION_RULES.md` leaves the steward/ratifier roster undefined.</li><li>The RFC index is empty, and `phase-4/proposals/` doesn't exist.</li></ul> | #107, #111 | Gregory (sponsor decision) | L4 | P1 |
| **MA-05** | **On-chain governance cadence and comms.** <ul><li>The status of Brandon's proposals is unclear: he says "#79 VSH approved", but the anchor lists VSH as #75. #80 is about monthly contribution pay.</li><li>Incomplete proposals expire silently.</li><li>Upgrade comms were poor (Dave acknowledged the security-embargoed upgrade).</li><li>Brandon's Jan 20 idea: quarterly executor reports acknowledged on-chain.</li></ul> | Oct 6; Jan 20 [0:48:00] | Dave + Gregory | L0 → L5 | P1 |
| **MA-06** | **RND commitments to Brandon are unfulfilled** (C1–C6). | §3.3 | Gregory | L5 | P0 (cheap, high trust value) |
| **MA-07** | **Contributor pathway, recognition, compensation.** <ul><li>He has made 87 commits but holds no formal role.</li><li>He has been invited to be a validator ("You should", Gregory, Oct 6).</li><li>The maintainer offer has not been acted on.</li><li>Contribution pay is surfacing through his on-chain proposal, not through RND.</li><li>Attribution risk: a forum snippet (#602) apparently describes `brawlaphant` as "an OpenAI Codex agent", but the transcripts show a human who builds with Codex. Verify, and correct if it is wrong.</li></ul> | Feb 10, Feb 24, Oct 6; forum #602 (unverified) | Gregory | L6 | P1 |
| **MA-08** | **Strategic fit.** <ul><li>Brandon's stack (VSH experiments, the ecological work protocol, velf.net packets and receipts, x402 APIs) maps onto the claims engine and the data module.</li><li>His Base-migration ask (~$250k, which Gregory says must be community-funded) and his anti-CEX stance diverge from RND and SPV plans.</li></ul> | Oct 6, May 19, Jun 2 | Gregory | L7 | P2 |
| **MA-09** | **Market-integrity and regulatory exposure.** <ul><li>The agent "army" exists to accumulate and offload sell pressure.</li><li>Retirement-linked trades were described as "essentially wash trading" (Sep 30 2025 [0:55:14]).</li><li>Agent and WG tokens have been floated.</li></ul> RND must not endorse these, and the repo must not encode price-support or wash-trading mechanics. | Apr 7 [0:30:54], Feb 3, Sep 30 2025 | Gregory (+ counsel) | L8 | P1 |
| **MA-10** | **Repo hygiene.** <ul><li>`phase-5/5.2` shows the NEEDS_GOVERNANCE items as "Open, Q2 2026", which is stale.</li><li>The anchor §3 says #107 "proposes" the RFC process, but it was merged the same day.</li><li>vitest and cadCAD are not run in CI.</li><li>`Cargo.lock` is gitignored, yet the CI cache key hashes it.</li><li>The `glandua` fork is 221 commits behind.</li></ul> | Repo | Gregory | L3 | P2 |
| **MA-11** | **Discoverability and WG health.** <ul><li>Brandon "discovers it through Claude".</li><li>He asked for "a concentrated public piece".</li><li>WG attendance has thinned to Brandon and Max, and the WG has been silent since Jun 9 2026.</li><li>Christian has no GitHub notifications on.</li></ul> | Oct 6, May 26, Jun 9 | Gregory / Max | L5 | P2 |

---

## 5. Multi-agent workflow

### 5.1 Design principles

1. **Agents prepare, humans decide.** Every lane ends in a PR, draft, or decision memo. Merging, forum posting, on-chain submission, and anything sent to Brandon all need Gregory's explicit approval. This mirrors `rfcs/GRADUATION_RULES.md`, where agents never submit on-chain.
2. **Small units.** At most about 400 changed lines per PR, one mechanism or one concern per PR, and each PR names its layer, mechanism, and agent framework (Gregory's Feb 24 rule). This directly addresses the "too big to review" failure.
3. **Evidence or it didn't happen.** Every claim cites `file:line`, a PR number, a transcript timestamp, or a chain query. Every unverified claim is labelled as such.
4. **Adversarial verification.** A separate verifier agent re-checks each lane's output before it reaches the human gate, and is told to refute the output, not confirm it.
5. **The anchor is canonical.** `docs/governance/monetary-policy-anchor.md` wins every parameter conflict. Conflicts go to the RFC track, not to silent edits.

### 5.2 Agent roster

| Lane | Agent | Inputs | Output (acceptance criteria) |
|---|---|---|---|
| **L0** | **Evidence & Access** | Forum (#602, #616, #617, #618, #567, #19, Brandon's profile), Regen REST (`/cosmos/gov/v1/proposals/{75,79,80}`), GitHub API (PR states, reviews, issues, CI runs) | `evidence/facts-register.md`: every "unverified" item in this plan resolved to verified, refuted, or still unknown, with source links. Must resolve the #75 vs #79 VSH conflict, the #80 status, the authorship of #602, #616, #617, #618, and the open/closed state of all PRs in §3.2. **Prerequisite:** allow `forum.regen.network` and a Regen REST host in the environment's network policy, and attach `regen-network/agentic-tokenomics` with GitHub API access. |
| **L1** | **PR Triage** | All unmerged PR heads | `triage/pr-dispositions.md`: one row per PR with disposition (merge as-is / rework / split / close as superseded), rationale, and a draft review comment. Superseded PRs (#90, #91, #92, #80, #99, #52, #6, #11, #108) get closing notes that credit the work. Required splits: AGENT-004 runtime (~6k lines) and #112 (~6k lines) each into reviewable PRs of 400 lines or fewer, with a proposed order. |
| **L2** | **Contract Security** | `contracts/*` | For each finding: a failing test first, then a minimal fix PR, one per contract. Order: fee-router (require funds matching the computed fee and add the real `BankMsg` routing, or explicitly mark it accounting-only), service-escrow (remove the double fee or define its source), contribution-rewards (fund-backed distribution), reputation-signal (enforce min stake; withdrawal path for challenger bond), credit-class-voting (stake- or allowlist-weighted votes; never send slashes to admin), attestation-bonding (arbiter-only resolve; odd-bond remainder). Cross-cutting: `UpdateAdmin` plus `migrate`. Port the larger test suites from #72–#76 where they still apply. `cargo test`, clippy, and the wasm build must pass. |
| **L3** | **Parameter Coherence & Hygiene** | Anchor doc plus every doc citing the cap, split, or burn | `docs/governance/parameter-register.md`: one row per parameter, with live value and chain source, spec value, the open-question ID, and every doc that cites it. A PR adds "superseded by the anchor" banners and does not rewrite history. Separate PRs: `dynamic-supply` handles supply above cap via a burn-down mode, or documents why it is deferred; fix `phase-5/5.2` status; fix the anchor §3 wording; add vitest and cadCAD smoke runs to CI; fix the Cargo.lock cache key. |
| **L4** | **RFC Shepherd** | #111, `rfcs/*`, anchor | (a) A review of RFC-0001 that removes the Appendix C citation and the 221M reliance, re-bases on 239.8M and the live #66 burn, and lists exactly what a sponsor must check. (b) A draft RFC-0000, "Steward & ratifier roster and dispute escalation", that fills the gap in GRADUATION_RULES. (c) A populated RFC index and a `phase-4/proposals/` scaffold. (d) A recommendation on whether OQ-M012-1 (the cap value) should be the next RFC, as the anchor says it should. |
| **L5** | **Comms & Commitments** | §3.3 ledger, transcripts, repo | Drafts for Gregory to edit and send, written with the `living-language-tone` skill and the messaging constraints (no price talk): (1) **the promised forum post (C1)**, covering data-module anchor/sign via the Regen MCP, a claims-engine overview and access path, a repo map with "where to contribute", and the RFC route; (2) a direct reply to Brandon closing the loop on C1–C4 and the PR dispositions; (3) an upgrade-comms cadence post (C8) for Dave; (4) a WG restart note proposing an agenda for Max. |
| **L6** | **Contributor Pathway** | MA-07, CODEOWNERS, M015 spec, #80 (via L0) | A 2-page decision memo with options: (A) scoped co-maintainer of `agents/` and `simulations/` through CODEOWNERS, while `contracts/` and parameters stay RND-plus-RFC gated; (B) contributor-group membership only; (C) status quo. Covers compensation routes (M015 contribution rewards, the #80-style community-pool proposal, claims-engine reciprocity), validator onboarding steps, and the attribution correction. Includes a recommendation. |
| **L7** | **Integration Mapping** | Brandon's stack (velf.net, the ecological work protocol, VSH, x402 APIs), the claims engine, the data module | A one-page integration sketch: VSH and labour-hour receipts become anchored data (`MsgAnchor`/attest), then claims-engine claims, then payment linkage. It names the user stories (construction-safety coordinator, funder, labourer), the minimum viable pilot, and what RND provides versus Eco Wealth. It must not assume any token-price mechanism. |
| **L8** | **Risk & Integrity Review** | MA-09 items; L4 and L6 outputs | A screen of every proposal that touches trading, agent accumulation, agent or WG tokens, or retirement-linked volume, run with `legal:compliance-check`. Output: a red/amber/green rating per item and language RND can use to decline gracefully. Also scans the repo for any spec or agent behaviour that encodes price support or wash trading (AGENT-003 market-monitor in particular). |
| **V** | **Verifier (red team)** | Every lane's output | A refute-first review: does each cited `file:line` say what the output claims, are any facts stale, and are there scope creep or price claims? Returns pass, fix, or reject. Nothing reaches a gate without a pass. |

### 5.3 Phases and gates

```
Phase 0 (Days 0–2)  L0 Evidence & Access ───────────────► G0: Gregory signs off the facts register
                                                           (unblocks everything below)

Phase 1 (Week 1)    L5 forum post + reply to Brandon ─┐
                    L1 PR triage table ───────────────┼──► G1: Gregory approves the dispositions,
                    L2 failing tests (no fixes yet) ──┘        sends the reply, publishes the forum post
                    V on all

Phase 2 (Weeks 2–3) L2 fix PRs (one per contract) ────┐
                    L3 parameter register + hygiene ──┤
                    L4 RFC-0001 review + RFC-0000 ────┼──► G2: Gregory merges in small batches,
                    L1 split PRs for AGENT-003/004 ───┘        sponsors RFC-0001 (or declines it, with reasons)
                    V on all

Phase 3 (Weeks 3–4) L6 contributor-pathway memo ──────┐
                    L7 integration sketch ────────────┼──► G3: Decisions: Brandon's role, compensation
                    L8 risk screen (on L4, L6, L7) ───┘        route, VSH and claims-engine pilot,
                                                               validator onboarding; then a 1:1 with Brandon
```

**Dependencies.**
- L2 fixes wait on L1, so fixes don't collide with open PRs.
- L4 waits on L3, so the RFC re-bases on the parameter register.
- L6 and L7 wait on L0, which supplies the #80 and VSH facts.
- L8 gates L6 and L7.

### 5.4 Running it

- **Sizing.** 9 agents plus 1 verifier. At the default size guideline that is one workflow per phase (each under 10 agents), not a single fan-out.
- **Branching.** Each lane works in its own worktree and branch: `wf/<lane>-<slug>`. PRs go to `regen-network/agentic-tokenomics`, which needs push access, or are opened as fork PRs from `glandua/agentic-tokenomics` after syncing the fork to upstream.
- **Handoffs.** Each lane writes `wf/<lane>/OUTPUT.md` with a list of claims and the evidence for each. V reads only that file and the cited sources.
- **What is needed from Gregory before Phase 0:**
  - network allowlist for `forum.regen.network` and one Regen REST endpoint
  - GitHub API access to upstream (or a sync of the fork)
  - confirmation that no v0 contract is deployed on any network. If one is, L2 becomes a private advisory and does not use public issues.

---

## 6. Guardrails

- Agents never merge, never post to the forum or Discord, never message Brandon, and never sign or submit transactions. They draft; Gregory sends.
- Public-facing text follows RND messaging constraints:
  - no REGEN price or return claims
  - no endorsement of agent accumulation or volume schemes
  - REGEN is framed as coordination and ecological-accounting infrastructure
- Contributor work is credited. Closing a superseded PR always links to the PR that carried its content forward.
- Brandon's sovereignty is respected (Dave, Oct 6). The plan offers structure and does not direct his independent ventures.

---

## 7. Recommendation

1. **This week, cheap and high-trust.** Send the forum post you promised (C1) and a direct reply to Brandon that acknowledges the body of work by name and gives a PR disposition table with dates. This is the single most leveraged action. Every transcript shows the gap is acknowledgment and direction, not volume.
2. **Make him a scoped co-maintainer (option A in L6)** of `agents/` and `simulations/`, with CODEOWNERS. Keep `contracts/` and parameters behind RND review plus the RFC process. This addresses the bottleneck without handing over control of the economic core.
3. **Redirect his energy to where it compounds for both sides:** VSH and labour-verification receipts on the data module, flowing into the claims engine (the L7 pilot). This is his strongest and most aligned idea.
4. **Draw a clear line on agent-trading and token schemes.** They stay outside RND repos and messaging, and the reasons are given respectfully (L8).
5. **Fix the contracts before anyone treats them as more than advisory.** The fee-router and escrow defects would lose or fabricate funds.

---

## 8. Next actions

- [ ] Gregory: allow `forum.regen.network` and a Regen REST host in the environment, and grant GitHub API access to upstream (unblocks L0).
- [ ] Gregory: confirm the deployment status of the v0 contracts (decides public vs private handling in L2).
- [ ] Gregory: approve running Phase 0 and Phase 1 as a multi-agent workflow.
- [ ] Gregory: publish the C1 forum post and send the reply to Brandon (drafts come from L5).
- [ ] Gregory: decide on the RFC-0001 sponsor after the L4 review.
- [ ] Gregory and Dave: set an upgrade-comms cadence and a validator touchpoint (C8).
- [ ] Gregory: Foundation pitch to Brandon (C3), or say explicitly that it is deferred.
- [ ] Max / Gregory: restart or formally pause the Tokenomics WG (silent since Jun 9).
