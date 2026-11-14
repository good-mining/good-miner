# Cards, temperatures and overclock

## Choosing which cards mine

`list gpu` numbers the cards. Use those numbers:

```text
./good-miner-cli no gpu 0,1 mine rvn ...        # this run: every card except 0 and 1
./good-miner-cli mine krgn gpu 0 ...            # this run: only card 0
./good-miner-cli config gpu disable 3           # card 3 off on every run (the miner never opens it)
./good-miner-cli config gpu enable all          # every card on again
./good-miner-cli config set gpu 0,2             # only cards 0 and 2 mine, on every run
./good-miner-cli config gpu                     # show which are on and off
```

A card turned off with `config` is remembered by its slot in the machine, not by its number, so it stays off
even when numbers shift after you add or remove a card.

Integrated graphics are left out unless you ask: `igpu` for one run, `config set igpu` for every run.

## Intel graphics

**Experimental Intel SPIR-V support.** Intel GPUs mine through OpenCL, with kernels built as SPIR-V. It is
the newest hardware path and the least tested.

| | |
| --- | --- |
| Tested on | the integrated Arc graphics of a Core Ultra (Arrow Lake) processor, Windows |
| Mining, with accepted shares | Qubitcoin (qhash): 147 MH/s |
| Checked hash-for-hash against the CPU reference | Verthash (Vertcoin), Equihash (Zcash) |
| Known not to work yet | Octopus (Conflux) |
| Everything else | has an Intel build in the release and has not been proven on Intel hardware by us |

- **Discrete Arc cards** should work the same way. We have not had one to test, so we do not claim it.
- An integrated GPU shares the system's memory and power with the CPU: expect modest rates, and expect CPU
  mining on the same machine to slow it down. It is opt-in for that reason (`igpu`).
- The miner does not control fans or clocks on Intel GPUs.
- If an algorithm fails or gets its shares rejected on your Intel GPU, please report it with the log.

## Two coins on one rig

```text
./good-miner-cli mine prl gpu 1,2 rvn ...       # PRL on cards 1 and 2, RVN on the rest
./good-miner-cli mine xmr cpu ...               # CPU only, in a second window beside a GPU miner
```

Several good-miner instances can share a rig as long as each has its own cards. The dashboard on port 4040
shows all of them together.

## Temperature protection

Always on, no setup:

| guard | default | change it with |
| --- | --- | --- |
| Pause a GPU that stays too hot | 90 C | `temp-limit <C>` |
| Resume it once cooled | 78 C | `temp-resume <C>` |
| Pause CPU mining | 110 C | `cpu-temp-limit <C>` |

A card that reports its own shutdown temperature is also paused 10 C short of it. A paused card resumes by
itself; the rest of the rig keeps mining.

## Fans

- **NVIDIA:** fans stay on the card's automatic curve.
- **AMD:** while mining, the miner runs a mining fan curve and puts the card's own back when it stops.
  `fan <percent>` holds a fixed speed (20 to 100) for a run; `no fan` leaves fans completely alone.
- If an AMD card is left on the mining curve after a crash or power cut (fans spinning at idle), run
  `./good-miner-cli device amd-restore`.

On Linux, fan and clock control need root.

## Overclock

The miner changes a card's clocks or power only in two cases: you asked, or the one-time memory tune.

- **Memory tune (NVIDIA).** The first time a card mines an algorithm that benefits from faster memory, the
  miner searches for that card's best memory offset: the fastest setting that still has an error-free setting
  above it. It stores the result per card and algorithm and applies it on later runs. It is put back to stock
  when the miner exits.
  - `list tuning` shows every stored setting and what it measured.
  - `no octune` skips the search (stored settings still apply).
  - `no oc` applies no overclock at all.
  - `util oc-autotune` runs the search on demand.
- **AMD power and junction (Linux).** `amd-governor` (or `config set amd-governor`) steers each AMD card's
  power cap to hold a junction temperature; `config set amd-junction-target 92` sets the target.
  `undervolt <mV>` (0 to 250) applies for the session, with the governor only.

If you overclock with another tool (MSI Afterburner, your mining OS), write `no oc` so two tools do not fight
over the same card.

## Cards with 8 GB

8 GB cards are supported. Where a coin's dataset has outgrown 8 GB, the miner says so at start and names the
cards it leaves out; it does not start and then fail.
