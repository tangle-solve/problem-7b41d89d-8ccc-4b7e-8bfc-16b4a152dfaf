<!-- solve-problem:7b41d89d-8ccc-4b7e-8bfc-16b4a152dfaf -->
# Coverage rewards with heterogeneous builder costs

A [Tangle Solve problem](https://solve.tangle.tools/problems/7b41d89d-8ccc-4b7e-8bfc-16b4a152dfaf).

## What is the problem?

Consider a **builder-coverage game**: a set of builders (block producers in proposer-builder separation, PBS) each choose which "regions" of the transaction/inclusion demand they serve (e.g., peripheral or latency-sensitive orderflow). The protocol pays rewards for covering regions, and an allocation rule selects which covered builder is chosen. In the current public formulation (assumed: complete information, common/public cost distributions, exogenous builder set, independent outages), equilibrium, a factor-2 price-of-anarchy bound, and market-concentration results are known (Öz et al. 2026, per census — verify). The open problem is to extend this model along four axes simultaneously:

1. **Private (heterogeneous) costs**: each builder's serving cost is its own private information, known only through bidding/coverage choices (a Bayesian or mechanism-design setting, not complete information).
2. **Endogenous entry**: builders decide whether to enter at all, incurring a fixed entry cost (linking to stochastic facility-location games with entry fees).
3. **Correlated outages**: builders' availability/failures are statistically dependent (shared infra, common exogenous shocks), not independent.
4. **Redundant identities (sybils)**: the reward/coverage rule must deter a single operator from registering multiple identities to farm coverage rewards.

The deliverable is a coverage-reward mechanism plus analysis: existence of (Bayesian) equilibrium, efficiency/welfare (price-of-anarchy or anarchy-stability) bounds robust to the four extensions, and sybil-resistance in the sense that splitting into multiple identities is never a profitable deviation.

## Why does it matter?

Peripheral coverage rewards are one of the few proposed tools to counter builder centralization in PBS markets without hard forking protocol trust assumptions. A mechanism that works only under public costs, fixed participation, and independent failures cannot be deployed: real builders have private costs, enter and exit, share infrastructure (correlated outages), and will run sybils if rewarded for doing so. Solving this yields a deployable anti-centralization reward design for Ethereum-style PBS and a clean bridge between facility-location games and blockchain market design.

## What's already known?

Per the census record (all items "verify" — the cited 2026 paper is the anchor): the base model of Öz, Wu, Correia, Yang, Mazorra and Leonardos establishes, for the complete-information game with an exogenous builder set, equilibrium existence, a **factor-2 price-of-anarchy** bound, and results on market concentration; the census dates these as "October 2026 equilibrium" results. Classical related literature: stochastic facility-location games with entry costs give equilibrium-existence and inefficiency machinery for location/coverage decisions with fixed entry fees; the literature on sybil-proof mechanisms (e.g., in contests, procurement, and reward sharing) gives tools for identity-resistance but typically without spatial/coverage structure or correlated availability. The census marks private costs + entry + correlation + sybil-resistance jointly as open; no partial results combining them are recorded.

## What would count as solving it?

A referee would accept any of:
- **Mechanism + theorem**: a coverage-reward rule under which, with private costs, endogenous costly entry, and correlated outage processes, a (Bayesian) equilibrium exists and satisfies either (a) a stated PoA bound (matching or degrading gracefully from the factor-2 benchmark), or (b) a coverage/coverage-robustness guarantee (all sufficiently valuable regions covered with high probability despite outages), together with a **sybil-resistance proof**: multi-identity deviations yield non-positive utility gain.
- **Lower bound / impossibility**: a proof that no budget-balanced reward rule simultaneously achieves non-trivial efficiency and sybil-resistance with private costs and correlated outages, with a concrete separating example.
- **Partial but clean**: solve any strict subset (e.g., private costs + sybil-resistance with exogenous entry and independent outages) with matching upper/lower bounds.

## How to start

1. Reconstruct the base model from Öz et al. (2026) — read its equilibrium and PoA sections first; this defines regions, rewards, allocation, and where factor-2 comes from (likely a smoothness argument — check whether smoothness extends to Bayesian settings, since Bayesian smoothness often carries complete-info bounds over).
2. Formalize private costs as a Bayesian game; try a direct-revelation variant (first-price vs. second-price-style coverage payments) to see which retains the factor-2 bound.
3. Model sybils as a multi-identity deviation mapping and test known sybil-resistance conditions (e.g., payments non-increasing in identity counts, or identity-invariant allocation) against the coverage objective — the main obstacle is that rewarding *marginal coverage* naturally pays each additional sybil its marginal region.
4. Add entry costs and correlated outages last, importing stochastic facility-location techniques for existence (fixed-point / potential-function arguments) and copula-based correlation for outage analysis.

## Key references

- Öz, ?, Wu, ?, Correia, ?, Yang, ?, Mazorra, ?, Leonardos, S. (2026), *The Price of Decentralization in Block Building*, DOI:10.4230/LIPIcs.AFT.2026.25 — base model: builder-coverage game with equilibrium existence, factor-2 PoA, and concentration results (details unverified; census is the sole source). https://doi.org/10.4230/LIPIcs.AFT.2026.25
- Stochastic facility-location games with entry costs (no specific citation in census) — the classical analogue for entry-cost equilibrium analysis; consult the facility-location game literature directly (verify).

## Warnings

- The key reference is dated 2026 and known only via the census record; author initials and even existence must be verified before relying on it — do not build on unstated assumptions about its model.
- The census phrasing is informal; the formalization above (Bayesian private costs, costly entry, correlated availability, sybil deviations) is the most reasonable reading, but the original authors may intend a narrower mechanism-design question.
- "Deterring redundant identities" is subtle: naive marginal-coverage rewards are sybil-*attractive*; per-identity caps or non-additive reward concavity are the usual fixes, but they can conflict with the coverage objective and the PoA bound — expect a real tension, not a free extension.
- Independent vs. correlated outages changes welfare metrics qualitatively (coverage probability is no longer a product), so concentration results may not transfer.

---
*`BCGT-000309` · flagged for review*

## Acceptance guidance

A referee would accept any of:
- **Mechanism + theorem**: a coverage-reward rule under which, with private costs, endogenous costly entry, and correlated outage processes, a (Bayesian) equilibrium exists and satisfies either (a) a stated PoA bound (matching or degrading gracefully from the factor-2 benchmark), or (b) a coverage/coverage-robustness guarantee (all sufficiently valuable regions covered with high probability despite outages), together with a **sybil-resistance proof**: multi-identity deviations yield non-positive utility gain.
- **Lower bound / impossibility**: a proof that no budget-balanced reward rule simultaneously achieves non-trivial efficiency and sybil-resistance with private costs and correlated outages, with a concrete separating example.
- **Partial but clean**: solve any strict subset (e.g., private costs + sybil-resistance with exogenous entry and independent outages) with matching upper/lower bounds.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/7b41d89d-8ccc-4b7e-8bfc-16b4a152dfaf?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: BCGT-000309.

- [Public source catalog](https://drewstone.github.io/problems/#/p/BCGT-000309)
