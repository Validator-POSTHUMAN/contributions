# Monad Liquid Staking Pools: Validator Integration Research

Last updated: 2026-07-01

This public research brief is for Monad validators, LST teams, and ecosystem
partners evaluating validator integrations, delegation routes, and MEV /
priority-fee opportunities across Monad liquid staking protocols.

It is written from a validator-operator perspective and focuses on reusable
questions: what the validator onboarding path looks like, what public
documentation exists, which operational changes may be required, and how clear
the delegation mechanism is.

POSTHUMAN examples are included only as field notes from one active Monad
validator. The main purpose is to help other validators prepare better
questions and help LST teams make validator onboarding easier to evaluate.

## Validator Priority Snapshot

| Protocol | Token | Validator onboarding signal | Priority | Notes for validators |
| --- | --- | --- | --- | --- |
| shMonad / FastLane | shMON | Clear public validator docs and direct onboarding path. | Very high | Best documented validator path. Delegation is tied to revenue generation and on-chain stake allocation. Requires beneficiary / coinbase flow, dedicated fullnodes, and MEV sidecar. |
| Kintsu | sMON | Positive team response and DAO / registry-based validator curation. | High | Promising route for validators that can participate in a registry / governance-driven delegation process. Exact operational requirements should be confirmed during onboarding. |
| Magma | gMON | Batch / whitelist style validator inclusion. | Medium-high | Strong LST product and gVault concept. Validators should prepare a profile and wait for the next inclusion batch or whitelist review. |
| aPriori | aprMON | Product is strong, validator onboarding path is not clear from public docs. | Low-medium | Worth tracking, but validators should verify official contact channels before relying on this route. |
| Moonmace | mcMON | Public scoring model exists, but onboarding and community signal are weak. | Low | Useful as a watchlist item. Needs clearer validator process and stronger execution signal. |

## Scoring Method

Scores are qualitative and intended for validator integration prioritization,
not investment advice or a final judgment on any protocol.

- 5 = actionable now, clear validator path, good response, material expected value.
- 3 = worth tracking or continuing outreach, but blocked by timing,
  governance, unclear rules, or team response.
- 1 = no clear path or weak signal.

| Protocol | Onboarding clarity | Team / channel signal | Delegation upside | Operational fit | Overall |
| --- | ---: | ---: | ---: | ---: | ---: |
| shMonad / FastLane | 5 | 5 | 5 | 4 | 5 |
| Kintsu | 4 | 4 | 4 | 3 | 4 |
| Magma | 3 | 3 | 4 | 4 | 3.5 |
| aPriori | 1 | 2 | 4 | 2 | 2 |
| Moonmace | 2 | 1 | 2 | 3 | 1.5 |

## Validator Questions to Ask Any Monad LST Team

- Is validator onboarding currently open?
- Is the validator set permissionless, curated, batch-based, or DAO-governed?
- What are the exact validator inclusion criteria?
- Is there a public application form, registry, or direct team process?
- What performance window is reviewed?
- How are uptime, commission, MEV revenue, and priority-fee capture measured?
- Are there stake caps, concentration limits, or region / provider constraints?
- What validator-side configuration changes are required?
- Does the protocol require a sidecar, beneficiary change, coinbase contract,
  fullnode peers, collateral, governance votes, or smart-contract interaction?
- How can a validator verify received delegation and revenue after onboarding?

## shMonad / FastLane

shMonad / FastLane currently has the clearest validator-facing route.
The protocol connects validator revenue generation with shMonad stake
allocation.

### Validator Path

The validator onboarding flow includes:

1. shMonad / FastLane deploys a validator-specific coinbase contract.
2. The validator sets that coinbase contract as beneficiary in node.toml.
3. The validator restarts monad-bft; RPC / execution restart is not required
   for the beneficiary change.
4. The validator connects FastLane dedicated fullnodes, with peer information
   selected by validator location.
5. The validator runs the MEV sidecar.
6. The validator monitors revenue, commission, donation settings, and stake
   allocation.

### Delegation / Revenue Model

FastLane's onboarding material describes:

- 90% of MEV auction revenue goes to the validator's coinbase contract.
- Priority fee distribution depends on validator commission, configurable by
  the validator.
- shMonad delegation is performance-based: more revenue means more stake.
- Stake allocation is on-chain and deterministic.
- The MEV sidecar runs as a separate process and was described as
  Foundation-approved.
- Revenue starts flowing from the next epoch after setup, approximately 5.5
  hours.
- FastLane stated during onboarding that 118 validators were already running
  the sidecar.

### Validator Considerations

- This is an operational integration, not only a listing request.
- Changing beneficiary / coinbase flow affects validator revenue routing.
- The sidecar should be monitored independently from the core node services.
- Validators should document rollback steps before changing production config.

