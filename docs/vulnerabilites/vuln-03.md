# Fiche Vulnérabilité N°03 — IRC (UnrealIRCd)

## 1. Contexte et Identification
- **Service cible** : IRC (UnrealIRCd)
- **Port d'écoute** : `6667/tcp`
- **Version détectée** : `UnrealIRCd 3.2.8.1`
- **Référence CVE** : `CVE-2010-2075`
- **Score CVSS v3** : `9.8 (Critique)`
- **Cible autorisée** : ESGIS VulnBox (`10.1.0.1`)

## 2. Observations Techniques
- **Description du composant** : Service identifié via le scan de bannières Nmap (`reports/nmap-services.txt`).
- **Vecteur d'exposition** : Port réseau direct accessible à travers le tunnel WireGuard (`10.1.0.1`).
- **Module Metasploit associé** : `exploit/unix/irc/unreal_ircd_3281_backdoor`

## 3. Preuves Réelles
> [!NOTE]
> *Cette section sera complétée uniquement avec les captures d'écran et sorties console obtenues lors de l'exercice encadré.*

- **Capture d'écran de l'analyse** : `screenshots/04-vulnerabilites/vuln-03-exec.png` *(En attente)*
- **Preuve technique / Résultat** : `screenshots/05-resultats/vuln-03-poc.png` *(En attente)*
- **Extrait de journal / Sortie console** :
```text
[En attente de vérification sur 10.1.0.1]
```

## 4. Mesures Correctives et Remédiation
- **Mise à jour logicielle** : Appliquer les correctifs de sécurité fournis par l'éditeur pour la version `UnrealIRCd 3.2.8.1`.
- **Principe de moindre privilège** : Exécuter le service sous un compte non privilégié.
- **Filtrage réseau** : Restreindre l'accès au port `6667` aux seuls hôtes d'administration autorisés.

---
**Statut actuel** : ⏳ *En attente de réalisation du test pédagogique*
