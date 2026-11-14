# CPU mining

RandomX coins (Monero and its relatives), GhostRider, Yespower and a few others mine on the CPU.

```text
./good-miner-cli mine xmr wallet <your address>          # all threads but one
./good-miner-cli mine xmr 8 wallet <your address>        # exactly 8 threads
./good-miner-cli mine xmr 0 wallet <your address>        # every thread
./good-miner-cli no gpu mine xmr wallet <your address>   # CPU only, leave the cards alone
```

By default the miner leaves one thread free so the machine stays usable. `cpu-threads <n>` before the command
does the same as the number after the coin.

## Getting full speed on RandomX

Two things roughly double RandomX speed, and both need administrator rights:

| | what | how |
| --- | --- | --- |
| Huge pages | large memory pages for the 2 GB dataset | Linux: run as root, the miner reserves them. Windows: run elevated once and reboot if it asks (the "Lock pages in memory" right takes effect at next sign-in). |
| MSR preset | CPU registers tuned for RandomX | Linux: root (the `msr` kernel module). Windows: elevated; the miner uses the PawnIO driver, which it will ask you to install if it is missing. |

The start-up lines say whether each one is active. To never touch them:

```text
./good-miner-cli config cpu disable msr          # never write CPU registers
./good-miner-cli config cpu disable hugepages    # ordinary memory
./good-miner-cli config cpu                      # show the settings
```

`no msr` and `no hugepages` do the same for one run. The registers are put back when the miner exits.

## Heat

CPU mining pauses if the CPU stays above 110 C (`cpu-temp-limit <C>` to change it), and stops the whole run
if it crosses its thermal backstop. A desktop cooler that is fine for games can be too small for all-core
mining around the clock: watch the temperature for the first hour.
