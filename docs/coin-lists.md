# Your own coin list: importing CSV and JSON

The miner keeps its coins in a small database, `good.db`, in its own folder. You can add coins, change a
coin's default pool, or set your wallets for many coins at once by importing a file. Useful when you:

- want your wallet filled in for every coin, so `mine <coin>` needs no `wallet` word;
- prefer other pools than the defaults;
- run several rigs and want them all set up the same way: one file, one command on each rig;
- mine a coin that is not in the list yet but uses an algorithm good-miner supports
  (`good-miner-cli list algorithms`).

```text
good-miner-cli db import my-coins.csv      # CSV
good-miner-cli db import my-coins.json     # JSON, when the name ends in .json
good-miner-cli db export backup.csv        # write the current list out (or backup.json)
```

Both examples below were run against the release build exactly as written.

## CSV

The first line names the columns. Only three are required: `coin_name`, `coin_symbol` and `coin_algorithm`.
Add the others you need, in any order.

```csv
coin_name,coin_symbol,coin_algorithm,coin_hardware,stratum_host,stratum_host_tls,stratum_password,stratum_login_format,coin_default_wallet_address
Ravencoin,RVN,KawPow,GPU,stratum.ravenminer.com:3838,stratum.ravenminer.com:3839,x,WALLET.WORKER,YOUR_RVN_ADDRESS
Monero,XMR,RandomX,CPU,us2.monero.herominers.com:1111,,x,WALLET.WORKER,YOUR_XMR_ADDRESS
```

```text
good-miner-cli db import my-coins.csv
good-miner-cli coin show rvn        # check what went in
good-miner-cli mine rvn             # uses the pool and wallet from the file
```

### The columns you will use

| column | meaning |
| --- | --- |
| `coin_name` | full name |
| `coin_symbol` | ticker; with the algorithm it identifies the row |
| `coin_algorithm` | an algorithm name from `list algorithms` |
| `coin_hardware` | `GPU`, `CPU` or `CPU+GPU` |
| `stratum_host` | the pool, `host:port`, plain connection |
| `stratum_host_tls` | the pool's TLS `host:port`, if it has one |
| `stratum_tls_required` | `TRUE` if the pool accepts TLS only |
| `stratum_password` | the pool password, usually `x` |
| `stratum_login_format` | how the pool wants the login, e.g. `WALLET.WORKER` |
| `coin_default_wallet_address` | **your** wallet for this coin, used when you give none on the command line |
| `pool_username` | for pools that log in with an account name instead of a wallet |
| `solo_pool_non_tls`, `solo_pool_tls`, `solo_wallet` | the pool and wallet used with the `solo` word |

`good-miner-cli db export all.csv` writes every column, which is the easiest way to see them all.

### Rules worth knowing

- **A file changes only the coins it lists.** Coins it does not mention stay as they are. To remove a coin:
  `good-miner-cli coin remove <ticker>`.
- **A column you leave out is left alone** on coins the miner already has. A column you include with an
  empty cell clears that value.
- **One row per coin and algorithm.** A coin mined on two algorithms has two rows.
- Put quotes around a cell that contains a comma.
- Importing does not contact any pool. Test one with `good-miner-cli util validate-pool <host:port>`.

## JSON

The same information as a list of objects:

```json
{
  "version": 1,
  "coins": [
    {
      "name": "Ravencoin",
      "symbol": "RVN",
      "algorithm": "KawPow",
      "hardware": "GPU",
      "stratum_host": "stratum.ravenminer.com:3838",
      "stratum_host_tls": "stratum.ravenminer.com:3839",
      "password": "x",
      "login_format": "WALLET.WORKER",
      "default_wallet": "YOUR_RVN_ADDRESS"
    }
  ]
}
```

```text
good-miner-cli db import my-coins.json
```

One difference from CSV: **a JSON import only adds coins that are not there yet.** It does not change a coin
the miner already has. To change existing coins, use CSV. `good-miner-cli db export my-coins.json` shows the
exact shape for every coin you have.

## A command line still wins

Whatever the list says, words on the command line come first: `wallet <address>`, `url <host:port>`,
`user`, `pass`. After a successful run the miner also remembers that coin's pool and wallet
(`config show <coin>`, `config clear <coin>`).

## Keep your file private

A coin list with your wallets and pool account names in it is yours. Wallet addresses are not secret, but
there is no reason to post them; never put an exchange API key in a file you share.
