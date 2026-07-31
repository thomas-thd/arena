# MITRE ATT&CK — Guide Éducatif Complet

## Qu'est-ce que MITRE ATT&CK ?

MITRE ATT&CK (Adversarial Tactics, Techniques & Common Knowledge) est un **référentiel mondial ouvert** créé par la MITRE Corporation. Il décrit le comportement des attaquants informatiques à travers le cycle de vie d'une intrusion.

Le framework se structure en **3 niveaux hiérarchiques** :

1. **Tactique** (TAxxxx) — L'objectif que l'attaquant veut atteindre (ex : obtenir un accès initial).
2. **Technique** (Txxxx) — La méthode générale utilisée pour atteindre cet objectif.
3. **Sous-technique** (Txxxx.xxx) — La variante précise d'une technique.

---

## Les 14 Tactiques (Cycle d'attaque complet)

### 1. Reconnaissance (TA0043)
**Définition** : Collecte d'informations avant l'attaque.  
**Exemples réels** : Scan de ports, recherche sur LinkedIn pour identifier des employés, analyse des certificats SSL, recherche de sous-domaines.  
**Techniques clés** :
- T1595 — Scan actif (recherche de ports et services ouverts)
- T1593 — Recherche sur sites ouverts (bases publiques, réseaux sociaux)
- T1592 — Informations sur la victime (identité des employés, technologies utilisées)
- T1590 — Découverte du réseau

**Défense** : Limiter l'exposition publique, surveiller les scans de ports, former au phishing informatif.

---

### 2. Développement des ressources (TA0042)
**Définition** : Préparation des outils et infrastructures nécessaires.  
**Exemples réels** : Achat de domaines malveillants, création de certificats SSL frauduleux, développement d'outils personnalisés.  
**Techniques clés** :
- T1583 — Acquisition d'infrastructure (serveurs, domaines, IPs)
- T1584 — Compromission d'infrastructure existante
- T1588 — Acquisition de capacités (exploits, malware)

**Défense** : Systèmes de réputation de domaines, surveillance des enregistrements de domaines, audit des infrastructures.

---

### 3. Accès initial (TA0001)
**Définition** : Premier point d'entrée dans le réseau.  
**Exemples réels** : Phishing par email (SolarWinds utilisait des techniques avancées d'accès initial), exploitation d'une application web publique non patchée.  
**Techniques clés** :
- T1566 — Phishing (lien, pièce jointe, service)
- T1190 — Exploitation d'application publique
- T1078 — Comptes valides (identifiants déjà volés)
- T1133 — Services externes distants

**Défense** : Authentification multifacteur (MFA), mises à jour régulières, formation au phishing, segmentation réseau.

---

### 4. Exécution (TA0002)
**Définition** : Lancement du code malveillant sur le système.  
**Exemples réels** : PowerShell lancé par une macro, script Python téléchargé, commande shell dans un conteneur.  
**Techniques clés** :
- T1059 — Interpréteur de commandes et scripts (PowerShell, Bash, Python)
- T1204 — Exécution par l'utilisateur (lancement volontaire d'un malware)
- T1053 — Tâche planifiée / Job
- T1203 — Exploitation pour exécution client

**Défense** : Restreindre les scripts non signés, désactiver les macros par défaut, surveiller les processus enfants inhabituels.

---

### 5. Persistance (TA0003)
**Définition** : Maintenir l'accès après un redémarrage ou un changement de mot de passe.  
**Exemples réels** : Création d'une tâche planifiée qui lance un payload au démarrage, modification du registre Windows (Run keys), installation d'un service.  
**Techniques clés** :
- T1053 — Tâche planifiée
- T1547 — Autostart au démarrage (registre, dossiers)
- T1136 — Création de compte
- T1543 — Création ou modification de service

**Défense** : Auditer régulièrement les tâches et services, surveiller le registre de démarrage, utiliser des outils EDR.

---

