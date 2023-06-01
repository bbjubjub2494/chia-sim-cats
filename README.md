### set up

```sh
git clone git@github.com:kimsk/chia-sim-cats.git my-chia-sim-cats
cd my-chia-sim-cats

```

#### PowerShell

```sh
$CHIA_SIM_ROOT=(pwd)
$env:CHIA_ROOT="$($CHIA_SIM_ROOT)/main"
$env:CHIA_KEYS_ROOT="$($env:CHIA_ROOT)/keys"
$CHIA_KEYS_ROOT=$env:CHIA_KEYS_ROOT

```

#### bash

```sh
export CHIA_SIM_ROOT="$(pwd)"
export CHIA_ROOT="$CHIA_SIM_ROOT/main"
export CHIA_KEYS_ROOT="$CHIA_ROOT/keys"

```

> make sure CHIA_ROOT and CHIA_KEYS_ROOT are set correctly before proceed

```sh
chia init --fix-ssl-permissions
for k in farmer maker taker; do
    chia keys add -l $k -f $CHIA_KEYS_ROOT/$k.txt
done

```

### start

```sh
chia dev sim --root-path $CHIA_SIM_ROOT start -w

```

### verify

```sh
chia show -s
chia keys show
chia wallet show -f 3682562999

```

```sh
❯ chia show -s
Network: simulator0    Port: 43994   RPC Port: 23005
Node ID: 450cdcb05b9e200211ff9f2713b08c51da2f78b111c04a035be4742b9c28be29
Genesis Challenge: eb8c4d20b322be8d9fddbf9412016bdffe9a2901d7edb0e364e94266d0e095f7
Current Blockchain Status: Full Node Synced

Peak: Hash: f6cc5e2ddf81a32ee691669c80d81bd919718d52d19d9d869d923073380bbfaf
      Time: Tue May 30 2023 15:41:23 +07                  Height:          3

Estimated network space: 25.956 MiB
Current difficulty: 1024
Current VDF sub_slot_iters: 1024

  Height: |   Hash:
        3 | f6cc5e2ddf81a32ee691669c80d81bd919718d52d19d9d869d923073380bbfaf
        2 | c08d327607e59e86d9ef6bc281a9403a33284b276adf2ae375f9196fe21e9ace
        1 | bd03b58cba7ebd698ec3f6c7fb2b2a97c0b7bb6212aac02bf7762159f8161bc7


❯ chia keys show
Showing all public keys derived from your master seed and private key:

Label: farmer
Fingerprint: 3682562999
Master public key (m): 95cd6b1b6e03f761d824d8d699c21148dee15234b7a895eef21c5cc6c1573f37e25c9ac66b08a634f727b029a8efd18b
Farmer public key (m/12381/8444/0/0): 8ecb4ece88bec575120fd914060ae704f6ffc26a5563ae10c5a7c3ae07b4e5e939d3d0c3d54dd11b4853879565d03881
Pool public key (m/12381/8444/1/0): 869a6526d17e266eb91071efd7dcda90e5260b9ab0b829fcc9c7ee385e0b894567fc2e5d64a03235b1aa8841cad46cdb
First wallet address: txch1ztlxh9x5kxapmyqaavvy0yfeksln8m6xfm46pw26fgdnjd5hewyq855klv

❯ chia wallet show -f 3682562999
Wallet height: 3
Sync status: Synced
Balances, fingerprint: 3682562999

Chia Wallet:
   -Total Balance:         21000002.0 txch (21000002000000000000 mojo)
   -Pending Total Balance: 21000002.0 txch (21000002000000000000 mojo)
   -Spendable:             21000002.0 txch (21000002000000000000 mojo)
   -Type:                  STANDARD_WALLET
   -Wallet ID:             1

CAT1:
   -Total Balance:         1000000000.0  (1000000000000 mojo)
   -Pending Total Balance: 1000000000.0  (1000000000000 mojo)
   -Spendable:             1000000000.0  (1000000000000 mojo)
   -Type:                  CAT
   -Asset ID:              657bdae0165c622f635374e539ef7e4632750ecc87541071478c21a7ba67096c
   -Wallet ID:             2

CAT2:
   -Total Balance:         1000000000.0  (1000000000000 mojo)
   -Pending Total Balance: 1000000000.0  (1000000000000 mojo)
   -Spendable:             1000000000.0  (1000000000000 mojo)
   -Type:                  CAT
   -Asset ID:              1b19cf566eb4e2bf9f563eac9b0263c1bd8b1007163da62436306699142fc71d
   -Wallet ID:             3

```

### Scenario
Offer is already in `./offer`.
Taker takes the offer:
```sh
chia wallet take_offer -f 1201765102 offer
```

See [Notes] to farm the transaction

maker checks their open offers. Expected behavior: 0 offers displayed
```sh
chia wallet get_offers -f 1984606926
```

# Notes

## config

- autofarm: `off`

> To farm manually, run

```sh
chia dev sim --root-path $CHIA_SIM_ROOT farm

```

> Or to farm automatically, run

```sh
chia dev sim --root-path $CHIA_SIM_ROOT autofarm on

```

## farming & prefarm

- Fingerprint: `3682562999`
- Reward address: `txch1a7wl6huvfck2x3rs5azynj7y65n8r4d33g63mh5d6ee4tzzh7j8s9w64sc`

## cat tails

- CAT1: `657bdae0165c622f635374e539ef7e4632750ecc87541071478c21a7ba67096c`
- CAT2: `1b19cf566eb4e2bf9f563eac9b0263c1bd8b1007163da62436306699142fc71d`
