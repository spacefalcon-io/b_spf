# Single Asset Staking Contract
# Install
[Install Guide](https://book.anchor-lang.com/chapter_2/installation.html)
# Local Development Setup

## Run local validator
On local development, you need to run solana local validator:
Run this commands on terminal:

```
mkdir ~/my-solana-wallet
solana-keygen new --outfile ~/my-solana-wallet/my-keypair.json # Remember this key
solana config get # Check solana config
solana config set --url http://127.0.0.1:8899
solana-test-validator
```
## Deploy code

Open a new terminal
```
git clone git@github.com:spacefalcon-io/b_spf.git
cd b_spf
rm -r -f target
```

Change `.env` file to `localnet`
Change cluster provider in `Anchor.toml` to `localnet`
Change wallet in `Anchor.toml` to `~/my-solana-wallet/my-keypair.json`

### Run:

Run anchor build. Your program keypair is now in target/deploy. Keep this secret. You can reuse it on all clusters.
Run
```
solana address -k target/deploy/reward_pool-keypair.json
```
Copy the address into your declare_id! macro at the top of lib.rs.
Run
```
anchor build
```
Change the provider.cluster variable in Anchor.toml to devnet.
```
anchor deploy
anchor test
```

## Create pool and fund
Create new file in `src` folder `localnet-config.json`

### [Create spl token and mint](https://spl.solana.com/token#example-creating-your-own-fungible-token)

Copy token and account address and paste to `testnet-config.json`.
Example:
```
{
  "rewardPoolProgram": "9pA7mQhCRMNciuQcazXMesB3SsYmBCQjT5qYcrDgUCZF",
  "cysMint": "8KzpuPPugk3yntu3CK57RiVEq46jfcNBTmaLM6qqwT5p",
  "cysTokenAccount": "cdxYaCfxhquhtSeacHcPjANQQL6rNtRGDJndZdEhyvr",
  "pools": []
}
```

```
yarn install
```
or
```
npm install
```

Run:

```
node src/createPool.js

```
Run:
```
node src/fund.js
```