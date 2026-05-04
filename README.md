🛡️ Cybersecurity HomeLab - Infrastructure Multi-Zone & SOC

Ce dépôt documente la conception, le déploiement et la sécurisation de mon laboratoire personnel de cybersécurité. L'objectif est de simuler un environnement d'entreprise critique pour tester des stratégies de défense, de détection et de durcissement (Hardening).

🚀 Pourquoi ce projet ?

En tant que futur ingénieur à l'IMT Nord Europe (ou ESIEA) et actuellement en poste chez OVHcloud, je suis convaincu que la cybersécurité doit être intégrée dès la couche physique et réseau (Security by Design). Ce lab me permet d'expérimenter des architectures résilientes hors production.

🏗️ Architecture Réseau (3-Tier)

L'infrastructure est segmentée logiquement via un pare-feu pfSense virtualisé :

WAN : Interface connectée à l'Internet public (Passerelle Freebox).

LAN_CORP (10.0.1.0/24) : Zone de confiance hébergeant l'Active Directory et les stations d'administration (Debian).

DMZ_WEB (10.0.2.0/24) : Zone exposée isolée hébergeant les services applicatifs (Nextcloud, Docker).

IoT_ISOLATION : Segment dédié aux objets connectés pour limiter la surface d'attaque.

🛠️ Stack Technique

Hyperviseur : VirtualBox / VMware (Hôte : Ryzen 5 5600X, 32GB RAM).

Firewalling : pfSense (Règles d'état, NAT, VPN WireGuard, VLANs 802.1Q).

SOC / SIEM : Stack Wazuh (Manager & Indexer) pour la corrélation de logs et la détection d'intrusions (HIDS/FIM).

Systèmes : Windows Server 2022 (AD DS & Hardening terminés), Debian 12 (Hardened).

Filtrage DNS : Pi-hole physique intégré comme DNS Sinkhole périmétrique.

🔒 Implémentations de Sécurité

1. Segmentation & Zero Trust

Mise en œuvre d'une politique Default Deny sur tous les segments.

Isolation stricte de la DMZ : interdiction totale des mouvements latéraux vers le LAN critique.

2. Surveillance Active (SOC)

Centralisation des logs d'authentification et de filtrage vers Wazuh.

Configuration d'alertes en temps réel sur les tentatives de brute-force SSH/RDP.

3. Durcissement Système (Hardening ANSSI)

Active Directory :

Promotion du serveur en tant que Contrôleur de Domaine racine (lab.fahem.local).

Désactivation des protocoles obsolètes et vulnérables (NetBIOS over TCP/IP et LLMNR) via GPO pour neutraliser les attaques par empoisonnement (type Responder).

Configuration de redirecteurs DNS vers pfSense/Pi-hole pour assurer une résolution de noms filtrée.

Linux : Durcissement SSH (clés uniquement, désactivation root) et protection proactive via Fail2Ban.

📈 Historique de Déploiement

Étape 1 : Architecture réseau et déploiement du pare-feu pfSense.

Étape 2 : Segmentation LAN/DMZ et configuration des règles de filtrage initiales (Zero Trust).

Étape 3 : Déploiement de Windows Server 2022, promotion AD DS et application des premières politiques de durcissement.

📂 Structure du Dépôt

/config : Extraits de fichiers de configuration (pfSense XML, règles Wazuh, scripts GPO).

/docs : Schémas d'architecture et procédures de remédiation.
