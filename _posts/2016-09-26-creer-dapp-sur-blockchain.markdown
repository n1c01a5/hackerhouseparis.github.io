---
layout: post
title:  "Créer une dapp sur Ethereum"
date:   2016-09-26 16:53:35 +0200
categories: blockchain ethereum
---
> Les adolescents représentent l’avenir. Ils ne sont pas encore embourbés par la
façon dont nous menons actuellement nos vies, avec nos cartes de crédit,
hypothèques, etc. Alors que pour la plupart des gens, passer au Bitcoin
est une souffrance à court terme car ils sont déjà à l’aise avec le fait
d’utiliser des cartes de crédit, pour les adolescents c’est à l’inverse tout
le processus d’ouverture de compte et de carte de crédit qui leur pose
problème. Ils préfèreraient simplement pouvoir commencer à gagner et dépenser
quelques “coins”. En outre, ils ne sont pas encore corrompus par la psychologie
du système de cartes de crédit qui veut qu’il est plus simple d’obtenir de
l’argent rapidement et temporairement en suppliant plutôt qu’en produisant. La
psychologie que ces jeunes adopteront sera, dans 10 ou 20 ans, celle qui
conduira la psychologie de la société.
> - Vitalik Buterin (17ans à l’écriture de ce post), co-fondateur d’Ethereum,
28/02/2012

[Ethereum][Ethereum] est une __plateforme décentralisée__ et __distribuée__ pour
lancer des __smart contracts__ (ou programmes autonomes sur une blockchain).
Cette plateforme est un ordinateur à l’échelle mondiale. Il est toujours
accessible et n’importe qui peut programmer un smart contract dessus. Cet
ordinateur global est formé à partir de milliers d'ordinateurs répartis sur
toute la planète et ces ordinateurs sont appelés les __noeuds__ du réseau dont
certains sont des __mineurs__.  Ils utilisent une base de __données
distribuée__, appelée __blockchain__, pour partager les transactions et les
programmes entre eux. Les données sont __décentralisées__, __persistantes__ et
sur un réseau __peer-to-peer__.
Avantage : il n’y a pas de “single point of failure”.

