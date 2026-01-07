# Projet Final : Conception et Déploiement d'une Infrastructure Réseau Multisites

**Étudiant :** Imad Smahi
**Filière :** Informatique
**Encadrant :** Prof. Azeddine KHIAT
**Année universitaire :** 2025/2026
**Module :** Réseaux Informatiques (VLAN + EtherChannel + RoaS + Routage Statique)

---

## 1. Description du Projet
Ce projet consiste à concevoir et déployer une infrastructure réseau d'entreprise multisite simulée sous **Cisco Packet Tracer**. L'objectif est de garantir une segmentation logique, une haute disponibilité et une interconnexion sécurisée entre le siège et les sites distants.

### Objectifs techniques validés :
* **Segmentation logique :** Séparation des flux par VLANs pour la sécurité et la performance.
* **Haute disponibilité :** Agrégation de liens avec **EtherChannel (LACP)** entre les commutateurs.
* **Routage Inter-VLAN :** Implémentation de l'architecture **Router-on-a-Stick** sur R1.
* **Interconnexion WAN :** Configuration du routage statique entre le siège (R1) et les sites distants (R2, R3).

---

## 2. Topologie et Plan d'Adressage

### 2.1 VLANs (Siège - Switchs S1 & S2)

| VLAN | Usage          | Réseau IP       | Masque (/28)    | Passerelle (R1) |
|------|----------------|-----------------|-----------------|-----------------|
| 10   | Utilisateurs 1 | 172.18.10.0     | 255.255.255.240 | 172.18.10.14    |
| 20   | Utilisateurs 2 | 172.18.20.0     | 255.255.255.240 | 172.18.20.14    |
| 30   | Utilisateurs 3 | 172.18.30.0     | 255.255.255.240 | 172.18.30.14    |
| 50   | VLAN Natif     | 172.18.50.0     | 255.255.255.240 | 172.18.50.14    |
| 60   | Admin/Gestion  | 172.18.60.0     | 255.255.255.240 | 172.18.60.14    |

### 2.2 Liaisons WAN (Série)

* **Lien R1 - R2 :** Réseau `10.0.30.176/30` (R1: .177, R2: .178)
* **Lien R1 - R3 :** Réseau `10.0.30.180/30` (R1: .181, R3: .182)
* **Lien R2 - R3 :** Réseau `10.0.30.184/30` (R2: .185, R3: .186)

---

## 3. Étapes de Réalisation

### Étape 1 : Configuration Layer 2 (Switching)
* Création des VLANs (10, 20, 30, 50, 60) sur les switchs S1 et S2.
* **EtherChannel :** Configuration du protocole LACP (mode active) sur les ports Fa0/21 et Fa0/22 (Channel-group 1).
* **Trunking :** Configuration du Port-channel 1 en mode Trunk (VLAN natif 50).

### Étape 2 : Routage Inter-VLAN (Router-on-a-Stick)
* Activation de l'interface `Fa0/0` sur R1.
* Création des sous-interfaces avec encapsulation dot1Q :
    * `Fa0/0.10` (VLAN 10)
    * `Fa0/0.20` (VLAN 20)
    * `Fa0/0.30` (VLAN 30)
    * `Fa0/0.50` (VLAN Natif)
    * `Fa0/0.60` (VLAN Admin)

### Étape 3 : Routage Statique WAN
* **R1 :** Ajout des routes statiques vers les réseaux des sites distants.
* **R2 & R3 :** Configuration d'une route par défaut vers R1 : `ip route 0.0.0.0 0.0.0.0 [IP_Next_Hop]`.

---

## 4. Tests et Validation

Les tests de connectivité suivants ont été validés (captures disponibles dans le dossier `/images`) :

1.  **Ping inter-VLAN :** Succès entre PC VLAN 10 et PC VLAN 20 (routage via R1).
2.  **Traceroute :** Vérification du saut via R1 pour atteindre les réseaux distants (`tracert 10.0.30.129`).
3.  **Gestion Réseau :** Ping réussi depuis R1 vers l'interface de gestion SVI du switch S2 (`172.18.60.2`).
4.  **Tables de routage :** Vérification de la présence des routes connectées (C) et statiques (S).

---

## 5. Livrables
Ce dépôt contient :
* 📄 **Rapport PDF** complet.
* 🔌 **Fichier Packet Tracer (.pkt)** finalisé.
  
**Réalisé par :** Imad Smahi
**Date :**  Décembre 2025
