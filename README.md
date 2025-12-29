# Projet de Conception et Routage Réseau (Packet Tracer)

##  Description du Projet
Ce dépôt contient la simulation complète d'une infrastructure réseau d'entreprise réalisée sur **Cisco Packet Tracer**. Le projet vise à interconnecter un site central (Siège) avec deux sites distants (Agences) en assurant la redondance, la segmentation et la connectivité de bout en bout.

##  Technologies et Protocoles Utilisés
Le projet met en œuvre les technologies suivantes :
* **Commutation (Layer 2) :**
    * VLANs (10, 20, 60, 99) pour la segmentation.
    * Trunking (802.1Q).
    * EtherChannel (LACP) pour l'agrégation de liens.
* **Routage (Layer 3) :**
    * Routage Inter-VLAN (Router-on-a-Stick).
    * **Routage Statique** pour la connectivité WAN (Siège ↔ Agences).
    * Routes par défaut sur les sites distants (Stub Networks).
* **Adressage :** IPv4 (VLSM).

##  Topologie du Réseau
L'architecture se compose de :
1.  **Siège (R1 + S1/S2) :** Héberge les VLANs utilisateurs et gestion. Utilise l'agrégation de liens entre les commutateurs.
2.  **Agence 1 (R2) :** Site distant connecté au siège via liaison série.
3.  **Agence 2 (R3) :** Site distant connecté au siège, assurant une redondance de chemin.

##  Détails de la Configuration
* **R1 (Siège) :** Configure avec des routes statiques vers le réseau WAN interconnectant R2 et R3.
* **R2 & R3 (Agences) :** Configurés avec une route par défaut (`0.0.0.0/0`) pointant vers le Siège (R1).
* **Switchs :** Configuration des VLANs de données et VLAN natif (99) pour la sécurité.

##  Tests de Validation
Le réseau a été validé avec succès via :
* **Ping Inter-VLAN :** Communication réussie entre PC VLAN 10 et PC VLAN 20.
* **Ping WAN :** Connectivité établie entre le Siège et les interfaces des Agences.
* **Traceroute :** Vérification du chemin et des sauts (Hops) entre le LAN et le WAN.

##  Comment utiliser
1.  Cloner ce dépôt.
2.  Ouvrir le fichier `.pkt` avec **Cisco Packet Tracer** (version 8.x ou supérieure).
3.  Utiliser les PCs pour effectuer des tests de connectivité (Ping/Tracert).

---
**Réalisé par :** Imad Smahi
**Date :** Décembre 2025
