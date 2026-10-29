<h<div align="center">

# 🌐 Travail Pratique : Installation et Configuration des Services DHCP, DNS et SSH sous Fedora

<p>
  <img src="https://img.shields.io/badge/Niveau-2%C3%AA%20ann%C3%A9e%20OFPPT-blue?style=for-the-badge" alt="Niveau OFPPT">
  <img src="https://img.shields.io/badge/Syst%C3%A8me-Fedora%20Linux-51A2DA?style=for-the-badge&logo=fedora&logoColor=white" alt="Fedora Linux">
  <img src="https://img.shields.io/badge/Dur%C3%A9e-2h30-informational?style=for-the-badge" alt="Durée">
  <img src="https://img.shields.io/badge/Formateur-Hamza%20Boulafkhouda-orange?style=for-the-badge" alt="Formateur">
</p>

</div>

---

## 📋 Informations Générales

* **Établissement / Niveau** : 2ème année OFPPT (Infrastructure Digitale)[cite: 1]
* **Support** : Fedora / Linux[cite: 1]
* **Formateur** : Hamza Boulafkhouda[cite: 1]
* **Objectif Général** : Installer, configurer et tester les services réseau **DHCP**, **DNS** et **SSH** sur un serveur Fedora en utilisant le terminal, les fichiers de configuration et le pare-feu (`firewalld`).[cite: 1]

---

## 🛠️ 1. Préparation du Serveur

Paramétrage initial de la machine pour configurer l'environnement réseau de base.

| Paramètre | Valeur Demandée |
| :--- | :--- |
| **Nom d'hôte (Hostname)** | `srv-ofppt`[cite: 1] |
| **Adresse IPv4 fixe** | `192.168.10.10/24`[cite: 1] |
| **Passerelle (Gateway)** | `192.168.10.1`[cite: 1] |
| **Domaine DNS** | `ofppt.local`[cite: 1] |
| **Réseau local** | `192.168.10.0/24`[cite: 1] |

### Étapes de Réalisation :
1. Ouvrir un terminal et passer en mode administrateur (`su -` ou `sudo -i`).[cite: 1]
2. Afficher le nom d'hôte actuel, puis le modifier en `srv-ofppt`.[cite: 1]
3. Afficher les interfaces réseau et identifier l'interface connectée.[cite: 1]
4. Configurer l'adresse IP fixe `192.168.10.10/24` et la passerelle sur l'interface appropriée.[cite: 1]
5. Vérifier la configuration IP et la table de routage.[cite: 1]
6. Tester la connectivité vers la passerelle (`ping`).[cite: 1]
7. Vérifier l'état du pare-feu, puis activer et démarrer `firewalld` si nécessaire.[cite: 1]

> **À compléter sur la feuille de TP :**
> * Commande de modification du hostname : 
> * Nom de l'interface réseau : 
> * Méthode de configuration IP : 

---

## ⚡ 2. Installation et Configuration du Serveur DHCP

Le serveur DHCP doit distribuer automatiquement des adresses IP aux postes clients du réseau local.[cite: 1]

| Paramètre | Valeur Demandée |
| :--- | :--- |
| **Plage d'adresses** | `192.168.10.100` à `192.168.10.200`[cite: 1, 2] |
| **Masque de sous-réseau** | `255.255.255.0`[cite: 1, 2] |
| **Passerelle distribuée** | `192.168.10.1`[cite: 2] |
| **DNS distribué** | `192.168.10.10`[cite: 2] |
| **Durée du bail** | `600` secondes[cite: 2] |

### Étapes de Réalisation :
1. Installer le paquet du serveur DHCP (`dhcp-server`).[cite: 2]
2. Identifier et ouvrir le fichier de configuration DHCP (`/etc/dhcp/dhcpd.conf`).[cite: 2]
3. Ajouter le bloc de configuration du réseau `192.168.10.0/24`.[cite: 2]
4. Définir la plage d'adresses, le masque, la passerelle et le serveur DNS.[cite: 2]
5. Configurer la durée du bail à 600 secondes.[cite: 2]
6. Vérifier la syntaxe du fichier de configuration.[cite: 2]
7. Démarrer le service DHCP et activer son démarrage automatique.[cite: 2]
8. Autoriser le service DHCP dans le pare-feu (`firewalld`) et recharger les règles.[cite: 2]
9. Vérifier l'état du service et consulter ses journaux (`journalctl`).[cite: 2]
10. Vérifier si le port UDP 67 est en écoute (`ss -tulnp`).[cite: 2]

