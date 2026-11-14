# Getting started

From download to your first accepted share. Ten minutes on a machine with working GPU drivers.

Commands are written as on Linux (`./good-miner-cli`). On Windows, write `good-miner-cli.exe` in a Command
Prompt or PowerShell window opened in the miner's folder.

## 1. Before you download

| you need | details |
| --- | --- |
| A 64-bit x86 PC | Windows 10 or 11, or a current Linux |
| A wallet address | for the coin you want to mine. Create it with the coin's own wallet or an exchange deposit address. The miner never creates or holds wallets. |
| GPU drivers | **NVIDIA:** a current driver (the release notes give the minimum). **AMD:** current Adrenalin on Windows; on Linux the amdgpu driver with an OpenCL loader (`ocl-icd`), and ROCm's `hip-runtime-amd` for the fastest RX 9070 kernels. **CPU mining needs no driver.** |
| Room for the DAG | Ethash-family and KawPow-family coins need 4 to 8 GB of GPU memory; a few coins need more. The miner says so at start instead of failing later. |

## 2. Download and check

1. On the [Releases](../../../releases/latest) page pick the archive for your system:
   - `v3` if your CPU has AVX2 (Intel Haswell from 2013, AMD Ryzen, or newer). Most machines.
   - `v2` for older CPUs, including the Celerons and Pentiums common in GPU rigs.
2. Check the SHA-256 checksum against the one on the release page ([how](../SECURITY.md)). Do not skip this:
   fake miners are a common way to steal hashrate.
3. Unpack it into a folder of its own and keep everything in that folder together. Beside the miner are the
   GPU kernel compilers it loads at start; without them NVIDIA coins stop at once with exit code 84.
4. Linux: `chmod +x good-miner-cli`.

## 3. See what the miner sees

```text
./good-miner-cli version          # the build you have
./good-miner-cli list gpu         # every card: number, model, memory, temperature
./good-miner-cli list cpu         # CPU model, cores, features
./good-miner-cli util nvrtc       # NVIDIA only: can this install build its kernels?
```

The numbers `list gpu` prints (0, 1, 2 ...) are the ones every other command uses. If a card is missing here,
fix the driver before going further ([troubleshooting](troubleshooting.md)).

## 4. Pick a coin

```text
./good-miner-cli list coins             # every coin in this release
./good-miner-cli list coins kawpow      # only one algorithm
./good-miner-cli coin show rvn          # one coin: algorithm, hardware, its default pool
```

[coins.md](coins.md) lists every coin with a ready command line.

## 5. Mine

Give the coin and your own wallet address:

```text
./good-miner-cli mine rvn wallet <your RVN address>
```

That uses the coin's default pool from the coin list. To choose the pool yourself:

```text
./good-miner-cli mine rvn url stratum.ravenminer.com:3838 wallet <your address> pass x
```

After the coin, words can come in any order. The useful ones:

| word | what it does |
| --- | --- |
| `wallet <address>` | where the pool pays you |
| `url <host:port>` | the pool, instead of the coin's default |
| `user <name>` / `pass <password>` | for pools that want an account name or a special password |
| `tls` / `tcp` | encrypted or plain connection, when the pool offers both |
| `gpu` / `cpu` | mine on that hardware only |
| `solo` | mine on the coin's solo pool: you keep the whole block, and get nothing between blocks |

The miner remembers the pool and wallet of your last successful run of each coin. Next time,
`./good-miner-cli mine rvn` is enough. `config show rvn` shows what is saved, `config clear rvn` forgets it,
and `config set rvn url <host:port> wallet <address>` sets it without mining.

## 6. What you should see

In order, within the first minute or two:

1. **The plan:** which cards and how many CPU threads will mine, the pool, and the developer fee for this
   algorithm.
2. **Connection:** the pool accepts the login and sends the first job.
3. **Preparation**, for some algorithms: building the DAG or dataset. One to two minutes on Ethash and KawPow
   coins, a few seconds on most others.
4. **Hashrate lines** per device, and **shares**: `accepted` is what you are paid for. The first accepted
   share can take from seconds to several minutes, depending on the pool's difficulty.

The first time a card mines an algorithm, the miner may spend a few minutes finding that card's best memory
overclock, then stores it. Write `no oc` before `mine` if you never want clocks touched, or `no octune` to
skip only the search ([cards and cooling](gpus-and-cooling.md)).

Stop with **Ctrl+C**. The miner puts fans and clocks back as it found them before it exits; give it the few
seconds it needs rather than closing the window.

## 7. Watch it

- **Console:** the default. Plain lines, good for logs and remote shells.
- **Terminal UI:** write `ui` before `mine` (`./good-miner-cli ui mine rvn ...`), or `config set ui` to have it
  every time.
- **Web dashboard:** open `http://localhost:4040` in a browser on the mining machine. To use a phone, run
  `./good-miner-cli util pair` and follow what it prints ([dashboard](dashboard.md)).
- **Log file:** `logs/good-miner.log.<date>` in the miner's folder. Attach it to any bug report.

## 8. Keep it running

`mine` starts a small watcher called **buddy** beside the miner. If the miner crashes or a card hangs, buddy
restarts it. If the problem cannot be fixed by restarting (wrong coin name, no wallet, a broken driver, too
many rejected shares), buddy stops and tells you why, with an exit code ([troubleshooting](troubleshooting.md)).

To start mining when the machine boots:

- **Linux:** a systemd service that runs the same command line, as root (root is needed for fan control and
  CPU tuning). An example unit is in [troubleshooting](troubleshooting.md#running-as-a-service).
- **Windows:** Task Scheduler, "At log on", "Run with highest privileges", with the same command line and
  "Start in" set to the miner's folder.
- **HiveOS:** see [hiveos.md](hiveos.md).

## 9. Next

- More than one card, mixed cards, temperatures, fans, overclock: [gpus-and-cooling.md](gpus-and-cooling.md)
- CPU mining, huge pages: [cpu-mining.md](cpu-mining.md)
- Let the miner pick the most profitable coin: [dashboard.md](dashboard.md#profit-and-mine-auto)
- Every command and word: [commands.md](commands.md)
