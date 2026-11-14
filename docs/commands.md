# Commands

good-miner takes plain words, no dashes:

```text
good-miner-cli [global words] <command> [words...]
good-miner-cli help                 # the overview
good-miner-cli help <command>       # one command, e.g. help mine
```

The miner's own `help` is always right for the build you have; this page is the map.

## Commands

| command | what it does |
| --- | --- |
| `mine <coin>` | mine a coin. `mine auto` picks the most profitable one for this hardware |
| `algo <algorithm>` | mine an algorithm directly on a pool you name: `algo kawpow url <host:port> wallet <address>` |
| `list` | look at things: `coins`, `gpu`, `cpu`, `algorithms`, `coin <ticker>`, `algorithm <name>`, `wallets`, `pools`, `tuning`, `network <coin>`, `market` |
| `coin` | `coin show <ticker>`, `coin list` |
| `config` | saved settings: per coin (pool, wallet, worker, threads) and for this machine (cards, UI, power price) |
| `device` | `device list`; `device amd-restore` puts AMD cards back on factory tuning |
| `stats` | `stats hashrates` (your benchmarks), `stats blocks`, `stats fee` |
| `util` | tools: `benchmark <coin>`, `profit`, `pair`, `api`, `probe <host:port>`, `validate-pool <url>`, `nvrtc`, `hiprtc`, `oc-autotune`, `trace`, `dump` |
| `version` | the build you have |

## `mine`

```text
good-miner-cli mine <coin> [words...]
```

After the coin, in any order:

| word | meaning |
| --- | --- |
| `wallet <address>` | your wallet |
| `url <host:port>` | the pool |
| `user <name>`, `pass <password>` | pool account name and password |
| `tls`, `tcp` | encrypted or plain connection |
| `gpu`, `cpu` | that hardware only |
| a number | CPU threads (0 = all; default all but one) |
| `gpu 1,2 <second coin>` | first coin on cards 1 and 2, the second coin on the rest |
| `algo <name>` | choose the algorithm, for a coin that has more than one |
| `solo` | the coin's solo pool |
| `auto-interval <minutes>` | how often `mine auto` re-checks |

Examples:

```text
good-miner-cli mine rvn wallet <address>
good-miner-cli mine rvn url stratum.ravenminer.com:3838 wallet <address> pass x
good-miner-cli mine auto
good-miner-cli mine auto cpu
good-miner-cli mine prl gpu 1,2 rvn
good-miner-cli mine krgn gpu 0
good-miner-cli mine qtc algo quantus wallet <address>
```

## Global words

They work with every command and go anywhere on the line.

| word | meaning |
| --- | --- |
| `ui` | open the terminal UI this run |
| `solo` | mine solo |
| `cpu-threads <n>` | CPU mining threads |
| `temp-limit <C>` / `temp-resume <C>` | pause a GPU above this, resume below that (90 / 78) |
| `cpu-temp-limit <C>` | pause CPU mining above this (110) |
| `fan <percent>` | hold AMD fans at this speed (Linux) |
| `undervolt <mV>` | undervolt AMD cards for the session, with `amd-governor` (Linux) |
| `amd-governor` | steer AMD power caps by junction temperature (Linux) |
| `igpu` | include integrated graphics |
| `api-port <n>` | this instance's API port |
| `log-file <path>`, `log-level <level>` | where the log goes and how much (`debug`, `info`, `warn`, `error`, `trace`) |
| `dump` | write diagnostics when the run ends |
| `buddy` | run under the watcher (`mine` always does) |
| `auto-kill` | stop other running miners instead of asking |

## Turning things off: `no`

`no` turns off whatever follows it, and can take several at once: `no gpu 0,1 cuda`.

| words | meaning |
| --- | --- |
| `no gpu` | no GPU mining |
| `no gpu 0,1` | leave out cards 0 and 1 this run |
| `no cpu` | no CPU mining |
| `no oc` | no overclock at all |
| `no octune` | skip the one-time memory tune (stored settings still apply) |
| `no tune` | no tuning sweep of any kind |
| `no cuda` | NVIDIA cards through OpenCL instead of CUDA |
| `no opencl` | no OpenCL devices |
| `no fan` | never write a fan speed |
| `no amd-governor` | AMD cards fan-only, power cap untouched |
| `no msr`, `no hugepages` | no CPU register writes, no huge pages |
| `no buddy` | no watcher: nothing restarts a crashed miner |
| `no ui`, `no igpu` | override a saved `config set ui` / `config set igpu` for this run |

## `config`

Per coin:

```text
good-miner-cli config set rvn url <host:port> wallet <address>
good-miner-cli config show rvn
good-miner-cli config clear rvn
good-miner-cli config list
```

For this machine, on every run:

| setting | meaning |
| --- | --- |
| `config set gpu 0,2` | only these cards mine |
| `config gpu disable <n>` / `enable <n>` / `enable all` | turn cards off and on |
| `config set ui` | always open the terminal UI |
| `config set igpu` | always include integrated graphics |
| `config set tcp` | prefer plain connections where a coin has one |
| `config set kwh 0.18` | your electricity price, for profit figures |
| `config set gpu-watts <W>`, `cpu-watts <W>` | the rig's real power draw, for profit figures |
| `config set amd-governor`, `amd-junction-target <C>` | AMD junction governor (Linux) |
| `config cpu disable msr` / `hugepages` | never use them |

`config show <word>` shows one, `config clear <word>` undoes it.
