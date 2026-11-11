# Mon HomeLab
- le commencement
Tout a commencé en juin 2026 , ne me plaisant pas dans les études ou j'étais ( clim , froid et conventionnement d'air ) j'ai décidé de tout arrêter je venais de validé ma première année de BTS. Je me suis donc renseigné sur ce qui ma toujours passionné **l'informatique** , un amis a moi ma donc conseiller le BTS SIO option SISR , une semaine âpres j’étais inscrit dans l'école Ensitech à Cergy.Et a partir de la j'ai voulu commencer a prendre de l'avance et par conseil du même amis j'ai décidé de monter mon propre **homelab**.

- J'ai donc commencé par acheté un Raspberry PI 5 avec 8Go de RAM , c'était ma première vrai expérience et tout c'est super bien passé j'ai donc installer Proxmox VE sur ce Rasberry et je me suis familiariser avec. Et quelque temps âpres j'ai aussi acheter mon premier pc dédié a mon Infrastructure un ProDesk Mini de la marque HP j'ai donc installer Proxmox VE aussi et j'ai retrouvé un ancien ordinateur portable qui trainer chez moi que j'ai donc reécuprer pour en faire un Proxmox Critique c'est la ou tourne ma connexion a distance via Netbird et mon DNS.
J'ai aussi acheter un routeur Cudy pour isoler mon infrastructure au réseau de la maison , j'ai nommé mes ordinateur d'une façon reconnaissable c'est a dire par des nom de voiture 😊.

## 🏗️ Mon infrastructure

<p align="center">
  <img src="https://img.shields.io/badge/Proxmox_VE-9-E57000?style=for-the-badge&logo=proxmox&logoColor=white" alt="Proxmox VE 9">
  <img src="https://img.shields.io/badge/cluster-2_n%C5%93uds-7B61FF?style=for-the-badge" alt="Cluster de 2 nœuds">
  <img src="https://img.shields.io/badge/conteneurs_LXC-9-2EA44F?style=for-the-badge&logo=linuxcontainers&logoColor=white" alt="9 conteneurs LXC">
  <img src="https://img.shields.io/badge/VPN-WireGuard-88171A?style=for-the-badge&logo=wireguard&logoColor=white" alt="VPN WireGuard">
  <img src="https://img.shields.io/badge/sauvegardes-3_copies-0A66C2?style=for-the-badge" alt="Sauvegardes en 3 copies">
</p>

<p align="center">
  <img src="Cluster%20Garage.png" alt="Vue d'ensemble du réseau" width="100%">
</p>

> **En résumé :** un cluster Proxmox de 2 machines, isolé du réseau de la maison derrière son propre routeur, avec un DNS filtrant en double, un accès à distance par VPN et des sauvegardes en 3 copies.

### 🖥️ Le matériel

| | Machine | Rôle |
|:-:|---|---|
| 🚗 | **mazda-mx5**<br><sub>Lenovo IdeaPad 330S · i3 · 4 Go</sub> | Nœud critique : DNS principal et passerelle VPN. Un vieux portable récupéré, qui tourne capot fermé avec la batterie bloquée à 60 %. |
| 🏎️ | **toyota-ae86**<br><sub>HP ProDesk Mini · i5 · NVMe 256 Go</sub> | Nœud services : Plex, supervision et tableau de bord. |
| 💾 | **ReadyNAS 424**<br><sub>4 baies · 5,4 To</sub> | Les films pour Plex et la 3e copie des sauvegardes. |
| 📡 | **Cudy WR3000S** | Routeur du homelab, sur un réseau séparé de celui de la maison. |
| 🍓 | **Raspberry Pi 5**<br><sub>8 Go</sub> | Bientôt le 3e vote du cluster (QDevice). |
| 🗄️ | **Rack 10" · 5U**<br><sub>imprimé en 3D · PLA</sub> | Range tout ce petit monde. |

### ⚙️ Les services

Un conteneur LXC par service : c'est léger, et chaque service se sauvegarde à part.