> **À compléter sur la feuille de TP :**
> * Paquet installé : 
> * Nom du service : 
> * Fichier modifié : 
> * Commande de consultation des journaux : 

---

## 🔍 3. Installation et Configuration du Serveur DNS

Installation de **BIND** (`named`) et configuration d'une zone directe pour le domaine `ofppt.local`.[cite: 3]

| Nom DNS | Adresse IPv4 |
| :--- | :--- |
| `ns1.ofppt.local` | `192.168.10.10`[cite: 3] |
| `www.ofppt.local` | `192.168.10.20`[cite: 3] |
| `ftp.ofppt.local` | `192.168.10.30`[cite: 3] |

### Étapes de Réalisation :
1. Installer le serveur DNS BIND et ses outils (`bind`, `bind-utils`).[cite: 3]
2. Identifier le fichier principal de configuration de BIND (`/etc/named.conf`).[cite: 3]
3. Déclarer une zone directe appelée `ofppt.local`.[cite: 3]
4. Créer le fichier de zone correspondant et définir l'enregistrement SOA.[cite: 3]
5. Ajouter l'enregistrement NS et les trois enregistrements A du tableau ci-dessus.[cite: 3]
6. Vérifier la syntaxe du fichier principal (`named-checkconf`) et du fichier de zone (`named-checkzone`).[cite: 3]
7. Démarrer le service DNS et activer son démarrage automatique.[cite: 3]
8. Autoriser le service DNS dans le pare-feu et recharger les règles.[cite: 3]
9. Tester la résolution de `www.ofppt.local` en interrogeant le serveur DNS `192.168.10.10` (`nslookup` ou `dig`).[cite: 3]
10. Tester la résolution de `ftp.ofppt.local` et consulter les journaux en cas d'erreur.[cite: 3]

> **À compléter sur la feuille de TP :**
> * Paquet DNS : 
> * Fichier principal : 
> * Fichier de zone : 
> * Port DNS : 
> * Type d'enregistrement nom -> IPv4 : 

---

## 🔒 4. Installation et Configuration du Serveur SSH

Permettre à l'administrateur de se connecter à distance au serveur Fedora de manière sécurisée.[cite: 3]

| Paramètre | Valeur Demandée |
| :--- | :--- |
| **Utilisateur autorisé** | `admin`[cite: 3] |
| **Port SSH** | `2222/TCP`[cite: 3] |
| **Connexion directe de root** | Interdite (`no`)[cite: 3] |

### Étapes de Réalisation :
1. Installer le paquet du serveur SSH (`openssh-server`).[cite: 3]
2. Vérifier la présence du fichier de configuration `/etc/ssh/sshd_config`.[cite: 3]
3. Créer l'utilisateur `admin` et définir son mot de passe (`useradd`, `passwd`).[cite: 3]
4. Modifier le fichier de configuration SSH pour utiliser le port `2222`.[cite: 3]
5. Interdire la connexion directe de root (`PermitRootLogin no`) et autoriser l'utilisateur `admin` (`AllowUsers admin`).[cite: 3]
6. Vérifier la syntaxe de la configuration avant de redémarrer le service (`sshd -t`).[cite: 4]
7. Démarrer le service SSH et activer son démarrage automatique.[cite: 4]
8. Autoriser le port TCP `2222` dans le pare-feu (`firewalld`) et recharger les règles.[cite: 4]
9. Vérifier que SSH écoute bien sur le port configuré.[cite: 4]
10. Depuis un autre poste, tester la connexion à l'adresse `192.168.10.10` avec l'utilisateur `admin` et le port `2222`.[cite: 4]
11. Générer une paire de clés SSH (`ssh-keygen`) et copier la clé publique vers le serveur distant (`ssh-copy-id`).[cite: 4]
12. Consulter les journaux du service SSH en cas de problème.[cite: 4]

> **À compléter sur la feuille de TP :**
> * Paquet installé : 
> * Fichier modifié : 
> * Directive de port : 
> * Directive interdisant root : 
> * Commande de vérification de configuration : 
> * Commande de connexion à distance : 

---

<div align="center">

### Fin du TP
*Remettre les commandes utilisées et les fichiers de configuration modifiés au formateur.*[cite: 4]

</div>
