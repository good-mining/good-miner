# Coins

Every coin here has had shares accepted by a real pool from good-miner. `good-miner-cli list coins` prints the
list in your release, and `good-miner-cli coin show <ticker>` one coin's details.

The pool shown is the coin's default in the coin list: a public pool we have mined on, not an endorsement and
not ours. Use any pool you like with `url <host:port>`. Replace `<your address>` with your own wallet address.

A ticker that appears twice is one coin with two algorithms (or two coins sharing a ticker): add the
algorithm name after the ticker, as shown.

## GPU coins

| coin | ticker | algorithm | default pool | command |
| --- | --- | --- | --- | --- |
| [Abelian](https://abelian.info) | ABEL | AbelHash | `fiona-service.abelian.info:27778` (TLS) | `mine abel wallet <your address>` |
| [Aeternity](https://aeternity.com) | AE | CuckooAe | `ae.2miners.com:4040` | `mine ae wallet <your address>` |
| [Alephium](https://alephium.org) | ALPH | Blake3Alephium | `us2.alephium.herominers.com:1221` | `mine alph wallet <your address>` |
| [Beam](https://beam.mw) | BEAM | BeamHashIII | `us2.beam.herominers.com:1130` | `mine beam wallet <your address>` |
| [Conflux eSpace](https://confluxnetwork.org/) | CFX | octopus | `us2.conflux.herominers.com:1170` | `mine cfx wallet <your address>` |
| [Cryptix](https://github.com/cryptix-network) | CPAY | CryptixHash | `us.nushypool.com:40003` | `mine cpay wallet <your address>` |
| [Decred](https://decred.org) | DCR | Blake3PoW | `decred.cedric-crispin.com:4494` | `mine dcr wallet <your address>` |
| [Etica](https://www.eticaprotocol.org/) | EGAZ | Etchash | `egaz.etica-stats.org:8008` | `mine egaz wallet <your address>` |
| [Epic Cash](https://epic.tech) | EPIC | EpicProgPow | `us.epicmine.io:3333` (TLS) | `mine epic algo epicprogpow wallet <your address>` |
| [Ergo](https://ergoplatform.org) | ERG | Autolykos | `us2.ergo.herominers.com:1180` | `mine erg wallet <your address>` |
| [Ethereum Classic](https://ethereumclassic.org) | ETC | Etchash | `us2.etc.herominers.com:1150` | `mine etc wallet <your address>` |
| [Evrmore](https://evrmorecoin.org) | EVR | EvrProgPow | `us.evrpool.org:5010` | `mine evr wallet <your address>` |
| [Frencoin](https://frencoin.io) | FREN | KawPow | `fren.coolpool.top:2042` | `mine fren wallet <your address>` |
| [Grin](https://grin.mw) | GRIN | Cuckatoo32 | `us-grin.2miners.com:3030` | `mine grin wallet <your address>` |
| [Hoosat](https://hoosat.fi) | HTN | HooHash | `us.nushypool.com:40012` | `mine htn wallet <your address>` |
| [Kerrigan](https://kerrigan.network/) | KRGN | KawPow | `na.rplant.xyz:7041` | `mine krgn algo kawpow wallet <your address>` |
| [Kerrigan](https://kerrigan.network/) | KRGN | Equihash192_7 | `ca.himpool.com:1469` | `mine krgn algo equihash192_7 wallet <your address>` |
| [Parallax](https://parallaxchain.org) | LAX | XHash | `na.rplant.xyz:7159` | `mine lax wallet <your address>` |
| [Meowcoin](https://meowcoin.com) | MEWC | MeowPow | `na.rplant.xyz:7120` | `mine mewc wallet <your address>` |
| [MimbleWimbleCoin](https://www.mwc.mw) | MWC | Cuckatoo31 | `us-mwc.2miners.com:7575` | `mine mwc wallet <your address>` |
| [Neoxa](https://www.neoxa.net) | NEOX | KawPow | `na.rplant.xyz:7069` | `mine neox wallet <your address>` |
| [Nexa](https://nexa.org/) | NEX | Nexapow | `us-nexa.2miners.com:5050` | `mine nex wallet <your address>` |
| [Pearl](https://pearl.network) | PRL | PearlHash | `us2.pearl.herominers.com:1200` | `mine prl wallet <your address>` |
| [Qubitcoin](https://superquantum.io/qubitcoin) | QTC | Qhash | `ca.luckypool.io:8615` | `mine qtc algo qhash wallet <your address>` |
| [Quantus Network](https://quantus.com) | QTC | Quantus | `us2.quantus.herominers.com:1155` | `mine qtc algo quantus wallet <your address>` |
| [Ravencoin](https://ravencoin.org) | RVN | KawPow | `stratum.ravenminer.com:3838` | `mine rvn wallet <your address>` |
| [SmartCore](https://github.com/says112/smartcore-node) | SMC | Ethash | `smartcore.su:8009` | `mine smc wallet <your address>` |
| [Telestai](https://telestai.io) | TLS | ProgPowTelestai | `na.rplant.xyz:7051` | `mine tls wallet <your address>` |
| [Vertcoin](https://vertcoin.org) | VTC | Verthash | `vertcoin.cedric-crispin.com:3334` | `mine vtc wallet <your address>` |
| [Waglayla](https://waglayla.com) | WALA | WalaHash | `mine.xdag1usa.com:3094` | `mine wala wallet <your address>` |
| [Warthog](https://www.warthog.network) | WART | Janushash | `us2.warthog.herominers.com:1143` | `mine wart wallet <your address>` |
| [Bitcoin BLAKE2b](https://bitcoin-blake2b.org) | XBT | Blake2bXbt | `ord.b2pool.io:4444` | `mine xbt wallet <your address>` |
| [Xelis](https://xelis.io) | XEL | XelisHash | `us2.xelis.herominers.com:1225` | `mine xel wallet <your address>` |
| [Neurai](https://neurai.org) | XNA | KawPow | `us-xna.2miners.com:6060` | `mine xna wallet <your address>` |
| [Tari](https://www.tari.com) | XTM | SHA-3X | `ca2.luckypool.io:6118` | `mine xtm algo sha-3x wallet <your address>` |
| [Tari](https://www.tari.com) | XTM | Cuckaroo | `gulf.moneroocean.stream:10128` | `mine xtm algo cuckaroo wallet <your address>` |
| [Zano](https://zano.org/) | ZANO | ProgPowZ | `us2.zano.herominers.com:1110` | `mine zano wallet <your address>` |

## CPU coins

| coin | ticker | algorithm | default pool | command |
| --- | --- | --- | --- | --- |
| [AdventureCoin](https://adventurecoin.quest) | ADVC | YespowerADVC | `na.rplant.xyz:7149` | `mine advc wallet <your address>` |
| [Babacoin](https://github.com/babacoinbbc/babacoin) | BBC | GhostRider | `na.rplant.xyz:7082` | `mine bbc wallet <your address>` |
| [DERO](https://dero.io) | DERO | AstroBWTv3 | `fastpool.xyz:10300` (TLS) | `mine dero wallet <your address>` |
| [Epic Cash](https://epic.tech) | EPIC | RandomX | `us.epicmine.io:3333` (TLS) | `mine epic algo randomx wallet <your address>` |
| [Etica](https://www.eticaprotocol.org/) | ETI | RandomX | `us.0xpool.io:3333` | `mine eti wallet <your address>` |
| [Mytherra](https://github.com/MYT-Core/MYT) | MYT | RandomX | `eu.rplant.xyz:7061` | `mine myt wallet <your address>` |
| [Quantum Resistant Ledger](https://www.theqrl.org/) | QRL | RandomX | `us2.qrl.herominers.com:1166` | `mine qrl wallet <your address>` |
| Ratatoskr | RATR | Yespower | `na.rplant.xyz:7122` | `mine ratr wallet <your address>` |
| [Rincoin](https://github.com/Rin-coin/rincoin) | RIN | RinHash | `na.rplant.xyz:7148` | `mine rin wallet <your address>` |
| Rhino | RMC | YespowerR16 | `na.rplant.xyz:7161` | `mine rmc wallet <your address>` |
| [Raptoreum](https://raptoreum.com) | RTM | GhostRider | `na.rplant.xyz:7056` | `mine rtm wallet <your address>` |
| [Salvium](https://salvium.io) | SAL | RandomX-Salvium | `salvium.minorpool.com:5070` | `mine sal wallet <your address>` |
| [Sugarchain](https://sugarchain.org) | SUGAR | YespowerSugar | `yespowerSUGAR.na.mine.zpool.ca:6241` | `mine sugar wallet <your address>` |
| [UraniumX](https://uraniumx.org/) | URX | YespowerURX | `cpu-pool.com:63378` | `mine urx wallet <your address>` |
| [Dagger](https://xdag.org) | XDAG | RandomX | `stratum.xdag.org:23656` | `mine xdag wallet <your address>` |
| [Monero](https://www.getmonero.org) | XMR | RandomX | `us2.monero.herominers.com:1111` | `mine xmr wallet <your address>` |
| [Zephyr](https://zephyrprotocol.com) | ZEPH | RandomX-Zephyr | `us.zephyr.herominers.com:1123` | `mine zeph wallet <your address>` |

## Notes

- **Memory:** Ethash-family, KawPow-family and Cuckoo-family coins need several GB of GPU memory. The miner
  tells you at start if a card cannot hold a coin's dataset.
- **AMD and NVIDIA:** GPU coins run on both unless the release notes say otherwise.
- **Intel:** experimental, and proven so far on Qubitcoin (qhash) only
  ([details](gpus-and-cooling.md#intel-graphics)).
- **Missing a coin?** Open a coin request. Coins are added when they have an accepted share, not before.
