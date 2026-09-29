# White Fang Medical Research — Whitepaper v1 (Draft)

**Coin:** White Fang · **Ticker:** WFANG *(preliminary availability check clear, Sept 29 2026)*
**Slogan:** *Supercomputer fighting disease.*
**Positioning:** *Every coin mined helped research.*
**Status:** DRAFT v1.1 — 29 September 2026. Tokenomics decided by IGOR under
Sebastien's delegation ("decide with the greatest logic"). The founder can
override any parameter before launch.

---

## 1. Abstract

White Fang (WFANG) is a proof-of-work cryptocurrency with a second purpose:
every unit of computation that secures the network is paired with computation
that serves medical research. The project combines a **Scrypt PoW blockchain**
for consensus and block production with a **reward oracle for Folding@home
contributors**, the long-running distributed computing project that simulates
protein folding to help understand diseases such as cancer, Alzheimer's and
Parkinson's.

The thesis is simple: the world's mining hardware already burns energy to
secure blockchains. White Fang redirects part of that incentive toward
something no ASIC can fake — real scientific computation.

## 2. The Problem

Proof-of-work mining consumes enormous amounts of electricity to compute
hashes whose only product is consensus. The work is necessary for security,
but it produces nothing outside the chain itself. Meanwhile, projects like
Folding@home have a permanent shortage of compute for protein-folding
simulations that directly advance drug discovery — and their contributors are
paid in nothing but points and goodwill.

Earlier attempts (CureCoin, Medic Coin, FoldingCoin) proved the model can
work, but most of them are dead, stalled, or were tokens riding on other
chains rather than sovereign networks. There is no living, mineable,
Scrypt-based chain pairing native consensus with folding rewards today.

## 3. The Solution: Useful Work, Two Tracks

White Fang runs a hybrid reward model with two independent ways to earn:

1. **Scrypt mining (Proof-of-Work).** Standard Nakamoto consensus on Scrypt.
   ASICs (e.g. Antminer L3 class hardware) secure the chain and produce blocks
   from block 1. This is the security backbone — battle-tested, simple, and
   immediately mineable with existing hardware and pool infrastructure.

2. **Folding rewards (Proof-of-Useful-Work).** Anyone with a CPU or GPU can
   install Folding@home, contribute compute to medical research, and earn
   WFANG proportional to their verified folding points. No ASIC required —
   a laptop can earn.

A fixed share of every block reward (or of a dedicated emission stream —
**[OPEN]**, see §5) is allocated to folding contributors, distributed
according to folding points verified through the Folding@home statistics API.

### Why Scrypt

- The founding hardware mines Scrypt from day one — no new machines needed.
- Existing, proven pool infrastructure (Stratum) can be reused directly.
- Scrypt is the most widely deployed ASIC-friendly PoW after SHA-256:
  deep miner and pool ecosystem, understood difficulty dynamics.

## 4. Folding@home Integration

Folding@home (foldingathome.org) is active and maintained — stable release
8.5.6 (July 2026), open source under GPL-3.0-or-later. Its statistics API
exposes team and donor scores programmatically (team endpoint verified
working, Sept 2026).

### How folding rewards are verified

1. The project operates an official Folding@home **team**. Miners fold under
   this team identity (or register a linked donor name).
2. An **oracle service** polls the Folding@home stats API, records each
   donor's point deltas per reward period, and publishes a signed,
   publicly auditable distribution list (donor → points → WFANG owed).
3. Folding rewards are paid from the folding allocation, either as
   on-chain coinbase outputs or via periodic distribution transactions —
   **[OPEN]** design decision.

### Oracle design — v1 decision (pragmatic, centralized at launch)

Perfection is the enemy of launch. The v1 oracle is **operated by the
project** and fully auditable; decentralization comes later.

1. A folder registers by publishing a signed binding:
   `Folding@home donor name → WFANG address` (signature proves address
   ownership; donor-name ownership is claimed on first registration —
   disputes resolved by the project in v1).
2. Each reward period (e.g. 24h), the oracle snapshots donor point deltas
   from the Folding@home stats API, computes each donor's share of the
   period's folding allocation, and publishes the complete distribution
   list **publicly** (donor, points, WFANG owed) before paying.
3. Anyone can recompute the distribution from the public Folding@home stats
   — the oracle is trusted to *execute*, not to *decide*.
4. Checkpoints prevent double-payment: a period's deltas are committed once
   and never re-counted.

Roadmap: v2 adds multi-signer oracle attestations; v3 targets on-chain
verification of folding proofs.

