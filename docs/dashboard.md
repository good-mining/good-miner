# Dashboard, profit and the API

## The web dashboard

While a miner runs, open `http://localhost:4040` on that machine. It shows every good-miner instance on the
rig: hashrate and shares per device, temperatures and power, earnings, each coin's network figures, and a
profit board. It can stop a lane or switch coin.

**From a phone or another computer:**

```text
./good-miner-cli util pair
```

prints a one-time 6-digit code (valid 5 minutes) and the link to open. The device then stays paired for 90
days. If the dashboard answers on the mining machine only, the same command says what to change.

**Without mining:** `./good-miner-cli util api` serves the dashboard and the history from the miner's database
when no miner is running. Beside a running miner give it another port: `util api 4041`.

Ports: 4040 is the rig's dashboard. Each miner instance also serves its own API on the first free port from
4041 (`api-port <n>` to choose).

## Profit and `mine auto`

The miner can rank coins for your hardware: your measured hashrate, times each coin's live network figures
and price, minus your power cost.

1. Measure your cards once per coin you care about: `./good-miner-cli util benchmark rvn`.
   `stats hashrates` shows what is stored.
2. Tell it your electricity price: `./good-miner-cli config set kwh 0.18` (dollars per kWh; 0.12 if unset).
   For a truer result also set the rig's real draw: `config set gpu-watts 700`, `config set cpu-watts 120`.
3. See the ranking: `./good-miner-cli util profit`.
4. Let it choose: `./good-miner-cli mine auto` mines the most profitable coin you have a wallet for.
   `mine auto cpu` or `mine auto gpu` limits it to that hardware; `auto-interval <minutes>` sets how often it
   re-checks and switches.

`mine auto` only switches to coins you have set a wallet for (`config set <coin> wallet <address>`).

Read the ranking as an estimate. Prices and difficulty move, pools pay with luck, and a coin that looks best
for an hour may not be over a week.

## For scripts and mining systems

The same data is served as JSON under `/api/v1/`; HiveOS reads `/api/v1/hiveos`. `list network <coin>` and
`list market` print the stored history in the console.