### 6. Élévation de privilèges (TA0004)
**Définition** : Passer d'un compte standard à un administrateur ou système.  
**Exemples réels** : Injection dans un processus système, contournement de UAC, manipulation de tokens d'accès.  
**Techniques clés** :
- T1055 — Injection de processus
- T1548 — Abus du contrôle d'élévation (UAC bypass)
- T1134 — Manipulation de tokens d'accès
- T1068 — Exploitation d'élévation de privilèges

**Défense** : Principe du moindre privilège, surveillance de sudo/admin, mises à jour contre exploits connus.

---

### 7. Évasion de défense (TA0005)
**Définition** : Éviter la détection par antivirus, EDR et analystes.  
**Exemples réels** : Fichiers compressés et chiffrés, désactivation d'EDR, suppression des journaux d'événements, masquage de processus.  
**Techniques clés** :
- T1562 — Altération des défenses (désactivation d'outils)
- T1027 — Fichiers ou informations obscurcis (compression, chiffrement, stéganographie)
- T1070 — Suppression d'indicateurs (effacement des journaux)
- T1036 — Masquage (renommer un processus malveillant)

**Défense** : EDR comportemental, protection contre la désactivation, journaux immuables (WORM), analyse de mémoire.

---

### 8. Accès aux crédentiels (TA0006)
**Définition** : Vol de mots de passe, tokens, certificats, clés.  
**Exemples réels** : Dumping de LSASS (Mimikatz), brute-force sur RDP, extraction depuis navigateurs (Chrome, Firefox), vol de clés de registre.  
**Techniques clés** :
- T1003 — Dumping des crédentiels OS (LSASS, NTDS, LSA Secrets)
- T1110 — Force brute
- T1555 — Crédentiels dans des magasins de mots de passe
- T1528 — Vol de token d'application

**Défense** : Authentification multifacteur, Credential Guard, surveillance des accès aux magasins de mots de passe, limitation des privilèges administratifs.

---

### 9. Découverte (TA0007)
**Définition** : Exploration du réseau et du système pour planifier la suite.  
**Exemples réels** : Lister les comptes utilisateurs, scanner le réseau, identifier les partages, découvrir les services.  
**Techniques clés** :
- T1083 — Découverte de fichiers et répertoires
- T1018 — Découverte de systèmes distants
- T1046 — Découverte de services réseau
- T1033 — Découverte du propriétaire du système

**Défense** : Limiter la visibilité inter-systèmes, surveiller les requêtes d'énumération, segmentation réseau.

---

### 10. Mouvement latéral (TA0008)
**Définition** : Déplacement de système en système dans le réseau.  
**Exemples réels** : Connexion RDP d'un poste à un serveur, copie via SMB/Windows Admin Shares, utilisation de SSH, passage du hash (Pass the Hash).  
**Techniques clés** :
- T1021 — Services distants (RDP, SMB, SSH, VNC)
- T1550 — Utilisation de matériel alternatif (hash, ticket Kerberos)
- T1133 — Services externes distants
- T1210 — Exploitation de services distants

**Défense** : Segmentation réseau, limitation du RDP et des services administratifs, surveillance des connexions inter-systèmes, utilisation de jump hosts.

---

### 11. Collecte (TA0009)
**Définition** : Rassemblement des données ciblées.  
**Exemples réels** : Copie de fichiers sensibles, capture d'écran, enregistrement audio, collecte d'emails, extraction depuis bases de données.  
**Techniques clés** :
- T1005 — Données du système local
- T1113 — Capture d'écran
- T1123 — Capture audio
- T1213 — Données depuis des dépôts d'informations (SharePoint, bases)

**Défense** : Classification des données, chiffrement au repos et en transit, surveillance des accès massifs.

---

### 12. Commandement et contrôle — C2 (TA0011)
**Définition** : Canal de communication avec le système compromis.  
**Exemples réels** : Trafic HTTPS vers un serveur contrôlé, tunnel DNS, utilisation de WebSocket, communication via des services cloud (Discord, Slack, Dropbox).  
**Techniques clés** :
- T1071 — Protocole applicatif (HTTP, HTTPS, DNS)
- T1090 — Canal chiffré ou tunnel
- T1572 — Utilisation de protocoles standard (masquage)
- T1568 — Résolution dynamique (Domain Generation Algorithms)

**Défense** : DNS filtering, analyse du trafic réseau, détection de patterns anormaux de volume et timing, utilisation de proxy avec inspection SSL.

---

### 13. Exfiltration (TA0010)
**Définition** : Transfert des données volées hors du réseau.  
**Exemples réels** : Envoi vers un serveur web contrôlé, utilisation de services cloud légitimes (Google Drive, Dropbox), exfiltration via le canal C2 existant.  
**Techniques clés** :
- T1041 — Exfiltration sur canal C2
- T1567 — Exfiltration sur service web
- T1048 — Exfiltration sur autre réseau (Bluetooth, WiFi)
- T1020 — Exfiltration automatisée

**Défense** : Solutions DLP (Data Loss Prevention), surveillance des transferts anormaux, quotas de bande passante, inspection du trafic sortant.

---

### 14. Impact (TA0040)
**Définition** : Perturbation, destruction ou manipulation des systèmes et données.  
**Exemples réels** : Ransomware (chiffrement des données), suppression massive de fichiers, arrêt de services critiques, corruption de données.  
**Techniques clés** :
- T1486 — Données chiffrées pour impact (ransomware)
- T1489 — Arrêt de service
- T1490 — Inhibition de la récupération (suppression des sauvegardes)
- T1529 — Arrêt du système

**Défense** : Sauvegardes hors ligne et testées régulièrement, surveillance des suppressions massives, isolation rapide des systèmes compromis, plans de reprise d'activité.

---

## Comment utiliser ATT&CK pour se défendre ?

### 1. Cartographier (Coverage Mapping)
Comparez vos outils de sécurité (EDR, SIEM, pare-feu, IDS) aux techniques ATT&CK. Identifiez quelles techniques ne sont pas couvertes par vos contrôles actuels.

### 2. Détecter (Detection Engineering)
Créez des règles de détection basées sur des **comportements réels** (techniques ATT&CK) plutôt que sur des signatures malveillantes fixes. Par exemple : détecter un processus enfant PowerShell lancé par Word (indicateur d'exécution de macro malveillante).

### 3. Simuler (Adversary Emulation / Red Teaming)
Utilisez le framework pour simuler des attaques réalistes. Par exemple, simulez un groupe APT connu (APT29, APT28) en suivant ses techniques documentées dans ATT&CK.

### 4. Prioriser (Threat Intelligence)
Concentrez vos ressources sur les tactiques et techniques les plus utilisées par les groupes de menaces actifs dans votre secteur d'activité.

---

## Exemples d'attaques réelles mappées sur ATT&CK

### NotPetya (2017)
- **Reconnaissance** : Scan de réseau
- **Accès initial** : Exploitation de la mise à jour MeDoc (fournisseur ukrainien)
- **Exécution** : Code injecté dans le processus système
- **Persistance** : Tâches planifiées
- **Élévation** : Exploitation de vulnérabilités locales
- **Évasion** : Suppression d'indicateurs
- **Mouvement latéral** : Propagation via EternalBlue et PsExec
- **Impact** : Chiffrement de données (ransomware masqué)

### SolarWinds (2020)
- **Développement** : Compromission de la chaîne d'approvisionnement
- **Accès initial** : Mise à jour malveillante distribuée
- **Persistance** : Services et tâches modifiés
- **Évasion** : Utilisation de noms de processus légitimes
- **C2** : Communication HTTPS vers des domaines contrôlés
- **Collecte** : Accès aux données sensibles dans le cloud
- **Exfiltration** : Transfert progressif des données

---

## Ressources supplémentaires

- Site officiel : https://attack.mitre.org/
- MITRE ATT&CK Navigator (outil de visualisation) : https://mitre-attack.github.io/attack-navigator/
- MITRE Engage (défense contre ATT&CK) : https://engage.mitre.org/
- MITRE D3FEND (défenses) : https://d3fend.mitre.org/

---

*Document éducatif créé pour l'apprentissage. Source : MITRE Corporation. Ce document n'est pas affilié officiellement à MITRE.*
