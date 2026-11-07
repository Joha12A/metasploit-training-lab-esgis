# Fiche Vulnérabilité N°10 — OpenSSH

## 1. Contexte et Identification
- **Service cible** : OpenSSH
- **Port d'écoute** : `22/tcp`
- **Version détectée** : `OpenSSH 8.2p1 Ubuntu`
- **Référence CVE** : `CVE-2020-15778`
- **Score CVSS v3** : `7.8 (Élevé)`
- **Cible autorisée** : ESGIS VulnBox (`10.1.0.1`)

## 2. Observations Techniques
- **Description du composant** : Service identifié via le scan de bannières Nmap (`reports/nmap-services.txt`).
- **Vecteur d'exposition** : Port réseau direct accessible à travers le tunnel WireGuard (`10.1.0.1`).
- **Module Metasploit associé** : `auxiliary/scanner/ssh/ssh_enumusers`

## 3. Preuves Réelles
> [!NOTE]
> *Cette section sera complétée uniquement avec les captures d'écran et sorties console obtenues lors de l'exercice encadré.*

- **Capture d'écran de l'analyse** : `screenshots/04-vulnerabilites/vuln-10-exec.png` *(En attente)*
- **Preuve technique / Résultat** : `screenshots/05-resultats/vuln-10-poc.png` *(En attente)*
- **Extrait de journal / Sortie console** :
```text
[En attente de vérification sur 10.1.0.1]
```

## 4. Mesures Correctives et Remédiation
- **Mise à jour logicielle** : Appliquer les correctifs de sécurité fournis par l'éditeur pour la version `OpenSSH 8.2p1 Ubuntu`.
- **Principe de moindre privilège** : Exécuter le service sous un compte non privilégié.
- **Filtrage réseau** : Restreindre l'accès au port `22` aux seuls hôtes d'administration autorisés.

---
**Statut actuel** : ⏳ *En attente de réalisation du test pédagogique*
