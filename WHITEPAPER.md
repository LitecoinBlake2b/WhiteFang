# White Fang Medical Research — Whitepaper v1 (Draft)

**Coin:** White Fang · **Ticker:** WFANG *(preliminary availability check clear, Sept 29 2026)*
**Slogan:** *Supercomputer fighting disease.*
**Positioning:** *Every coin mined helped research.*
**Status:** DRAFT v1 — 29 September 2026. Open decisions are marked **[OPEN]**.

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

### Anti-fraud and open questions **[OPEN]**

- **Identity binding:** how a Folding@home donor name is cryptographically
  bound to a WFANG address (signed message scheme proposed).
- **Sybil resistance:** one human, one donor identity — policy and
  enforcement TBD.
- **Double-payment:** deltas must be computed against committed checkpoints
  so points are never paid twice.
- **API dependence:** the individual-donor stats endpoint returned
  HTTP_NOT_FOUND in testing (Sept 2026); the exact data source for
  per-donor scores must be validated before launch. Fallback: team-level
  aggregation with sub-accounts.
- **Oracle trust:** the oracle is a trusted component at launch; the
  roadmap includes decentralizing it (multi-signer attestations, then
  on-chain verification).

## 5. Tokenomics **[OPEN — parameters proposed, not decided]**

| Parameter | Proposal | Status |
|---|---|---|
| Name | White Fang Medical Research | Decided |
| Coin name | White Fang | Decided |
| Ticker | WFANG | Preliminary check clear |
| Consensus | Scrypt PoW | Decided |
| Premine | None — fair launch from block 1 | Decided |
| Block time | 2.5 minutes (Litecoin-style) | Proposed |
| Max supply | 84,000,000 WFANG | Proposed |
| Halving | Every 840,000 blocks (~4 years) | Proposed |
| Folding / PoW reward split | 70% folding / 30% PoW | **Proposed, NOT accepted** |
| Launch date | TBD | Open |

The 70/30 split in favor of folding reflects the project's mission —
security needs far less than the mission deserves — but the final ratio is
the founder's call.

## 6. Fair Launch

No premine. No ICO. No founder allocation. Mining starts at block 1 and
anyone can participate from the first block — with an ASIC on the PoW track
or with any computer on the folding track. The founder's hardware mines
under the same rules as everyone else's.

## 7. Roadmap

- [x] Concept validated — "Every coin mined helped research."
- [x] Branding locked — name, slogan, coin visual, token logos (v1).
- [ ] **Tokenomics finalized** — block time, supply, reward split, oracle design.
- [ ] Full availability verification — name, ticker, domains, socials, trademarks.
- [ ] Chain implementation — Scrypt PoW client (fork of an established codebase).
- [ ] Folding oracle — identity binding, delta computation, auditable distribution.
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
