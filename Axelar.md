![1v (6)](https://user-images.githubusercontent.com/92199696/195659349-109c51b4-1af4-419f-927e-0c629e1acce6.png)

# POSTHUMAN Contributions to [Axelar](https://axelar.network)

# 🛠 Technical Contributions

- We operate an [Axelar mainnet validator](https://www.mintscan.io/axelar/validators/axelarvaloper1ftqma496np33y054x6gjeh2maxy00e00p2nl9l).

- We operate Axelar `vald` and `tofnd` and maintain external-chain voting
  infrastructure.

## Axelar Validator Operations AI Skill

- [Open-source Axelar validator skill](https://github.com/Validator-POSTHUMAN/AI-skills-for-networks/tree/f9b0b74e1be8d7399721059371a72e8017164a69/axelar)
- Validator-neutral inventory schema and safety evals.
- Healthcheck for `axelard`, `vald`, `tofnd`, broadcaster funding, recent
  consensus signatures, external-chain maintainer state, and stale consensus.

## Axelar Safe Recovery Kit

- [Recovery reference](https://github.com/Validator-POSTHUMAN/AI-skills-for-networks/blob/f9b0b74e1be8d7399721059371a72e8017164a69/axelar/references/safe-recovery.md)
- [Restore and archive-validation evidence](https://github.com/Validator-POSTHUMAN/AI-skills-for-networks/blob/f9b0b74e1be8d7399721059371a72e8017164a69/axelar/references/recovery-validation.md)
- [Snapshot verifier](https://github.com/Validator-POSTHUMAN/AI-skills-for-networks/blob/f9b0b74e1be8d7399721059371a72e8017164a69/axelar/scripts/axelar-snapshot-verify.sh)
- [Deterministic verifier tests](https://github.com/Validator-POSTHUMAN/AI-skills-for-networks/blob/f9b0b74e1be8d7399721059371a72e8017164a69/axelar/scripts/axelar-snapshot-verify-test.sh)
- Full-download, trusted SHA-256, LZ4 integrity, safe archive-layout,
  signer-state, staged extraction, rollback, and external-signing gates.

## Upstream `axelar-core` Contributions

- [PR #2382 — fail health check on stale consensus](https://github.com/axelarnetwork/axelar-core/pull/2382)
  addresses [issue #1039](https://github.com/axelarnetwork/axelar-core/issues/1039)
  by checking catching-up state, height, block time, and consensus freshness.
- [PR #2383 — use decode hooks in health check](https://github.com/axelarnetwork/axelar-core/pull/2383)
  fixes a panic on valid Linea `finality_override = "confirmation"`
  configuration and returns normal health-check errors for genuine decode
  failures.
- Both focused patches include regression tests and passed local package,
  race, vet, full-suite, build, and clean-apply checks before publication.

## Sputnik Network

We added AXL support to [Sputnik Network Bot](https://t.me/SputnikNetworkBot)
without project funding.

![image](https://user-images.githubusercontent.com/92199696/205491037-51fa4cfb-f604-4acc-9a43-66cad0fca7c2.png)

We added $AXL to Sputnik Exchange and Sputnik Network. Users can send AXL tips
on X and Telegram and use the Telegram P2P exchange.
[Announcement](https://twitter.com/SputnikNetwork/status/1592164428476473345)

## Axelar Block Explorer

- **Block Explorer** [for Axelar](https://explorer.posthuman.digital/axelar)

<img width="2200" height="1356" alt="image" src="https://github.com/user-attachments/assets/4c76ff86-0468-4d90-9167-16e33d72ebb0" />

## We added Axelar to [Restake](https://restake.app/axelar/axelarvaloper1ftqma496np33y054x6gjeh2maxy00e00p2nl9l)

## Mail2Telegram

[Mail2Telegram](https://github.com/Validator-POSTHUMAN/mail2telegram) forwards
Axelar operational email notifications to Telegram.

## Public Axelar Services

Service hub: https://nodes.posthuman.digital/chains/axelar

- RPC: https://rpc.axelar.posthuman.digital
- REST: https://rest.axelar.posthuman.digital
- gRPC: grpc.axelar.posthuman.digital:443
- Peer: adece904395c55d4fd1c2581b0d7a9be899f5a9d@peer.axelar.posthuman.digital:64656
- Snapshots: https://snapshots.axelar.posthuman.digital
- [Installation Guide](https://nodes.posthuman.digital/chains/axelar?tab=installation-guide)
- [Safe Snapshot Recovery](https://nodes.posthuman.digital/chains/axelar?tab=snapshots)
- [Axelar AI Validator Skill](https://nodes.posthuman.digital/chains/axelar?tab=skill)

# 🧠 Community and Educational Contributions

Including community growth, ecosystem education, media, and Axelar news
coverage.

Current channel inventory and audience figures are maintained on the
[POSTHUMAN Superpowers page](https://github.com/Validator-POSTHUMAN/About-POSTHUMAN/blob/main/superpowers.md).

## Historical Axelar Quest Campaign

We launched an Axelar quest and task campaign on the Centrifuge platform with
300 participants. The original campaign page is currently unavailable; the
campaign screenshot is preserved below.

<img width="2875" height="719" alt="image" src="https://github.com/user-attachments/assets/6aab432d-288d-4820-b0c0-e32b2109dbc2" />

## Russian-language Media and Education

- **YouTube** (11.4k subscribers)
  [CryptoBase](https://www.youtube.com/@CRYPTOBASED)

## Videos

- [Cosmos Ecosystem Insider Chat #37. New Bot. Rebus Drop, Where Did the Evmos Interest Go?, Axelar](https://www.youtube.com/watch?v=OOYZ0XnS3t4)

We also host recurring Cosmos ecosystem audio/video discussions that include
Axelar news and education.

<img width="2585" height="1572" alt="image" src="https://github.com/user-attachments/assets/840856a4-0856-47b1-a3df-f54635130e7e" />

[==>Go to playlist<==](https://youtube.com/playlist?list=PLgQFzABJoJYx-lwnvZwKjDqsDxiccjP-G)

## Russian-language Telegram Communities

We maintain and contribute to these communities:

- https://t.me/CosmosEcosystem_ru | ~8k members
- https://t.me/Crypto_Base_Chat | ~4.1k members
- https://t.me/CosmosEcosystemNews_ru |  ~2000 members

### Social Media
- **X (Twitter)**  
  - [Cosmos Ecosystem](https://x.com/CosmosEcosystem) (34.8k followers)
  - [POSTHUMAN](https://x.com/POSTHUMAN_DVS) (7.2k followers)

## Contributions for Axelar Network

<img width="1684" height="1664" alt="image" src="https://github.com/user-attachments/assets/55e90ffa-a532-4fe4-8164-3902d99a5f24" />

### Special Infographics  
Covering news from the Axelar Ecosystem:  
- [Infographic 1](https://x.com/CosmosEcosystem/status/1845843159885943206)  
- [Infographic 2](https://x.com/CosmosEcosystem/status/1849041307953410516)  
- [Infographic 3](https://x.com/CosmosEcosystem/status/1860887292467970239)  

### 📰Daily News  
- [Daily News about Axelar](https://x.com/CosmosEcosystem/status/1937505218490695955)
- [Daily News about Axelar](https://x.com/CosmosEcosystem/status/1932730497983029437)
- [Daily News about Axelar](https://x.com/CosmosEcosystem/status/1919060529869443202)
- [Daily News about Axelar](https://x.com/CosmosEcosystem/status/1907067916505272328)
- [Daily News about Axelar](https://x.com/CosmosEcosystem/status/1882354699497886153)
- [Daily News about Axelar](https://x.com/CosmosEcosystem/status/1872357225039303130)
- [Daily News about Axelar](https://x.com/CosmosEcosystem/status/1850919048638280031)
- [Daily News about Axelar](https://x.com/CosmosEcosystem/status/1848026611007848843)


### 📰Weekly News (Statistics)  
- [Weekly News about Axelar](https://x.com/CosmosEcosystem/status/1842233928310304800)  
- [Weekly News about Axelar](https://x.com/CosmosEcosystem/status/1847257084036841811)  
- [Weekly News about Axelar](https://x.com/CosmosEcosystem/status/1849776309213295102)  
- [Weekly News about Axelar](https://x.com/CosmosEcosystem/status/1852347500134388075)  
- [Weekly News about Axelar](https://x.com/CosmosEcosystem/status/1857817790763159999)  


### Our contributions for the growth of the Axelar community.

| Name               | Description                                              | Relevant URLs                                                                                      | Additional Details                                          |
|--------------------|-----------------------------------------------------------|---------------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| Cosmos Ecosystem X | 34.8k followers. We have been promoting Axelar Network and its updates since genesis. | [Query CosmosEcosystem tweets about Axelar Network](https://x.com/search?q=from%3ACosmosEcosystem%20(Axelar%20OR%20axelar%20OR%20%24AXL)&src=typed_query&f=live) | We spread the word about Axelar Network and its updates since genesis. |
| POSTHUMAN X        | 7.2k followers. We actively cover Axelar Network updates and ecosystem news since genesis. | [Query POSTHUMAN_DVS tweets about Axelar Network](https://x.com/search?q=from%3APOSTHUMAN_DVS%20(Axelar%20OR%20axelar%20OR%20%24AXL)&src=typed_query&f=live) | We spread the word about Axelar Network and its updates since genesis. |

# Economic Contributions

We plan to distribute a share of validator income to delegators.
[Details](https://posthuman.digital/phmn)

## About POSTHUMAN

[Learn more about our team](https://posthuman.digital/team).