### Example Field Note

One active Monad validator, POSTHUMAN, contacted FastLane / shMonad, was
accepted, received onboarding instructions, and installed the FastLane MEV
sidecar for its Monad mainnet validator.

Example validator profile used during onboarding:

- Validator ID: 197
- Location: Tokyo, Japan
- Commission: 15%
- Validator page:
  https://monadvision.com/validator/0xAED164187A9D6314591Ae581A922380A63a1Bd67

### Sources

- shMonad docs: https://docs.shmonad.xyz/
- Validator onboarding:
  https://docs.shmonad.xyz/validators/onboarding
- Sidecar installation:
  https://docs.shmonad.xyz/validators/onboarding/install-sidecar-rootless-docker
- Stake allocation:
  https://docs.shmonad.xyz/stake-allocation
- Revenue dashboard:
  https://analytics.shmonad.xyz/stake-analytics/revenue
- MEV analytics: https://mev-pulse.fastlane.xyz
- Revenue calculator: https://fastlane-revenue-calculator.vercel.app
- Commission portal:
  https://analytics.shmonad.xyz/validator-portal/commission
- FastLane GitHub: https://github.com/FastLane-Labs
- FastLane contracts:
  https://github.com/FastLane-Labs/fastlane-contracts
- FastLane sidecar:
  https://github.com/FastLane-Labs/fastlane-sidecar
- FastLane blog: https://www.fastlane.xyz/blog
- FastLane X: https://x.com/0xFastLane
- FastLane Discord: https://discord.fastlane.xyz

## Kintsu

Kintsu is a Monad liquid staking protocol that issues sMON and uses a
DAO-driven validator registry / delegation marketplace.

### Validator Path

Public Kintsu documentation describes a decentralized validator registry
controlled by the DAO. Validators should expect a more governance-oriented
onboarding process than a simple whitelist form.

Validators should clarify:

- whether validator registry onboarding is open;
- whether collateral is required;
- whether governance / voting weight affects delegation;
- how validator performance is measured;
- how stake targets are updated.

### Validator Considerations

- Kintsu appears promising for validators willing to engage with DAO / registry
  mechanics.
- The technical and governance requirements should be confirmed directly before
  treating the opportunity as production-ready.
- Validators may need a communication plan, not only node-side changes.

### Example Field Note

Kintsu replied positively to POSTHUMAN and indicated that onboarding can
continue. The process is still in progress, so exact requirements should be
confirmed directly with the Kintsu team.

### Sources

- Kintsu site: https://kintsu.xyz/
- Kintsu staking app: https://kintsu.xyz/staking
- Kintsu docs: https://docs.kintsu.xyz/
- Kintsu on Monad:
  https://docs.kintsu.xyz/supported-blockchains/kintsu-on-monad.md
- Monad LST architecture:
  https://docs.kintsu.xyz/the-kintsu-protocol/architecture-and-integration/monad-lst-architecture.md
- DAO and governance:
  https://docs.kintsu.xyz/the-kintsu-protocol/dao-and-governance.md
- Official contract addresses:
  https://docs.kintsu.xyz/the-kintsu-protocol/official-contract-addresses.md
- Kintsu GitHub: https://github.com/WaterCoolerStudiosInc
- Kintsu audits:
  https://github.com/WaterCoolerStudiosInc/Kintsu-Audits
- Kintsu X: https://x.com/Kintsu
- Kintsu legacy Twitter handle: https://twitter.com/kintsu_xyz
- Kintsu Discord: https://discord.gg/kintsu
- Kintsu Medium: https://medium.com/@kintsu_xyz

## Magma

Magma is a liquid staking protocol on Monad that issues gMON. Its docs describe
liquid staking, gVaults, and MEV-boosted yield.

### Validator Path

Magma appears to use a curated or batch-based validator inclusion process.
Its gVault model is especially relevant for validators because it can let users
choose a validator-specific route while still receiving fungible gMON.

Validators should prepare:

- validator ID and public validator page;
- uptime and performance history;
- commission;
- infrastructure region / provider profile;
- MEV and priority-fee readiness;
- monitoring and alerting summary.

### Validator Considerations

- Strong product direction and useful gVault structure.
- Public docs do not currently expose a simple self-serve validator onboarding
  form.
- The practical route is direct team contact and waiting for the next validator
  batch / whitelist window.

### Example Field Note

Magma's team response to POSTHUMAN was to wait for the next validator batch.
This supports the current assumption that validator inclusion is batch-based or
curated rather than fully self-serve.

### Sources