### Remaining open questions **[OPEN]**

- **Sybil resistance:** one human, one donor identity — policy and
  enforcement TBD (v1 relies on registration + public scrutiny).
- **API dependence:** the individual-donor stats endpoint returned
  HTTP_NOT_FOUND in testing (Sept 2026); the exact data source for
  per-donor scores must be validated before launch. Fallback: team-level
  aggregation with sub-accounts.

## 5. Tokenomics

| Parameter | Value | Status |
|---|---|---|
| Name | White Fang Medical Research | Decided |
| Coin name | White Fang | Decided |
| Ticker | WFANG | Preliminary check clear (full verification pending) |
| Consensus | Scrypt PoW | Decided |
| Premine | None — fair launch from block 1 | Decided |
| Block time | 2.5 minutes | Decided |
| Max supply | 84,000,000 WFANG | Decided |
| Block reward (initial) | 50 WFANG | Decided |
| Halving | Every 840,000 blocks (~4 years) | Decided |
| Reward split | **60% folding / 40% PoW miners** | Decided (see rationale) |
| Launch date | TBD | Open |

Emission check: 840,000 blocks × 50 WFANG × 2 (geometric series) =
84,000,000. ✓

### Why 60/40

The split is the project's most important economic decision, and it was made
on the following logic:

- **The mission is the brand.** The slogan is *Supercomputer fighting
  disease* — folding must receive the majority of every block, or the
  branding is a lie.
- **Security must be real from block 1.** 40% of the block reward is a full,
  serious miner incentive — more than enough to attract Scrypt hashrate at
  low early difficulty, when coins are cheapest to mine. A new chain's
  biggest risk is low hashrate, not low folding participation.
- **60/40, not 70/30:** the earlier 70/30 proposal starved the security
  budget for little extra mission gain. 60/40 keeps the mission clearly
  first while giving miners a share no one can call symbolic.
- The split is consensus-critical and cannot be changed lightly after
  launch — hence deciding it now, before any code exists.

### How the split works mechanically

Each block mints 50 WFANG: **20 WFANG** to the PoW miner (coinbase),
**30 WFANG** to the folding allocation. The folding allocation accumulates
and is distributed periodically (e.g. daily) by the oracle, proportional to
verified Folding@home points earned in the period — see §4.

## 6. Fair Launch

No premine. No ICO. No founder allocation. Mining starts at block 1 and
anyone can participate from the first block — with an ASIC on the PoW track
or with any computer on the folding track. The founder's hardware mines
under the same rules as everyone else's.

## 7. Roadmap

- [x] Concept validated — "Every coin mined helped research."
- [x] Branding locked — name, slogan, coin visual, token logos (v1).
- [x] **Tokenomics decided** — 2.5 min blocks, 84M max, 50 WFANG/block,
      halving every 840,000 blocks, 60% folding / 40% PoW.
- [x] **Oracle v1 designed** — project-operated, publicly auditable,
      decentralization roadmap set.
- [ ] Full availability verification — name, ticker, domains, socials, trademarks.
- [ ] Chain implementation — Scrypt PoW client (fork of an established codebase).
- [ ] Folding oracle implementation.
- [ ] Donor stats API source validated (HTTP_NOT_FOUND issue resolved).
- [ ] Testnet with folding rewards.
- [ ] Website / landing page.
- [ ] Mainnet launch — fair, from block 1.

## 8. Branding

- **Project:** White Fang Medical Research
- **Coin:** White Fang (WFANG)
- **Slogan:** *Supercomputer fighting disease.*
- **Visual identity:** gold coin, geometric white wolf head; token icons in
  gold-on-dark and white-on-gold variants.
- The wolf is the emblem; the mission is the message. "Croc Blanc" remains
  the community nickname for French speakers.

## 9. Risks and Honest Limitations

- **New chain, no network effect.** Like every fair launch, White Fang starts
  with zero hashrate beyond its founders — early 51% risk is real and must be
  managed (checkpoints, honest disclosure).
- **Oracle centralization at launch.** Folding rewards depend on an
  operator-run oracle until it is decentralized.
- **Folding@home dependence.** The project relies on a third-party academic
  project remaining available and its API remaining accessible.
- **Regulatory.** No legal review has been conducted. Nothing here is
  financial advice or an offer of securities.

---

*White Fang Medical Research — Supercomputer fighting disease.*
*Draft v1, 29 September 2026. Comments and corrections welcome — this document
evolves with the project's decisions.*
