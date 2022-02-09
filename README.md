# Single Asset Staking Contract
# Install
[Install Guide](https://book.anchor-lang.com/chapter_2/installation.html)
# Local Development Setup

**Highly recomemt to use Ububtu for solana development, there are lots issues while working with Mac and Window**

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

# Testnet Development and create pool 

### Create Keypair
```
solana-keygen new --outfile ~/my-solana-wallet/my-keypair.json # Remember this key
```

### Set config to testnet
```
solana config get # Check solana config
solana config set --url https://api.testnet.solana.com
```

## Deploy code

Open a new terminal
```
git clone git@github.com:spacefalcon-io/b_spf.git
cd b_spf
rm -r -f target
```

Change `.env` file to `testnet`  
Change cluster provider in `Anchor.toml` to `testnet`  
Create `jeet.json` file copy `~/my-solana-wallet/my-keypair.json` to `jeet.json`

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
Change the provider.cluster variable in Anchor.toml to testnet.
```
anchor deploy
anchor test
```

Current program id on testnet: 
```
Deploying workspace: https://api.testnet.solana.com
Upgrade authority: /home/peter/.config/solana/id.json
Deploying program "reward-pool"...
Program path: /home/peter/Desktop/SpaceFalcon/b_spf/target/deploy/reward_pool.so...
Program Id: 9pA7mQhCRMNciuQcazXMesB3SsYmBCQjT5qYcrDgUCZF

Deploy success
```
Copy program Id `9pA7mQhCRMNciuQcazXMesB3SsYmBCQjT5qYcrDgUCZF` to create pool

## Create pool and fund
Create new file in `src` folder `testnet-config.json`

### [Create spl token and mint](https://spl.solana.com/token#example-creating-your-own-fungible-token)

Copy token and account address and paste to `testnet-config.json`
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

If encounter error check the version of `@project-serum` and `@solana` in `package.json`, may need update.

Run:

```
node src/createPool.js 
Pool:  4mYsk6S5HfPPrybtGfdTyKdWywfJWGs7MC3mc62yVg26
StakingVault:  8GVEgNMRm1WLg3FE32P5bKYcw1gp5eXYVeEyFqS3LKFh
rewardVault:  CewdfKAKpjkXjYVSFmnbhez8yxeFZdj4yfUmXpBBkS9
Pool Signer:  63ELCFgJiY6nNukUFu5eHVNP1YGx711AMC5MvZfbyAHP
Pool Nonce:  254
Tx:  5dsZQDNytkdkVm6eWfRz9r6mg7Jeqf4cs6LFguEZiSAEN3gK1wTxRBdAnREafQ2B2ioS5R2yTs8k2AEmfgTh4zcQ
Add new pool info...

```
Run:
```
node src/fund.js 
Tx:  dczKxy5mYAUaxBarNVKENejvdsik3RtbUcwQjPvKNmc9R7PxfUXMndz27G3wySu8Kyz3goJQvPvoA7qVqyHZx2H
```