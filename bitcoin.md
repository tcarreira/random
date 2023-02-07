# Bitcoin


# HD Wallets - BIP 32 Hierarchical Deterministic Wallets



## mnemonic (sometimes also called seed)

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



### Derivation Path

In hierarchical deterministic wallets (BIP32),
a derivation path is a sequence of fields or levels through which a wallet
organizes coins in a multi-currency, multi-account, and multi-address system.
According to BIP44, this hierarchy consists of five levels,
in addition to the master extended private key (`xpriv`) represented by `m`.
Derivation paths for the master extended public key (`xpub`) use `M`.
Double-check what fields your wallet uses in our chart above,
as BIP44 has been implemented inconsistently!

```
m / purpose’ / coin_type’ / account’ / change / address_index
```

- **Purpose**: This field, which was added through BIP43, indicates which standard the derivation path follows. Possibilities include 0 or 44 referring to the default BIP44 P2PKH / ‘1’ legacy addresses, 45 referring to BIP45 P2SH multi-party multi-signature wallets (proposed), 47 referring to BIP47 reusable payment codes (draft), 48 referring to hardware multisignature wallets (no BIP or standard proposal), 49 referring to BIP49 P2WPKH-nested-in-P2SH / ‘3’ SegWit addresses, or 84 referring to BIP84 P2WPKH / ‘bc1’ native SegWit addresses. Some wallets support more than one (for example, many wallets now have both the legacy and wrapped or native SegWit address types).
- **Coin Type**: This field indicates which cryptocurrency is being used in a multi-currency wallet. All coins, including testnet bitcoin, are assigned a constant number. For example, a derivation path for a Monero (XMR) account would be m/44'/128'. Note that BIP45 would designate this level as the ‘Cosigner Index’ instead.
- **Account**: This field, in a multi-account wallet, indicates the identity or collection of addresses, which allows users to segregate funds for different things (ex. savings, donations). Note that BIP45 would not include this field. BIP47 would designate this level as ‘Identity’, though it is equivalent to ‘Account.’
- **Change**: This field, if the constant 0 is present, indicates “external chain” (regular) addresses; if the constant 1, indicates “internal chain” or change addresses. Note that BIP47 would designate this level for the notification keys and ephemeral payment codes.
- **Address Index**: This field indicates the specific address number in a sequence, within an account.


https://walletsrecovery.org/



- [generate bip39 by hand](./extras/bip39-by-hand-backup)
<!-- https://gist.github.com/atoponce/44d50f0bbcd06811c8c8eeef13b79585 -->

- bitcoin seed xor: https://seedxor.com/

- How To Make Your Own Crypto Steel Recovery Seed Backup for Only $3.35
https://johnchow.com/how-to-make-your-own-crypto-steel-recovery-seed-backup/

- frontend tool to generate and check mnemonics, etc..
  https://iancoleman.io/bip39/



- BIP32 - Hierarchical Deterministic Wallets
- BIP39 - Mnemonic code for generating deterministic keys
- BIP43 - Purpose Field for Deterministic Wallets
- BIP44 - Multi-Account Hierarchy for Deterministic Wallets
- BIP49 - Derivation scheme for P2WPKH-nested-in-P2SH based accounts
- BIP84 - Derivation scheme for P2WPKH based accounts
- BIP173 - Base32 address format for native v0-16 witness outputs
- SLIP44 - Registered coin types for BIP-0044

*[BIP]: Bitcoin Improvement Proposal
*[BIP32]: Hierarchical Deterministic Wallets
*[BIP39]: Mnemonic code for generating deterministic keys
*[BIP43]: Purpose Field for Deterministic Wallets
*[BIP44]: Multi-Account Hierarchy for Deterministic Wallets
*[BIP49]: Derivation scheme for P2WPKH-nested-in-P2SH based accounts
*[BIP84]: Derivation scheme for P2WPKH based accounts
*[BIP173]: Base32 address format for native v0-16 witness outputs
*[SLIP44]: Registered coin types for BIP-0044
