# HiveOS

good-miner runs on HiveOS as a custom miner. Each release carries a HiveOS package (`good-miner-<version>.tar.gz`
with the `h-*.sh` scripts).

## Flight sheet

Pick **Custom miner** and fill in:

| field | value |
| --- | --- |
| Miner name | `good-miner` |
| Installation URL | the HiveOS package's link from the release page |
| Hash algorithm | the algorithm name as good-miner knows it, e.g. `kawpow`, `pearlhash` (`good-miner-cli list algorithms`) |
| Wallet and worker template | `%WAL%.%WORKER_NAME%` |
| Pool URL | `host:port` |
| Pass | `x`, or what the pool wants |
| Extra config arguments | any good-miner words, e.g. `tls` or `no gpu 2` |

HiveOS then shows hashrate, temperature and fan per card, accepted and rejected shares, and uptime.

Under HiveOS the miner runs without its own watcher and without its own overclock, because HiveOS provides
both: set clocks and power in HiveOS as you would for any miner.

## Other mining systems

Any system that can launch a custom miner with a command line and read JSON over HTTP can run good-miner. The
command line is the same as in [getting started](getting-started.md); per-rig statistics are at
`http://<rig>:4040/api/v1/`. Tell us which system you use and we will add its steps.