![Ethereum](http://i.stack.imgur.com/hDDzg.png)

Qu’est-ce que la blockchain ?
=============================

La blockchain est une base de donnée distribuée dans laquelle on peut
enregistrer des données sans passer par un intermédiaire. La blockchain la plus
connue est [Bitcoin][Bitcoin] qui permet de s’échanger des __tokens__, une
forme de cryptomonnaie. Ces transactions sont enregistrées dans la blockchain
par des mineurs qui apportent leur puissance de calcul à l'effort
d'enregistrement (n’importe qui avec son ordinateur peut miner). Le processus
d'enregistrement se fait par blocs de transactions successifs, d'où le
terme de blockchain.
Concrètement l'effort de calcul que fournisse les mineurs sécurise chaque bloc
en garantissant son immuabilité.
Ethereum reprend cette technologie et la généralise pour construire des
applications sur la blockchain, et pas seulement une *monnaie*. Concrètement,
il s’agit de développer un smart contract avec la logique de l’application et de
la pousser dans la blockchain Ethereum.

Comment sont créés les blocs ?
===========================

L'ajout d'un bloc dans le registre que constitue la blockhain est l'oeuvre des
mineurs qui fournissent une solution à un puzzle cryptographique propre à chaque
bloc. Ces puzzles sont générés par le protocole de la blockchain et il n'existe
pas de meilleure technique de résolution que le brute-force pour les résoudre.
Ainsi, un mineur qui parvient à résoudre le puzzle d'un bloc peut prouver au
réseau qu'il a bien fourni un travail computationnel sur ce puzzle. Le puzzle
est, par construction, difficile à résoudre et cette difficulté s'adapte à la
puissance de calcul de l'ensemble du réseau. Cependant, lorsqu'une solution est
trouvée, elle est très simple à vérifier. Il est dès lors très facile pour les
noeuds du réseau qui reçoivent un bloc de vérifier que sa solution est conforme
et ainsi d'obtenir le __consensus des noeuds__ sur le dernier bloc de la
blockchain. Cette preuve de validité d’un bloc est appelée __proof-of-work__ ou
preuve de travail. Trouver cette preuve demande énormément de ressources de
calcul et donc d'électricité pour les mineurs, mais cette énergie est convertie
en sécurité pour la blockchain. En raison de cette forte demande de ressources,
les blocs s'accompagnent d'une récompense: le mineur se voit verser un certain
montant de cryptomonnaie fraîchement créée. La complexité ainsi que le chaînage
des uns à la suite des autres font qu'il est difficile de falsifier ou supprimer
les données de la blockchain. L'héritage d'un bloc à l'autre fait que la
modification des données d'un bloc entraine la nécessité de résoudre un nouveau
puzzle pour le bloc modifié et l'ensemble des blocs qui le suivent. Les noeuds
suivent une règle fondamentale: la chaîne la plus longue est la chaîne qui fait
foi. Ce dernier point implique que pour qu'une modification soit validée par le
réseau, il faut que cette modification soit accompagnée d'un effort calculatoire
qui croît exponentiellement à mesure que la modification est en aval dans la
chaîne.

Que sont les smart contracts d'Ethereum ?
=============================================

Le smart contract (pour contrat intelligent) est un programme qui s'exécute sur
la blockchain. Il peut dialoguer avec d'autres smart contracts, prendre des
décisions, envoyer des ethers (la cryptomonnaie d'Ethereum) et exécuter d'autres
smart contracts. Ces smart contracts existeront tant que le réseau sera
accessible. Il ne peuvent s'arrêter seulement s'ils ne sont plus alimentés par
du __gas__ (qui est une des formes de __l'ether__, c'est à dire la cryptomonnaie
de la blockchain Ethereum) ou si le développeur a programmé son
auto-destruction.

Qu'est-ce qu'une dApp ?
=======================

DApp est l'abbrévation de __application décentralisée__. Une dApp a un *backend*
qui s'exécute sur un réseau peer-to-peer, le *smart contract*. Et la dApp a un
*frontend* qui est l'interface utilisateur pour dialoguer avec le backend. Ce
frontend n'est pas forcément sur une blockchain mais cela est possible avec des
outils tels que [Swarm ou IPFS][Swarm_IPFS].

DApp = frontend + contracts

![schema_dapp](http://i.stack.imgur.com/jzm8y.png)

Quels sont les outils de base pour développer une dApp ?
========================================================

Les outils les plus utilisés sont [geth][geth] pour mettre en place le réseau et
[solc][solc] pour compiler le smart contract.

Pour ajouter ces outils avec le gestionnaire de paquet *apt* :

```bash
apt-get update
apt-get install -y software-properties-common
add-apt-repository -y ppa:ethereum/ethereum
add-apt-repository -y ppa:ethereum/ethereum-dev
apt-get update
apt-get install -y ethereum solc # pour installer le compilateur smart contract
```
Sur mac:

```bash
brew tap ethereum/ethereum
brew install ethereum
```

Comment créer une blockchain privée avec des noeuds ?
=====================================================

Il faut un premier bloc avec l'ensemble des caractéristiques de départ de notre
blockchain.
Le format est le suivant :

```json
{
  "nonce": "0x00",
  "difficulty": "0x1000",
  "mixHash": "0x00",
  "timestamp": "0x00",
  "parentHash": "0x00",
  "extraData": "0x00",
  "gasLimit": "0x1000000000"
}
```

- __nonce__ : hash que le mineur fait varier pour résoudre le proof-of-work
- __difficulty__ : difficulté de la preuve de travail
- __mixmash__ : hash de l'entête du bloc sur lequel se base le mineur pour
trouver le nonce
- __timestamp__ : moment de validation du bloc
- __parentHash__ : hash du bloc précédant
- __extraData__ : argument facultatif pour stocker des données
(32 octets max.)
- __gasLimit__ : montant maximum de *gas* que les contrats peuvent consommer

Pour créer et initialiser le premier noeud de la blockchain :

```bash
geth --datadir ./noeud1 --networkid "100" init genesis.json
```

Pour ajouter un autre noeud, il faut répéter la commande en modifiant le nom du
noeud.

Par exemple :

```bash
geth --datadir ./noeud2 --networkid "100" init genesis.json
```

- __datadir__ : répertoire de données du noeud
- __networkid__ : flag qui identifie le réseau et permet aux pairs de le
rejoindre

Dans cet exemple, les flags *datadir* et *networkid* seront obligatoires pour
appeler le client `geth` sur ce réseau, car ils identifient respectivement le
répertoire de travail et l'identifiant du réseau.

Comment créer un smart contract `Hello world!`?
===============================================

Il faut créer un nouveau compte sur le noeud pour réaliser des transactions,
créer et interagir avec des smart contracts.

Sur le *noeud 1* :

```bash
geth --datadir ./noeud1 --networkid "100" account new
```

Une fois que le mot de passe est configuré, la console vous renvoie __clé
publique__.

Il faut ensuite lancer les noeuds.
Pour lancer le *noeud 1* sur le port *30301* :

```bash
geth --datadir ./noeud1 --networkid "100" --port "30301" console
```

Pour connaître l'adresse réseau de votre réseau, il faut entrer dans la console
`geth` :

```javascript
admin.nodeInfo
```

Pour lier les noeuds entre eux, il faut utiliser *bootnodes* de `geth`.
Pour lier le *noeud 1* avec le *noeud 2* :

```bash
geth --nodiscover --bootnodes="[enodeNoeud1],[enodeNoeud2],[enodeNoeudN]"
```

Pour créer le smart contract et l'assigner à la variable `greeterSource` dans la
console :

```javascript
var greeterSource = 'contract mortal { address owner; function mortal() { owner = msg.sender; } function kill() { if (msg.sender == owner) suicide(owner); } } contract greeter is mortal { string greeting; function greeter(string _greeting) public { greeting = _greeting; } function greet() constant returns (string) { return greeting; } }';
```

Pour compiler le smart contract :

```
var greeterSourceCompiled = web3.eth.compile.solidity(greeterSource);
```


Bibliographie
=============

- [Ethereum][Ethereum]: site officiel d'Ethereum
- [Ethereum guide][Ethereum-guide]: guide d'Ethereum
- [Ethstats][Ethstats]: statistiques sur Ethereum
- [Etherchain][Etherchain]: statistiques sur Ethereum
- [jefflau.net][jefflau.net]: introduction à Ethereum
- Programmez!#199: introduction à la programmation sur Ethereum
- O'Reilly blockchain: introduction à la technologie de Bitcoin


[Ethereum]: https://www.ethereum.org/
[Ethereum-guide]: https://ethereum.gitbooks.io/frontier-guide/content/index.html
[Bitcoin]: https://bitcoin.org/fr/
[Ethstats]: https://ethstats.net/
[Etherchain]: https://www.etherchain.org/
[jefflau.net]: http://jefflau.net/how-to-start-developing-on-ethereum-for-web-developers/
[Swarm_IPFS]: https://github.com/ethersphere/go-ethereum/wiki/IPFS-&-SWARM
[geth]: https://github.com/ethereum/go-ethereum
[solc]: https://github.com/ethereum/solc-js
