

# HD Wallets - BIP 32 Hierarchical Deterministic Wallets

## mnemonic

Some random words (12-24) which generate the [seed of a wallet](./#seed) - a sequence of random bytes.
SUPER SECRET SHIT!!!

The weird part, there are multiple algorithms for creating them (AND THEY ARE NOT COMPATIBLE):
- no mnemonic, just use the seed (old days)
- Electrum - good (first ones to implement it - [doc](https://electrum.readthedocs.io/en/latest/seedphrase.html))
- BIP39 - official but not as perfect as ElectrumMnemonics (standardized list of words [BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki))


If you have an Electrum Mnenomic, you are good to go.  
If you have a BIP39, you must know what software and version you used (or brute force it to find out).

## seed




## wallets

- Deterministic wallets (old)
- HD wallets - Hierarchical Deterministic wallets

HD let you have a single account with multiple addresses (and multiple accounts with multiple addresses).

Meaning, you can have 2 accounts inside a master one.  
Eg: your kid can have his own account inside your wallet.
He can only see his funds, but you can see both of them.

HD wallets let you generate a new address for each transaction.
Good for privacy (addresses and balances are public)

```
# only one-way, cannot be reversed
entropy (seed mnemonic) -> BIP39 Mnemonic -> BIP32 root key -> HD Wallet
entropy (seed mnemonic) -> ElectrumV2 Mnemonic -> ElectrumV2 root key -> HD Wallet
```
