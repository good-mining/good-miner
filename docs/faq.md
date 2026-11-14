# FAQ

## About the miner

**What is good-miner?** A miner written from scratch in Rust: one program for NVIDIA, AMD and Intel graphics
and CPUs, with its own dashboard, protection for your hardware, and a published fee.

**Why is it closed source?** The developer fee is how the work is paid for, and an open miner's fee is removed
by someone within a day. What we give instead: checksums and a changelog for every release, a fee published
per algorithm and printed by the miner itself, and public answers here.

**How much is the fee? Can I turn it off?** Between 0.65 % and 1.5 % depending on the algorithm; the table is
in the [README](../README.md#developer-fee) and `good-miner-cli list algorithms` prints it for your copy. It
cannot be turned off. `stats fee` shows what your rig has contributed.

**Does it send you anything besides fee hashrate?** No. It connects to the pool you chose, and to public price
and network-statistics sources for the dashboard's earnings figures. It collects no personal data and needs
no account.

## Safety

**My antivirus flags it.** Antivirus products flag most miners because mining malware exists. Check the
checksum against the release page ([SECURITY.md](../SECURITY.md)); if it matches, it is our file.

**Will it damage my hardware?** Mining runs hardware hot and hard, with any miner. good-miner pauses a card
or the CPU that gets too hot, stops rather than keep sending bad work, and puts fans and clocks back when it
exits. It will try a memory overclock on NVIDIA cards unless you say `no oc`
([cards and cooling](gpus-and-cooling.md#overclock)). Your cooling and your power supply are still yours to
get right.

**Does it need administrator or root rights?** Not to mine on GPUs. It needs them for fan control, AMD power
tuning and the CPU tuning that doubles RandomX speed.

## Mining

**Which coin should I mine?** `util profit` ranks them for your hardware and power price, and `mine auto`
follows the ranking ([dashboard](dashboard.md#profit-and-mine-auto)).

**Is it faster than `<another miner>`?** On some coins and cards it matches the best miner we could test, and
on some it is behind. The README's table says which, with dates. We would rather you run the faster miner for
your card than believe a claim.

**Pool or solo?** A pool pays a little all the time. Solo (`solo`) pays a whole block when you find one and
nothing otherwise; with a small rig on a large coin that can mean months. Solo makes sense when your rig is
a visible fraction of the coin's network.

**Does it work on Intel graphics?** Yes, experimentally, through OpenCL: tested on Core Ultra integrated
graphics ([details](gpus-and-cooling.md#intel-graphics)). Add `igpu` to mine on an integrated GPU.

**Can I mine two coins at once?** Yes: different coins on different cards, or a CPU coin beside a GPU coin
([cards and cooling](gpus-and-cooling.md#two-coins-on-one-rig)).

**Can you add `<coin>`?** Open a coin request. We need the coin's node source, a working explorer, a pool,
and an algorithm we can verify against the coin's own software.

**I found a bug.** Thank you. [Troubleshooting](troubleshooting.md#reporting-a-problem) lists what to attach.
