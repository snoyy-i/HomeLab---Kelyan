# Mon homelab

Salut, moi c'est kelyan, je suis en BTS SIO option SISR. Ici je partage le homelab que je monte chez moi pour apprendre.

## Comment ça a commencé

En juin 2026, j'ai décidé d'arrêter mes études dans la clim, le froid et le conditionnement d'air car ce métier ne me plaisait plus. Je venais de valider ma première année de BTS. Je me suis demandé ce qui m'avait toujours passionné, et c'était l'informatique. Un ami m'a conseillé le BTS SIO option SISR, et une semaine après j'étais inscrit chez Ensitech à Cergy.

Pour prendre de l'avance, et toujours sur les conseils de ce même ami, j'ai décidé de monter mon propre homelab.

## Mon matériel

J'ai commencé avec un Raspberry Pi 5 (8 Go de RAM). J'ai installé Proxmox VE dessus pour découvrir, c'était ma première vraie expérience et ça s'est super bien passé.

Ensuite j'ai acheté mon premier vrai PC pour le homelab, un HP ProDesk Mini, et j'ai récupéré un vieux portable Lenovo qui traînait chez moi. Les deux sont sous Proxmox et forment un cluster que j'ai appelé "garage". Dernièrement j'ai aussi récupéré un Dell OptiPlex 3000 que je suis en train d'ajouter au cluster comme 3e nœud. J'ai donné des noms de voitures à mes machines 😊

- **toyota-ae86** (HP ProDesk Mini, passé à 16 Go de RAM) : c'est là que tournent la plupart de mes services
- **mazda-mx5** (le vieux portable Lenovo) : mon nœud "critique", il fait tourner le DNS, l'accès à distance et mon agent IA
- **nissan-skyline** (Dell OptiPlex 3000, 16 Go de RAM) : mon nouveau nœud, Proxmox est en cours d'installation
- un **ReadyNAS** pour stocker mes films et mes sauvegardes
- un routeur **Cudy** pour mettre le homelab sur un réseau séparé de celui de la maison
- le **Raspberry Pi 5**, que je garde pour un second accès NetBird

Tout est rangé dans un petit rack 10 pouces que j'ai imprimé en 3D.

## Mes services

Chaque service tourne dans son propre conteneur LXC.

- **AdGuard Home** (x2) : mon DNS, il bloque les pubs sur tout le réseau. J'en ai mis un sur chaque machine, comme ça si une tombe, internet marche toujours
- **NetBird** : un VPN pour accéder à mon homelab quand je ne suis pas chez moi
- **Hermes Agent** : un agent IA open source de Nous Research. Je lui parle depuis mon téléphone par messagerie, il garde une mémoire de nos échanges et utilise un modèle d'IA en ligne
- **Plex** : mes films et mes séries, pour moi et mes proches
- **Tautulli** : pour voir qui regarde quoi sur Plex, avec des alertes sur Discord
- **Beszel** et **Uptime Kuma** : pour surveiller mes machines et savoir quand un service ne répond plus
- **Homepage** : une page d'accueil avec tous mes services
- **FiveM** : un serveur GTA RP (éteint pour l'instant)

## Mes sauvegardes

J'ai appris qu'une sauvegarde à un seul endroit, ça ne suffit pas. Donc chaque conteneur est sauvegardé 3 fois :

1. sur la machine elle-même
2. sur l'autre machine du cluster
3. sur le NAS, une fois par semaine

## Ce que j'ai appris (et mes galères)

- En YAML, un espace en trop et plus rien ne marche. Homepage me l'a bien fait comprendre
- Avec un cluster de 2 machines, si une s'éteint, l'autre se bloque (le quorum). C'est pour ça que j'ajoute un 3e nœud : avec 3 machines, le cluster tient même si une tombe
- Une erreur bizarre ça peut juste être une ligne oubliée dans un fichier de config
- Les mots de passe ne vont jamais dans les fichiers de config ni sur les captures d'écran, ils vont dans un gestionnaire de mots de passe
- Je n'ouvre pas mon interface d'admin sur internet, j'y accède seulement par le VPN

<p align="center">
  <img src="https://img.shields.io/badge/Proxmox_VE-9-E57000?style=for-the-badge&logo=proxmox&logoColor=white" alt="Proxmox VE 9">
  <img src="https://img.shields.io/badge/cluster-3_n%C5%93uds-7B61FF?style=for-the-badge" alt="Cluster de 3 nœuds">
  <img src="https://img.shields.io/badge/conteneurs_LXC-10-2EA44F?style=for-the-badge&logo=linuxcontainers&logoColor=white" alt="10 conteneurs LXC">
  <img src="https://img.shields.io/badge/VPN-WireGuard-88171A?style=for-the-badge&logo=wireguard&logoColor=white" alt="VPN WireGuard">
  <img src="https://img.shields.io/badge/sauvegardes-3_copies-0A66C2?style=for-the-badge" alt="Sauvegardes en 3 copies">
</p>

## Les schémas

Voici les schémas de mon infra (sans les IP bien sûr).

![Vue d'ensemble](Cluster%20Garage.png)
![Rack et câblage](Rack%20et%20C%C3%A2blage.png)
![Services](Services.png)
![DNS et accès distant](DNS%20et%20Acc%C3%A8s%20Distant.png)
![Plex, sauvegardes et sécurité](Exploitation.png)

Le PDF complet est ici : [homelab-garage.pdf](homelab-garage.pdf)

<p align="center">
  <img src="https://img.shields.io/badge/AdGuard_Home-68BC71?style=flat-square&logo=adguard&logoColor=white" alt="AdGuard Home">
  <img src="https://img.shields.io/badge/NetBird-F68330?style=flat-square&logo=wireguard&logoColor=white" alt="NetBird">
  <img src="https://img.shields.io/badge/Hermes_Agent-5B3FD1?style=flat-square" alt="Hermes Agent">
  <img src="https://img.shields.io/badge/Plex-EBAF00?style=flat-square&logo=plex&logoColor=black" alt="Plex">
  <img src="https://img.shields.io/badge/Tautulli-E5A00D?style=flat-square&logo=plex&logoColor=black" alt="Tautulli">
  <img src="https://img.shields.io/badge/Beszel-374151?style=flat-square" alt="Beszel">
  <img src="https://img.shields.io/badge/Uptime_Kuma-5CDD8B?style=flat-square&logo=uptimekuma&logoColor=white" alt="Uptime Kuma">
  <img src="https://img.shields.io/badge/Homepage-7B61FF?style=flat-square" alt="Homepage">
  <img src="https://img.shields.io/badge/FiveM-F40552?style=flat-square&logo=fivem&logoColor=white" alt="FiveM">
</p>

## La suite

- [ ] acheter un switch 8 ports pour faire des VLAN
- [ ] installer Proxmox sur nissan-skyline et l'ajouter au cluster
- [ ] acheter un onduleur
- [ ] tester une vraie restauration de sauvegarde
