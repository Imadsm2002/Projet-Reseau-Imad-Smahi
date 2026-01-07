# Projet Réseau : Infrastructure Segmentée Multisite (VLANs & Routage Statique)

**Module :** Réseaux Informatiques  
**Encadrant :** Prof. Azeddine KHIAT  
**Année :** 2025/2026

##  Description du Projet
Ce dépôt contient les livrables du projet final de conception réseau. L'objectif est de déployer une architecture d'entreprise simulant un siège social et deux sites distants, en mettant l'accent sur la segmentation, la redondance et l'optimisation des flux.

## 🛠️ Technologies Déployées
* **Switching (L2) :**
    * VLANs (802.1Q) : Segmentation en 5 réseaux logiques (Utilisateurs, Natif, Admin).
    * EtherChannel (LACP) : Agrégation de liens entre les commutateurs S1 et S2.
    * Sécurité : Configuration du VLAN Natif 50.
* **Routing (L3) :**
    * Router-on-a-Stick : Routage inter-VLAN sur R1.
    * Routage Statique : Interconnexion WAN entre R1, R2 et R3.
    * Route par défaut : Gestion du trafic de retour sur les sites distants.

##  Structure du Dépôt
* `/Fichiers_PKT` : Le fichier de simulation Cisco Packet Tracer (.pkt).
* `/Captures` : Captures d'écran validant le fonctionnement (Ping, Traceroute, Show commands).
* `/Rapport` : Version PDF du rapport de déploiement.

## Plan d'Adressage Rapide
| Équipement | Interface | IP / Masque | Description |
| :--- | :--- | :--- | :--- |
| **R1** | Fa0/0.10 | 172.18.10.14 /28 | Gateway VLAN 10 |
| **R1** | S0/3/0 | 10.0.30.177 /30 | Vers R2 |
| **S1/S2** | Po1 | - | Trunk (Natif 50) |

##  Validation
Le projet a été validé par les tests suivants :
1.  **Ping Inter-VLAN :** Fonctionnel.
2.  **Traceroute WAN :** Routage correct via les sauts R1 -> Rx.
3.  **Accès SSH/Telnet :** Gestion accessible via VLAN 60.


---
**Réalisé par :** Imad Smahi
**Date :**  Décembre 2025