- Magma site: https://www.magmastaking.xyz/
- Magma docs: https://docs.hydrogenlabs.xyz/magma
- Magma liquid staking:
  https://docs.hydrogenlabs.xyz/magma/liquid-staking-gmon.md
- gVaults docs: https://docs.hydrogenlabs.xyz/magma/gvaults.md
- gVaults app: https://gvaults.magmastaking.xyz/
- gVaults launch article:
  https://blog.magmastaking.xyz/p/gvaults-are-live-staking-vaults-built
- Magma audits:
  https://docs.hydrogenlabs.xyz/magma/developers/audits
- Magma GitHub:
  https://github.com/magmastaking/contracts-public
- Magma X: https://x.com/magmastaking
- Magma Discord: https://discord.com/invite/magmastaking

## aPriori

aPriori has a strong Monad MEV / liquid staking narrative. aprMON is positioned
as a liquid staking token that accrues staking and MEV revenue.

### Validator Path

Public docs explain the product and staking yield, but they do not currently
make the validator onboarding route clear.

Validators should verify:

- whether new validators can join the aprMON delegation set;
- whether the set is curated, automated, or governance-controlled;
- which official contact path should be used;
- whether MEV infrastructure integration is required.

### Validator Considerations

- Protocol narrative is strong.
- Validator inclusion path is opaque from public docs.
- Validators should avoid relying on unofficial or unstable community routes
  until an official channel is confirmed.

### Example Field Note

Validator outreach friction was observed during POSTHUMAN's attempt to contact
aPriori: ticket creation did not work cleanly, and a visible server/channel
route later became unavailable. This is treated as a process-risk signal for
validator onboarding clarity, not as a conclusion about the protocol or product
quality.

### Sources

- aPriori site: https://www.apr.io/
- aPriori docs: https://apriori-docs.gitbook.io/apriori-docs
- aprMON basics:
  https://apriori-docs.gitbook.io/apriori-docs/aprmon/aprmon-basics.md
- Staking yield:
  https://apriori-docs.gitbook.io/apriori-docs/aprmon/aprmon-basics/staking-yield.md
- aPriori FAQ:
  https://apriori-docs.gitbook.io/apriori-docs/faqs/faq.md
- Stake app: https://stake.apr.io
- aPriori X: https://x.com/aPriori
- aPriori Discord: https://discord.com/invite/apriori

## Moonmace

Moonmace is a smaller Monad liquid staking project with mcMON. Public docs
describe a validator selection matrix, but the practical validator onboarding
route is not yet clear.

### Validator Path

Moonmace docs describe validator scoring based on:

- performance / reliability;
- MEV or priority-fee efficiency;
- centralization risk;
- stake caps and concentration-aware penalties.

### Validator Considerations

- The scoring model is relevant for validators.
- Current observable signal is weaker than the other reviewed protocols.
- Validators should monitor passively until community activity and onboarding
  process become clearer.

### Example Field Note

POSTHUMAN did not receive a useful onboarding response at review time, and
public validator-facing signal appeared limited. Validators may still track the
project, but should wait for a clearer process before prioritizing integration.

### Sources

- Moonmace docs: https://moonmace.gitbook.io/moonmace-docs
- mcMON liquid staking:
  https://moonmace.gitbook.io/moonmace-docs/liquid-staking-mcmon.md
- Validator strategy:
  https://moonmace.gitbook.io/moonmace-docs/validator-strategy.md
- System architecture:
  https://moonmace.gitbook.io/moonmace-docs/system-architecture.md
- Moonmace X: https://x.com/moonmace_ai

## Practical Checklist for Validators

Before integrating with any Monad LST pool:

1. Confirm the official onboarding channel.
2. Confirm whether the process is open, curated, batch-based, or DAO-governed.
3. Ask for all validator-side changes in writing.
4. Back up node configuration before changing beneficiary, peers, or sidecars.
5. Define rollback steps before restarting production services.
6. Monitor the LST-specific sidecar / revenue path separately from core Monad
   node health.
7. Verify delegation and revenue after the next epoch.
8. Keep public validator profile, commission, uptime, and region information
   ready for future LST teams.

## Example Validator Profile: POSTHUMAN

This profile is included as an example of the information an LST team may ask
from any validator during onboarding:

- Validator: POSTHUMAN
- Monad mainnet validator ID: 197
- Validator page:
  https://monadvision.com/validator/0xAED164187A9D6314591Ae581A922380A63a1Bd67
- Commission: 15%
- Location: Tokyo, Japan
- Operator profile: experienced multi-chain validator with production
  monitoring, active alerting, and existing Monad mainnet operations.
- MEV / priority-fee posture: willing to integrate validator-side revenue
  infrastructure when the operational requirements are clear and safe.
