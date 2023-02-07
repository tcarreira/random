# Crypto - Bitcoin

## Resumo

Todas as "instruções" referentes a Bitcoin estão descritas em BIPs (Bitcoin Improvement Proposals). O BIP 44 define um padrão para gerar endereços de Bitcoin. O BIP 49 define um padrão para gerar endereços de Bitcoin compatíveis com SegWit. O BIP 84 define um padrão para gerar endereços de Bitcoin nativos SegWit. O BIP 141 define o formato de transação SegWit. O BIP 173 define o formato de endereço Bech32.



## Conceitos Teóricos
Vou explicar as coisas especificamente para Bitcoin,
embora muitas das coisas possam ser extrapoladas para outras crypto moedas.

Todas as crypto moedas funcionam de uma forma virtual.
A Bitcoin é uma base de dados descentralizada, da qual existem inúmeras cópias.
Cada transação/movimentação tem que ser aceite de forma concensual por toda a rede.
Essas operações são aceites e validadas usando conceitos de matemática e criptografia,
que tornam a Bitcoin um meio de transferência de valor.
Além disso, toda a base de dados é pública e transparente,
o que não permite que alguma entidade central tenha controlo sob qualquer bitcoin.


### Conceitos básicos

- As bitcoins são guardadas numa [Wallet (Carteira)](#wallet).
- A forma de aceder uma Wallet é através da [Seed (semente)](#seed).
- Uma seed que pode ser criada através de [Mnemonics (Mnemónicas))](#mnemonics).
- Uma wallet tem a capacidade de criar um par de **chaves** privada e pública \*
  - A chave privada serve para movimentar as bitcoins da carteira
  - A chave pública permite criar um endereço para receber bitcoins
- As wallets mais recentes são do tipo Hierarchical Deterministic Wallet - [HD Wallet](#hd_wallet) (Carteira Hierárquica Determinística):
  - pode gerar inúmeros pares de **chaves**
  - aumenta a privacidade da carteira


### Wallet

A função de uma carteira é gerir os bitcoins.
Existem vários tipos de carteiras:

- [Non Deterministic Wallet](#non-deterministic-wallet) - carteira não determinística
- [Sequencial Deterministic Wallet](#sequencial-deterministic-wallet) - carteira determinística sequencial
- [Hierarchical Deterministic Wallet (WD-Wallet)](#hierarchical-deterministic-wallet-wd-wallet) - carteira hierárquica determinística
- [Multi-Signature Wallet](#multi-signature-wallet) - carteira multi-assinatura


#### Non-Deterministic Wallet

Carteira Não Determinística

Este é o conceito mais básico de uma carteira, a qual é composta por uma chave pública e uma chave privada.
A chave pública tem poderes limitados, como dar acesso de leitura ao endereço para envio de bitcoins.
A chave privada tem poderes absolutos sobre os fundos da carteira, é a chave usada para poder transferir bitcoins.
Todos os endereços gerados pela carteira têm que ser guardados e feito um backup de todos eles.

#### Sequencial Deterministic Wallet

Carteira Determinística Sequencial

Esta é uma variação sobre a anterior, na medida em que a mesma chave privada consegue derivar vários endereços públicos.
Isto permite que a mesma carteira possa ter inúmeros endereços para envio de bitcoins, mantendo apenas o backup da chave raiz.
Assim é possível indicar diferentes endereços bitcoin efémeros que na verdade estão sob custódia da mesma carteira.
Desta forma, um endereço bitcoin efémero, permite-me enviar fundos para a carteira,
mas não me permite consultar todos os fundos dos outros endereços da mesma carteira.
Isto apresenta vantagens a nível da privacidade (lembrando que todas as transações bitcoin são públicas).

#### Hierarchical Deterministic Wallet (WD-Wallet)

Carteira Hierárquica Determinística

Definida pelo BIP32
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

#### Multi-Signature Wallet

Carteira Multi-assinatura

Definida pelo BIP11, esta carteira permite que um endereço bitcoin tenha mais do que uma chave privada associada.
Existem vários esquemas de multi-assinatura. Exemplos:
- 2-3 - existem 3 chaves privadas, e são necessárias 2 para movimentar fundos
- 2-2 - existem 2 chaves privadas, e são necessárias 2 para movimentar fundos
- 3-5 - existem 5 chaves privadas, e são necessárias 3 para movimentar fundos
- etc...

### Wallet Storage

Também existem diversas formas de guardar wallets:
- [Non-Custodial Wallet](#non-custodial-wallet) - Carteira não custodiada
- [Paper Wallet](#paper-wallet) - carteira em papel
- [Hardware Wallet](#hardware-wallet) - Carteira Eletrónica Física
- [Software Wallet](#software-wallet) - Carteira de Software

#### Non-Custodial Wallet

Carteira não custodiada

Exemplos como a Binance e a Coinbase, são carteiras não custodiadas.
A nossa conta dá acesso à carteira, mas na verdade é a empresa que tem a carteira.
As exchanges (que normalmente disponibilizam uma carteira para uso)
são muito úteis para trocar dinheiro "normal" por criptomoedas,
mas há vários relatos de empresas deste tipo que desapareceram com os fundos dos seus clientes.

> Not your keys, not your crypto - "Não são as tuas chaves, não é a tua criptomoeda"


#### Paper Wallet

Carteira em papel

Na verdade, este não é um tipo de carteira, mas antes uma materialização offline de uma.
Foca-se na segurança removendo qualquer acesso eletrónico às chaves públicas.
Advoga ser mais seguro porque em papel não existem vírus que possam roubar chaves.

#### Hardware Wallet

Carteira Eletrónica Física

São as carteiras mais seguras para operar crypto, implementando um ou vários tipos de carteiras enumerados em seguida.
Noemalmente estão bem protegidas (eg: com pin) e "autodestroem-se" caso alguém tente aceder às chaves com brute-force.
Elas fazem um papel fundamental em garantir segurança mesmo para os menos experientes.



## Conceitos técnicos

### Criar uma HD Wallet

1. criar entropia (o aleatório que faz com que seja impossível descobrir as chaves da carteira)
2. transformar a entropia em palavras (mnemonics)
3. transformar as palavras (mnemonics) em seed
4. transformar a seed em chave base
5. transformar a chave base em chaves pública e privada (master keys)
6. recursivamente derivar chaves/endereços filhos a cada nova transação
   1. derivar a chave pública numa chaves pública filha
   2. derivar a chave privada num par público+privado filho
7. transformar a chave pública em endereço

## Problemas e complicações

### Versões de mnemonics

As palavras (mnemonics) são o que nós usamos para aceder a todos os fundos da carteira.
É importante que estas não seja mantida em absoluto segredo;
mas igualmente importante que esta consiga ser recuperada.

Mas na verdade, aquilo que é a chave da carteira é a seed;
e a forma de transformar palavras numa **seed** é um standard com algumas nuances.
O standard que define os algoritmos envolvidos é o BIP39, mas nem todos os softwares o implementam.
O exemplo mais claro e mais usado é o Electrum, que usou mnemonics antes de existir o BIP39.

A conlusão é que é necessário saber qual o software e versão usada para criar as mnemonics.

### Segwit???


### Derivation Path

As derivações de uma HD-Wallet são dados pelo caminho de derivação (derivation path).
Este define um index e um nível de uma determinada chave.
Exemplos de derivation path: `m/0'`, `m/1/0`, `M/1`

- Começa com `m` para private master key ou `M` para public.
- seguido de um `/` para indicar um sub-nível hierárquico. Pode haver vários níveis.
- seguido de um index que identifica uma carteira naquele nível (de 0 a ~infinito)
- opcionalmente, um `'` que identifica um index fortificado (não pode gerar filhos)

A master key que alguns softwares ou wallets nos mostram têm um derivation path que não é padrão.
O site https://walletsrecovery.org/ tem uma lista bastante completa
de quais derivation path são usados pelos vários softwares/hardwares.



*[BIP]: Bitcoin Improvement Proposal











https://github.com/modood/btckeygen

- BIP32 - Hierarchical Deterministic Wallets
- BIP39 - Mnemonic code for generating deterministic keys
- BIP43 - Purpose Field for Deterministic Wallets
- BIP44 - Multi-Account Hierarchy for Deterministic Wallets
- BIP49 - Derivation scheme for P2WPKH-nested-in-P2SH based accounts
- BIP84 - Derivation scheme for P2WPKH based accounts
- BIP173 - Base32 address format for native v0-16 witness outputs
- SLIP44 - Registered coin types for BIP-0044
