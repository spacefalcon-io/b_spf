# Single Asset Staking Contract

**Highly recomemt to use Ububtu for solana development, there are lots issues while working with Mac and Window**
# Install
[Install Guide](https://book.anchor-lang.com/chapter_2/installation.html)

# Run local validator
On local development, you need to run solana local validator:
Run this commands on terminal: 

hr

```
mkdir ~/my-solana-wallet
solana-keygen new --outfile ~/my-solana-wallet/my-keypair.json # Remember this key
solana config get # Check solana config
solana config set --url http://127.0.0.1:8899
solana-test-validator
```
# Deploy code

Open a new terminal
```
git clone git@github.com:spacefalcon-io/b_spf.git
cd b_spf
rm -r -f target
```

Change `.env` file to `localnet`  
Change cluster provider in `Anchor.toml` to `localnet`  
Change wallet in `Anchor.toml` to `~/my-solana-wallet/my-keypair.json` 

## Run:

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

**Similiar setup for devnet, don't need to run validator**