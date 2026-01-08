🛡️ Cybersecurity HomeLab - Infrastructure Multi-Zone

Ce dépôt documente la conception, le déploiement et la sécurisation de mon laboratoire personnel de cybersécurité. L'objectif est de simuler un environnement d'entreprise pour tester des stratégies de défense, de détection et de durcissement (hardening).

🏗️ Architecture Réseau (3-Tier)

L'infrastructure est segmentée en trois zones distinctes via un pare-feu pfSense virtualisé :

WAN : Interface connectée à l'Internet public (Passerelle Freebox).

LAN_CORP (10.0.1.0/24) : Zone de confiance hébergeant l'Active Directory et les stations d'administration (Debian).

DMZ_WEB (10.0.2.0/24) : Zone exposée hébergeant les services applicatifs (Nextcloud, serveurs Web).

🛠️ Stack Technique

Hyperviseur : VirtualBox / VMware (Hôte : Ryzen 5 5600X, 32GB RAM).

Firewalling : pfSense (Stateful Packet Inspection, NAT, VPN, VLANs).

SOC / SIEM : Wazuh (HIDS/SIEM) pour la centralisation des logs et la détection d'intrusions.

Systèmes : Windows Server 2022 (AD en cours), Debian 12 (Hardened).

Filtrage DNS : Pi-hole (DNS Sinkhole) physique intégré via pfSense.

🔒 Implémentations de Sécurité

1. Segmentation & Zero Trust

Isolation physique et logique via pfSense.

Règles de pare-feu de type "Default Deny" sur toutes les interfaces.

Interdiction des mouvements latéraux (Anti-pivotage) entre DMZ et LAN.

2. Monitoring & Détection (SOC)

Centralisation des logs système vers une instance Wazuh (en cours).

Analyse de flux réseaux périmétriques.

3. Hardening (Durcissement)

Filtrage DNS : Redirection de l'ensemble des flux DNS du LAN vers un Sinkhole Pi-hole (192.168.1.201).

Accès Applicatifs : Flux restreints via des Aliases de ports spécifiques (ex: 8080 pour Nextcloud).

Historique de Déploiement (Changelog)

Étape 1 : Architecture réseau et déploiement du pare-feu pfSense. ✅

Étape 2 : Segmentation LAN/DMZ et configuration des règles de filtrage initiales. ✅

Étape 3 : (En cours) Installation de l'Active Directory, configuration DNS Forwarding et GPO de durcissement. 🔄

Structure du Dépôt

/config : Extraits de fichiers de configuration (pfSense XML, règles Wazuh).

/docs : Schémas d'architecture et procédures de remédiation.
