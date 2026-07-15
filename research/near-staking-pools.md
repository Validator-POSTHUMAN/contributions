# NEAR Staking Pools and Validator Delegation Research

Last updated: 2026-07-15

This validator-facing brief covers the main NEAR liquid-staking pools and
delegation programs, their public selection rules, and practical onboarding
routes. Values and registries are point-in-time; recheck before outreach or
operational changes.

## Priority Snapshot

| Route | Public model | Validator path | POSTHUMAN status |
| --- | --- | --- | --- |
| Meta Pool / stNEAR | Liquid staking plus validator programs | Node Studio cohorts, performance, and mpDAO votes | Active in Node Studio Cohort #3; about `40.2K NEAR` delegated by `meta-pool.near` |
| NEAR Legion City Nodes | Community-linked direct delegation | Qualify through recurring city activity and apply | Madrid is a credible candidate route; event approval and Legion evidence are still required |
| LiNEAR / LiNEAR | Automatic validator scoring and stake optimization | Meet published rules, then confirm current registry/onboarding process | Not found in the checked LiNEAR validator registry on 2026-07-15 |
| Rhea Finance / rNEAR | Weighted validator pool periodically reviewed by the Rhea DAO | Direct team/DAO outreach; no public validator form found | Not found in the checked rNEAR validator registry on 2026-07-15 |

## POSTHUMAN Validator Snapshot

- Validator: `posthuman.poolv1.near`
- Explorer: https://nearblocks.io/validators/posthuman.poolv1.near
- Active validator, no current kickout, `7%` fee.
- Current role: chunk validator / endorser. `0 produced / 0 expected` blocks
  and chunks is normal for this role and does not mean the node is inactive.
- Current-epoch sample on 2026-07-15: `4,478 / 4,509` endorsements
  (`99.31%`).
- Total pool stake: about `40.3K NEAR`; Meta Pool stake: about `40.2K NEAR`.

## Meta Pool / Node Studio

POSTHUMAN already participates in Node Studio Cohort #3. The practical task is
program compliance, not a second application.

Published terms include:

- `40,000 NEAR` initial delegation for 12 months;
- `5 NEAR` monthly platform payment, charged on the first day of the month;
- at least five documented activity points each month;
- a monthly evidence report;
- possible additional delegation through performance and community votes.

Recommended actions:

1. Keep the payment account funded before each monthly charge.
2. Submit activity evidence every month.
3. Maintain validator performance and promote the mpDAO vote link.

Links:

- Validator programs: https://docs.metapool.app/master/validator-nodes/validator-programs
- Participation guidelines: https://docs.metapool.app/master/validator-nodes/validator-programs/node-studio-program-1/participation-guidelines
- Monthly payment: https://docs.metapool.app/master/node-studio/monthly-payment
- POSTHUMAN vote link: https://www.metapool.app/vote/?validator=posthuman.poolv1.near

## NEAR Legion City Nodes

City Nodes is not an LST, but it is the largest published direct-delegation
route reviewed here. The 2026 announcement describes ten city-node slots with
`300,000 NEAR` delegated to each selected validator and recurring reviews.

The published eligibility paths are:

- one Legion member already running at least three events per month in a city;
  or
- a team of at least three Vanguard members that has already hosted an event
  together.

Madrid is a realistic POSTHUMAN route because the team has access to a venue
and prior meetup experience. A useful evidence pack should include official
event approval, calendar listings, agendas, attendance, photos, public links,
reports, and Proof of Attendance SBTs.

Links:

- Program: https://www.near.org/blog/legion-city-nodes
- Application: https://docs.google.com/forms/d/e/1FAIpQLScJWdRx2ZP0ymDstiVJMIP8D-IdkJpfGFXNi66LEzM0leDWog/viewform
- Legion calendar: https://luma.com/near-legion
- Legion support: https://t.me/nearlegionsupport

## LiNEAR

LiNEAR publishes an automatic staking-optimization model. Its documented
eligibility rules are:

- validator is in the active set;
- validator APY is above `6%`;
- validator fee is at most `10%`;
- all conditions hold for ten consecutive epochs.

The published `APY > 6%` threshold needs confirmation. NEAR protocol version
84 reports a maximum inflation rate of `1/40`, or `2.5%` of total supply per
year. Validator APY cannot be configured directly; it follows protocol
issuance, the active staking ratio, performance, and commission. Under the
current economics, a normal validator may not be able to sustain more than
6% gross APY. This is an operator inference, not a statement of current
LiNEAR policy.

Recommended outreach questions:

1. Is the published 6% threshold still applied literally after the inflation
   reduction?
2. Is validator addition automatic, manager-controlled, or manually reviewed?
3. Which ten-epoch and 30-day performance evidence is required?
4. Does the current chunk-validator / endorser role satisfy active-set
   eligibility?

Links:

- Delegation model: https://docs.linearprotocol.org/developer-guide/automatic-staking-optimization
- X: https://x.com/LinearProtocol
- Discord: https://discord.gg/bkkvWwMf2T

## Rhea Finance / rNEAR

Rhea documents a decentralized weighted pool of validators scored by:

- reward performance with time weighting;
- uptime stability;
- staking ratio;
- community reputation.

Scores are calculated automatically and periodically reviewed by the Rhea
DAO. No public self-service validator application was found, so direct
onboarding outreach is the practical route.

Links:

- rNEAR and validator strategy: https://guide.rhea.finance/near-chain-guides/near-liquid-staking-tokens-lst
- Contracts: https://guide.rhea.finance/developers/contracts
- X: https://x.com/rhea_finance
- Discord: https://discord.gg/rheafinance

## Recommended Outreach Packet

Send LiNEAR and Rhea:

1. Validator ID and explorer link.
2. Active chunk-validator status and the explanation for `0/0 expected`
   blocks/chunks.
3. Ten-epoch and 30-day performance, fee, uptime, and kickout history.
4. Existing Meta Pool Node Studio delegation and operational history.
5. Infrastructure region, monitoring summary, and decentralization value.
6. A direct request for current eligibility, registry addition, and allocation
   process.

## Recommended Order

1. Keep Meta Pool Node Studio compliance green.
2. Formalize Madrid Legion events and apply for City Nodes when eligible.
3. Request current LiNEAR criteria and registry addition.
4. Request Rhea DAO/team onboarding.

## Primary Sources

- NEAR liquid staking providers and contracts:
  https://docs.near.org/primitives/liquid-staking/liquid-staking
- Meta Pool validator programs:
  https://docs.metapool.app/master/validator-nodes/validator-programs
- LiNEAR automatic staking optimization:
  https://docs.linearprotocol.org/developer-guide/automatic-staking-optimization
- Rhea rNEAR validator strategy:
  https://guide.rhea.finance/near-chain-guides/near-liquid-staking-tokens-lst
- NEAR Legion City Nodes:
  https://www.near.org/blog/legion-city-nodes

This report is operational research for validator onboarding, not investment
advice or a guarantee of delegation.