| Catégorie | Service | À quoi ça sert |
|---|---|---|
| 🌐 Réseau | ![AdGuard Home](https://img.shields.io/badge/AdGuard_Home-68BC71?style=flat-square&logo=adguard&logoColor=white)<br><sub>sur mazda-mx5</sub> | DNS principal : bloque les pubs et les domaines malveillants |
| | ![AdGuard Home 2](https://img.shields.io/badge/AdGuard_Home_2-68BC71?style=flat-square&logo=adguard&logoColor=white)<br><sub>sur toyota-ae86</sub> | DNS de secours, synchronisé automatiquement |
| 🔐 Accès distant | ![NetBird](https://img.shields.io/badge/NetBird-F68330?style=flat-square&logo=wireguard&logoColor=white)<br><sub>sur mazda-mx5</sub> | VPN WireGuard : administration à distance sans aucun port d'admin ouvert |
| 🎬 Médias | ![Plex](https://img.shields.io/badge/Plex-EBAF00?style=flat-square&logo=plex&logoColor=black)<br><sub>sur toyota-ae86</sub> | Films et séries, transcodage matériel Intel Quick Sync |
| | ![Tautulli](https://img.shields.io/badge/Tautulli-E5A00D?style=flat-square&logo=plex&logoColor=black)<br><sub>sur toyota-ae86</sub> | Statistiques Plex et alertes Discord |
| 📊 Monitoring | ![Beszel](https://img.shields.io/badge/Beszel-374151?style=flat-square)<br><sub>sur toyota-ae86</sub> | CPU, RAM et disque des machines |
| | ![Uptime Kuma](https://img.shields.io/badge/Uptime_Kuma-5CDD8B?style=flat-square&logo=uptimekuma&logoColor=white)<br><sub>sur toyota-ae86</sub> | Disponibilité des services, avec alertes |
| 🏠 Tableau de bord | ![Homepage](https://img.shields.io/badge/Homepage-7B61FF?style=flat-square)<br><sub>sur toyota-ae86</sub> | L'état de tous les services sur une seule page |
| 🎮 Jeux | ![FiveM](https://img.shields.io/badge/FiveM-F40552?style=flat-square&logo=fivem&logoColor=white)<br><sub>sur toyota-ae86</sub> | Serveur GTA RP, à l'arrêt pour l'instant |

### 🗺️ Les schémas

<table>
  <tr>
    <td align="center" width="50%">
      <img src="Rack%20et%20C%C3%A2blage.png" alt="Rack et câblage"><br>
      <b>Rack et câblage</b>
    </td>
    <td align="center" width="50%">
      <img src="Services.png" alt="Services hébergés"><br>
      <b>Services hébergés</b>
    </td>
  </tr>
  <tr>
    <td align="center" width="50%">
      <img src="DNS%20et%20Acc%C3%A8s%20Distant.png" alt="DNS et accès distant"><br>
      <b>DNS et accès distant</b>
    </td>
    <td align="center" width="50%">
      <img src="Exploitation.png" alt="Plex, sauvegardes et sécurité"><br>
      <b>Plex, sauvegardes et sécurité</b>
    </td>
  </tr>
</table>

<p align="center">
  <a href="homelab-garage.pdf"><img src="https://img.shields.io/badge/Sch%C3%A9ma_complet-PDF_%C2%B7_5_pages-B31B1B?style=for-the-badge" alt="Schéma complet en PDF"></a>
</p>

### 💾 Sauvegardes : la règle des 3 copies

| | Où | Quand |
|:-:|---|---|
| 1️⃣ | Sur la machine elle-même | Sauvegarde Proxmox (vzdump) |
| 2️⃣ | Sur l'autre nœud | Copie automatique après chaque sauvegarde |
| 3️⃣ | Sur le NAS | Chaque semaine, 4 versions gardées |

Les films ne sont pas copiés : le montage du NAS est exclu des sauvegardes.

### 🛡️ Sécurité

- 🔑 Connexion SSH d'administration par clé uniquement
- 🔐 Double authentification (2FA) sur les consoles d'admin
- 🌍 Aucune interface d'admin sur Internet : l'accès à distance passe uniquement par le VPN
- 📦 Conteneurs non privilégiés
- 🗝️ Secrets hors des fichiers de configuration, mots de passe dans un gestionnaire dédié
- 💾 NAS jamais exposé à Internet, et Plex ne lit les films qu'en lecture seule
- 🎬 Plex partagé uniquement par comptes invités, aucun accès sans authentification

### 🚀 Feuille de route

- [x] Cluster Proxmox à 2 nœuds
- [x] DNS filtrant en double (2 AdGuard synchronisés)
- [x] Accès à distance par VPN (NetBird)
- [x] Plex et sa supervision (Tautulli, Beszel, Uptime Kuma)
- [x] Sauvegardes en 3 copies
- [x] Rack 10" imprimé en 3D
- [ ] Switch 8 ports administrable (VLAN)
- [ ] Raspberry Pi 5 en QDevice, 3e vote du cluster
- [ ] Onduleur
- [ ] Câble entre le routeur et la box
- [ ] Test de restauration complet

---

<p align="center">
  <sub>Monté par <b>keke</b> · étudiant en BTS SIO SISR</sub><br>
  <a href="https://kck-it.fr"><img src="https://img.shields.io/badge/KCK--IT-site-7B61FF?style=flat-square" alt="KCK-IT"></a>
  <a href="https://portfolio-kelyan.web.app"><img src="https://img.shields.io/badge/Portfolio-voir-2EA44F?style=flat-square" alt="Portfolio"></a>
</p>

