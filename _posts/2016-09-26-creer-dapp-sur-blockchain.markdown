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
> - Vitalik Buterin (17ans à l’écriture de ce post), fondateur d’Ethereum,
28/02/2012

[Ethereum][Ethereum] est une __plateforme décentralisée__ et distribuée pour
lancer des __smart contrats__ (ou programmes autonomes sur une blockchain). Cette
plateforme est un ordinateur à l’échelle mondiale. Il est toujours accessible et
n’importe qui peut programmer un smart contrat dessus. Cet ordinateur global est
formé à partir de milliers d'ordinateurs répartis sur toute la planète, ces
ordinateurs sont appelés les __mineurs__. Ils utilisent une base de
__données distribuée__, appelée __blockchain__, pour partager les transactions et
les programmes entre eux. Les données sont __décentralisées__, __persistantes__,
sur un réseau __peer-to-peer__. Avantage : il n’y a pas de “single point of failure”.

![Ethereum](http://i.stack.imgur.com/hDDzg.png)

Qu’est-ce que la blockchain ?
=============================

La blockchain est une base de donnée distribuée où l'on peut enregistrer des
données sans passer par un intermédiaire. La blockchain la plus connue est
[Bitcoin][Bitcoin] qui permet de s’échanger des __tokens__, c’est une forme de
cryptomonnaie. Ces transactions sont validées par des mineurs, qui partagent une
partie de leur puissance de calcul numérique (n’importe qui avec son ordinateur
peut miner). Etherum reprend cette technologie et la généralise pour construire
des applications, et pas seulement une *monnaie*, sur la blockchain. Concrètement,
il s’agit de développer un smart contract avec la logique de l’application et
de la pousser dans la blockchain ethereum.

Comment valider les blocs ?
===========================

Le registre de la blockhain peut être modifié par un ou plusieurs mineurs. Alors
comment s’assurer de la légitimité de celle-ci ? La validité de la blockchain
est assurée par le __consensus des noeuds__ du réseau distribué. Principe : si
un block est validé par la majorité des mineurs, il est considéré comme valide.
Cette preuve de validité d’un bloc est appelé __proof-of-work__. Trouver cette
preuve demande énormément de ressource.
C'est pourquoi, pour chaque ajout à la blockchain, le mineur se voit verser un
certain montant de cryptomonnaie, fraîchement créée. La complexité ainsi
que le chaînage des uns à la suite des autres font qu'il est difficile de
falsifier ou supprimer les données de la blockchain. Pour modifier les données
d'un bloc, il faut refaire valider l'ensemble des blocs qui le suivent, avant
qu'un autre noeud n'ajoute un nouveau bloc à la chaîne.

Qu'est-ce que les smart contract d'Ethereum ?
=============================================

Le smart contract (pour contrat intelligent) est un programme qui s'exécute sur
la blockhain. Il peut dialoguer avec d'autres smart contract, prendre des
décisions, envoyer des ethers (la cryptomonnaie d'Ethereum) et exécuter d'autres
smart contract. Ces smart contract existeront tant que le réseau sera
accessible. Il ne peuvent s'arrêter seulement s'ils ne sont plus alimentés par
du __gas__ (la cryptomonnaie pour lancer les smart contract) ou si le
développeur a programmé son auto-destruction.

Qu'est-ce qu'une dApp ?
=======================

DApp est l'abbrévation de __application décentralisée__. Une dApp a un *backend*
qui s'éxécute sur un réseau peer-to-peer, le *smart contract*. Et la dApp a un
*frontend* qui est l'interface utilisateur pour dialoguer avec le backend. Ce
frontend n'est pas forcément sur une blockhain mais cela est possible avec des
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

Comment créer une blockhain privée avec des noeuds ?
==================================================

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
- __mixmash__ : hash de l'entête du bloc sur lequel se base le mineur pour
trouver le nonce
- __timestamp__ : moment de validation du bloc
- __parentHash__ : hash du bloc précédant
- __extraData__ : argument facultatif pour stocker des données
(32 octets max.).
- __gasLimit__ : montant maximum de *gas* que les contrats peuvent consommer
- __difficulty__ : difficulté de la preuve de travail

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
créer et interagir avec des smart contract.

Sur le *noeud 1* :

```bash
geth --datadir ./noeud1 --networkid "100" account new
```

Une fois que le mot de passe est configuré, la console vous renvoie __clé
publique__.

Il faut ensuite lancer les noeuds.
Pour le *noeud 1* sur le port *30301* :

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
geth --nodiscover --bootnodes enode://71160f012f666c47dbacbdfaa56b360478899b139ea57d5d1531eba80638c4786cdd250addfe8e81b4de33c20dcf0637793e8e36e7670ae510ba79dc8b378018@[::]:30301,enode://f4f06833fbc41d39eacbc110e66077ee931e5100c33ebbbcf9b3ccc84ef5aa6832754ed9eef5f70ae380c19e1412f6f04476cfe0ec8d81b6e3694039049e7f3d@[::]:30302
```

<div class="alert">
  <span class="closebtn" onclick="this.parentElement.style.display='none';">
    &times;
  </span>
  <b>Attention !</b> Il faut lancer cette commande avant d'avoir lancer les
  noeuds.
</div>

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
- O'Reilly blockhain: introduction à la technologie de Bitcoin


[Ethereum]: https://www.ethereum.org/
[Ethereum-guide]: https://ethereum.gitbooks.io/frontier-guide/content/index.html
[Bitcoin]: https://bitcoin.org/fr/
[Ethstats]: https://ethstats.net/
[Etherchain]: https://www.etherchain.org/
[jefflau.net]: http://jefflau.net/how-to-start-developing-on-ethereum-for-web-developers/
[Swarm_IPFS]: https://github.com/ethersphere/go-ethereum/wiki/IPFS-&-SWARM
[geth]: https://github.com/ethereum/go-ethereum
[solc]: https://github.com/ethereum/solc-js
