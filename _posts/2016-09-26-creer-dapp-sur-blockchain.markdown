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
