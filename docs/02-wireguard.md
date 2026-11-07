# 02 - Connexion VPN WireGuard

## 1. Objectif
Établir une liaison VPN sécurisée via WireGuard entre la machine attaquante (Kali Linux) et le réseau d'entraînement OURITEK / ESGIS afin de joindre la machine cible ESGIS VulnBox (`10.1.0.1`).

## 2. Prérequis
- Paquet `wireguard` et `wireguard-tools` installés sur Kali Linux.
- Fichier de configuration WireGuard fourni par les administrateurs du lab (ex. `etudiant5.conf` conservé hors du dépôt Git conformément aux règles de sécurité).
- Accès Internet actif.

## 3. Procédure
1. Placement du fichier de configuration dans `/etc/wireguard/` (hors du répertoire Git).
2. Démarrage de l'interface WireGuard via `wg-quick` :
   ```bash
   sudo wg-quick up wg0 # ou nom de l'interface associée
   ```
3. Vérification du statut de la liaison :
   ```bash
   sudo wg show
   ip addr show
   ```
4. Test de connectivité vers la passerelle ou la cible autorisée (`10.1.0.1`) :
   ```bash
   ping -c 4 10.1.0.1
   ```

## 4. Captures d'écran
*Emplacement réservé aux captures d'écran de la session active :*
- Statut de la commande `wg show` : `screenshots/02-wireguard/01-wg-status.png` *(En attente)*
- Ping vers 10.1.0.1 : `screenshots/02-wireguard/02-ping-target.png` *(En attente)*

## 5. Résultat observé
*(Section en attente d'exécution et de validation)*

## 6. Analyse technique
*(Section en attente de validation de la liaison)*

## 7. Recommandations éventuelles
- Veiller à ne jamais commiter de fichier de configuration contenant des clés privées ou des adresses IP d'infrastructure sensible.
- Couper le tunnel une fois la session de laboratoire terminée : `sudo wg-quick down <interface>`.
