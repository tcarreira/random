# Crypto - Bitcoin

Vou explicar as coisas especificamente para Bitcoin,
embora muitas das coisas possam ser extrapoladas para outras crypto moedas.

Todas as crypto moedas funcionam de uma forma virtual.
A Bitcoin é uma base de dados descentralizada, da qual existem inúmeras cópias.
Cada transação/movimentação tem que ser aceite de forma concensual por toda a rede.
Essas operações são aceites e validadas usando conceitos de matemática e criptografia,
que tornam a Bitcoin um meio de transferência de valor.
Além disso, toda a base de dados é pública e transparente,
o que não permite que alguma entidade central tenha controlo sob qualquer bitcoin.


## Conceitos básicos

- As bitcoins são guardadas numa [Wallet (Carteira)](#wallet).
- A forma de aceder uma Wallet é através da [Seed (semente)](#seed).
- Uma seed que pode ser criada através de [Mnemonics (Mnemónicas))](#mnemonics).
- Uma wallet tem a capacidade de criar um par de **chaves** privada e pública \*
  - A chave privada serve para movimentar as bitcoins da carteira
  - A chave pública permite criar um endereço para receber bitcoins
- As wallets mais recentes são do tipo Hierarchical Deterministic Wallet - [HD Wallet](#hd_wallet) (Carteira Hierárquica Determinística):
  - pode gerar inúmeros pares de **chaves**
  - aumenta a privacidade da carteira



# Wallet

A função de uma carteira é gerir os bitcoins.
Existem vários tipos de carteiras:

- [Paper Wallet](#paper-wallet) - carteira em papel
- [Simple Wallet](#simple-wallet) - carteira simples
- [Deterministic Wallet](#deterministic-wallet) - carteira determinística
- [Hierarchical Deterministic Wallet (WD-Wallet)](#hierarchical-deterministic-wallet-wd-wallet) - carteira hierárquica determinística

## Paper Wallet

Na verdade, este não é um tipo de carteira, mas antes uma materialização offline de uma dos outros tipos de carteiras.

## Simple Wallet

Este é o conceito mais básico de uma carteira, a qual é composta por uma chave pública e uma chave privada.
A chave pública tem poderes limitados, como dar acesso de leitura ao endereço para envio de bitcoins.
A chave privada tem poderes absolutos sobre os fundos da carteira, é a chave usada para poder transferir bitcoins.

## Deterministic Wallet

Esta é uma variação sobre a anterior, na medida em que a mesma chave privada consegue derivar vários endereços públicos.
Isto permite que a mesma carteira possa ter inúmeros endereços para envio de bitcoins.
Assim é possível indicar diferentes endereços bitcoin efémeros que na verdade estão sob custódia da mesma carteira.
Desta forma, um endereço bitcoin efémero, permite-me enviar fundos para a carteira,
mas não me permite consultar todos os fundos dos outros endereços da mesma carteira.
Isto apresenta vantagens a nível da privacidade (lembrando que todas as transações bitcoin são públicas).

## Hierarchical Deterministic Wallet (WD-Wallet)

Além de permitirem criar vários endereços públicos a partir da mesma seed,
estas também permitem gerar chaves privadas, que por sua vez pode gerar mais chaves privadas.
Assim, a partir de uma seed, é possível gerar uma árvore hierárquica de chaves,
na qual cada par de chaves têm total autonomia sob os seus filhos,
mas não tem visibilidade sobre as suas chaves pais.

Isto permite vários casos de uso, sendo um exemplo numa grande empresa.
A [Master Private Key](#master-private-key) da empresa toda pode criar chaves privadas para cada um dos seus departamentos.
Estes podem gerir o seu departamento de forma independente, e até gerar novas chaves para algum sub-departamento
(e podemos continuar recursivamente).<br>
A [Master Private Key](#master-private-key) tem total controlo sobre todos os seus filhos (e filhos de filhos).

Existe também uma [Master Public Key](#master-public-key) que permite derivar todas as chaves públicas filhos.
Isto permite ter sistema (eg: site/serviço) que pode gerar e consultar inúmeros endereços públicos efémeros
para pagamento em bitcoin e verificação da transação efetuada, mas não tem controlo sobre os fundos -
apenas a chave privada o pode fazer.
Eg: uma loja gera um endereço para pagamento de uma encomenda e pode verificar quando a transação foi efetuada,
mas não pode movimentar esses fundos.

