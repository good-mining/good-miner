# Hashrates

What good-miner measured, card by card. Every number here came from the miner's own benchmark
(`good-miner-cli util benchmark <coin>`) or from a pool run, on the card named, on the date given. Nothing is
estimated, copied from another site or scaled from a different card.

Stock clocks unless a power cap is stated. A tuned card will usually do better; a card in a hot case will do
worse. Your numbers are welcome: see the end of this page.

## NVIDIA

### RTX 4090 (stock, 2026-11-06)

| coin | algorithm | hashrate |
| --- | --- | --- |
| Pearl (PRL) | PearlHash | 262.5 TH/s |
| Kaspa (KAS) | kHeavyHash | 2.05 GH/s |
| Alephium (ALPH) | Blake3 | 4.99 GH/s |
| Nexa (NEX) | NexaPow | 196.3 MH/s |
| Ethereum Classic (ETC) | Etchash | 113.8 MH/s |
| Conflux (CFX) | Octopus | 113.1 MH/s |
| Ravencoin (RVN) | KawPow | 58.6 MH/s |

### RTX 5090

| coin | algorithm | hashrate | power | date |
| --- | --- | --- | --- | --- |
| Pearl (PRL) | PearlHash | about 338 TH/s | 500 W | 2026-11-10 |
| Pearl (PRL) | PearlHash | 261 TH/s | capped at 400 W | 2026-11-10 |

### H100 SXM

| coin | algorithm | hashrate | power | date |
| --- | --- | --- | --- | --- |
| Pearl (PRL) | PearlHash | 352 TH/s | 700 W | 2026-11-10 |
| Pearl (PRL) | PearlHash | 213 TH/s | capped at 500 W | 2026-11-10 |

### RTX 5070

| coin | algorithm | hashrate | power | date |
| --- | --- | --- | --- | --- |
| Conflux (CFX) | Octopus | 76.9 MH/s | 235 W | 2026-10-07 |

### RTX 5060 Ti

| coin | algorithm | hashrate | date |
| --- | --- | --- | --- |
| Nexa (NEX) | NexaPow | 82.4 MH/s | 2026-10-29 |
| Aeternity (AE) | Cuckoo 29 | 11.1 G/s | 2026-10-20 |

### RTX 3070

| coin | algorithm | hashrate | date |
| --- | --- | --- | --- |
| Aeternity (AE) | Cuckoo 29 | 9.0 G/s | 2026-10-20 |

## AMD

### RX 9070

| coin | algorithm | hashrate | power | date |
| --- | --- | --- | --- | --- |
| Conflux (CFX) | Octopus | 76.7 MH/s | 219 W | 2026-10-08 |
| Ravencoin (RVN) | KawPow | 39.1 MH/s | 203 W | 2026-10-27 |
| Pearl (PRL) | PearlHash | 67.6 to 68.0 TH/s | capped at 164 W | 2026-10-20 |

## CPU

| CPU | coin | algorithm | hashrate | date |
| --- | --- | --- | --- | --- |
| Ryzen 9 9950X | Monero (XMR) | RandomX | 18.2 kH/s | 2026-10-07 |
| Ryzen 9 5900X | Monero (XMR) | RandomX | 11.0 kH/s | 2026-11-06 |

## More to come

This table is short because we print only what we measured on that exact card. We are filling it in coin by
coin for the cards on our own rig (RTX 3070, RTX 5060 Ti, RTX 5070, RX 9070) and for cards we rent.

## Add your card

```text
good-miner-cli util benchmark <coin>
good-miner-cli stats hashrates
```

Open an issue with the output, your card, driver version and operating system, and whether the card is
overclocked. We add community numbers under the reporter's name, marked as community-measured.
