# Fiche Vulnérabilité N°04 — Apache Jserv Protocol

## 1. Contexte et Identification
- **Service cible** : Apache Jserv Protocol
- **Port d'écoute** : `8009/tcp`
- **Version détectée** : `Apache Jserv Protocol v1.3 (Tomcat)`
- **Référence CVE** : `CVE-2020-1938`
- **Score CVSS v3** : `9.8 (Critique)`
- **Cible autorisée** : ESGIS VulnBox (`10.1.0.1`)

## 2. Observations Techniques
- **Description du composant** : Service identifié via le scan de bannières Nmap (`reports/nmap-services.txt`).
- **Vecteur d'exposition** : Port réseau direct accessible à travers le tunnel WireGuard (`10.1.0.1`).
- **Module Metasploit associé** : `auxiliary/admin/http/tomcat_ghostcat`

## 3. Preuves Réelles
> [!NOTE]
> *Cette section sera complétée uniquement avec les captures d'écran et sorties console obtenues lors de l'exercice encadré.*

- **Capture d'écran de l'analyse** : `screenshots/04-vulnerabilites/vuln-04-exec.png` *(En attente)*
- **Preuve technique / Résultat** : `screenshots/05-resultats/vuln-04-poc.png` *(En attente)*
- **Extrait de journal / Sortie console** :
```text
[En attente de vérification sur 10.1.0.1]
```

## 4. Mesures Correctives et Remédiation
- **Mise à jour logicielle** : Appliquer les correctifs de sécurité fournis par l'éditeur pour la version `Apache Jserv Protocol v1.3 (Tomcat)`.
- **Principe de moindre privilège** : Exécuter le service sous un compte non privilégié.
- **Filtrage réseau** : Restreindre l'accès au port `8009` aux seuls hôtes d'administration autorisés.

---
**Statut actuel** : ⏳ *En attente de réalisation du test pédagogique*
