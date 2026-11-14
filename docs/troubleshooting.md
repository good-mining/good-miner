# Troubleshooting

Start with the last lines the miner printed and with `logs/good-miner.log.<date>`. When the miner stops on
purpose it says why, and its exit code tells a script or a mining OS the same thing.

## Exit codes

| code | meaning | what to do |
| --- | --- | --- |
| 0 | finished or stopped normally | |
| 75 | a GPU's driver context faulted; a fresh process is the cure | nothing: buddy restarts it. If it repeats on one card, lower that card's overclock (`no oc` to test) and check its power cables. |
| 76 | a device took a job and never started working | nothing: buddy restarts it. Repeats point at a driver or that card. |
| 77, 78 | switching coin (`mine auto`, or the dashboard asked) | nothing: buddy starts the new coin. |
| 79 | the request cannot work: unknown coin or algorithm, or no wallet | fix the command line. `list coins` shows the names. |
| 80 | the pool did not answer | check the address and port; `util probe <host:port>`. Buddy keeps retrying slowly. |
| 81 | no share was accepted | the wallet or login format is wrong for this pool, or the pool is on another algorithm. `coin show <coin>` gives the expected login format. |
| 82 | 10 rejected shares in a row | usually an overclock that is too high, or a wrong pool for the coin. Try `no oc`. If it persists, report it with the log. |
| 83 | half or more of the shares rejected | as 82. |
| 84 | this install cannot build or load its GPU kernels | keep every file from the archive together; update the GPU driver; run `util nvrtc` (NVIDIA) or `util hiprtc` (RX 9070). |
| 85 | the CPU crossed its thermal limit | cooling. The miner will not restart into the same heat. |
| 86 | you stopped it (Ctrl+C, the UI, the dashboard) | |

Codes 81 to 83 are safety stops: the miner refuses to keep burning power on work the pool is not paying for.

## A card is missing from `list gpu`

- **NVIDIA:** does `nvidia-smi` show it? If not, it is the driver or the hardware (riser, cable, power), not
  the miner.
- **AMD on Linux:** an OpenCL loader must be installed (`ocl-icd` / `libOpenCL.so.1`) with the AMD OpenCL
  driver.
- A card turned off earlier with `config gpu disable` stays off: `config gpu` shows them, `config gpu enable all`
  turns them back on.
- Integrated graphics are hidden unless you ask (`igpu`).

## "No wallet address" at start

Give `wallet <address>` on the command line once; the miner remembers it for that coin after a successful run.

## The pool connects but nothing is accepted

- Wrong coin for the pool, or wrong port: many pools use a different port per coin or per algorithm.
- Login format: some pools want `WALLET.WORKER`, some want an account name (`user <name>`), some want a
  special password (`pass <...>`). `coin show <coin>` shows what the coin's default pool expects.
- TLS: if the pool's port is TLS-only, add `tls`; if it is plain, add `tcp`.

## Rejected shares

A few rejects an hour are normal (a share that arrived just after a new block). A steady stream means an
overclock that is too aggressive: run with `no oc`, and if that fixes it, `list tuning` shows the stored
setting to distrust.

## Hashrate lower than you expect

- Compare against the same card model, not a faster one, and against a number measured on this algorithm.
- Other programs using the GPU (a game, a browser with video, a remote-desktop session) cost hashrate.
- Thermal throttling: watch the temperature and clock in `list gpu` while mining.
- If another miner is faster on your card, tell us: an issue with both miners' versions, the card, the driver
  and both hashrates is exactly what we want to read.

## Antivirus removed the miner

See [SECURITY.md](../SECURITY.md). Verify the checksum, then add an exclusion for the miner's folder.

## Fans keep spinning after the miner stopped (AMD)

`./good-miner-cli device amd-restore` puts every AMD card back on its factory fan curve and tuning.

## Reporting a problem

Open an [issue](../../../issues/new/choose) with: `good-miner-cli version`, the output of `list gpu`, your
operating system and driver versions, the exact command line (remove your wallet), and the log file. For a
crash or a hang, also attach what `./good-miner-cli util trace` prints: it is the miner's flight recorder of
the last seconds before the stop.

## Running as a service

A minimal systemd unit (Linux). Adjust the folder, coin and wallet:

```ini
[Unit]
Description=good-miner
After=network-online.target
Wants=network-online.target

[Service]
WorkingDirectory=/opt/good-miner
ExecStart=/opt/good-miner/good-miner-cli no ui mine rvn wallet YOUR_ADDRESS
Restart=on-failure
RestartSec=30
User=root

[Install]
WantedBy=multi-user.target
```

Stop it with `systemctl stop`, which lets the miner restore fans and clocks; do not `kill -9` it.
