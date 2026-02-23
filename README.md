# Scanner de Réseau ARP avec Scapy

Un script Python simple et puissant pour découvrir tous les appareils connectés à votre réseau local. En utilisant des requêtes ARP de bas niveau via la bibliothèque Scapy, cet outil identifie rapidement les hôtes actifs et affiche leurs adresses IP et MAC correspondantes.

## Fonctionnalités Clés

  - **Découverte d'Hôtes sur le Réseau Local** : Scanne une plage d'adresses IP spécifiée (ex: `192.168.1.1/24`) pour trouver tous les appareils qui y répondent. (implémenté dans `main.py`)
  - **Utilisation de Requêtes ARP** : Envoie des paquets ARP de diffusion (`broadcast`) pour identifier les appareils. Cette méthode est particulièrement efficace et fiable sur les réseaux locaux. (implémenté dans `main.py` avec les couches `ARP` et `Ether`).
  - **Affichage des Adresses IP et MAC** : Récupère et affiche une liste claire de chaque appareil détecté, associant son adresse IP à son adresse MAC (physique). (implémenté dans la boucle de traitement des résultats de `main.py`).
  - **Léger et Contrôlé** : Repose uniquement sur Scapy pour forger et envoyer des paquets, offrant un contrôle précis sans la complexité d'outils de scan plus lourds.

## Comment ça marche ?

Le script suit un processus de découverte réseau en trois étapes simples :

1.  **Création du Paquet** : Un paquet ARP est forgé pour demander "qui possède cette adresse IP ?" pour chaque adresse de la plage spécifiée. Ce paquet est encapsulé dans une trame Ethernet de diffusion pour être envoyé à tous les appareils du réseau.
2.  **Envoi et Réception** : Le paquet est envoyé sur le réseau, et le script écoute les réponses pendant quelques secondes.
3.  **Analyse des Réponses** : Chaque appareil actif répond avec son adresse IP et son adresse MAC. Le script collecte ces réponses et les affiche dans un tableau formaté.

## Configuration et Exemple de Sortie

La seule configuration requise se fait directement dans le fichier `main.py`.

### Configuration

Modifiez la variable `target_ip` pour définir la plage réseau que vous souhaitez scanner.

```python
# exemple pour un réseau domestique standard
target_ip = "192.168.1.1/24" 
```

### Exemple de Sortie

Après exécution, le script affichera une liste des appareils trouvés dans la console :

```
Available devices in the network:
IP                MAC
192.168.1.1       0a:1b:2c:3d:4e:5f
192.168.1.102     a1:b2:c3:d4:e5:f6
192.168.1.134     10:20:30:40:50:60
```

## Installation

1.  Clonez ce dépôt sur votre machine locale.
2.  Il est recommandé de créer un environnement virtuel Python.
    ```bash
    python3 -m venv .venv
    source .venv/bin/activate
    ```
3.  Installez les dépendances nécessaires :
    ```bash
    pip install -r requirements.txt
    ```
4.  Exécutez le script avec des privilèges administrateur, car Scapy en a besoin pour envoyer des paquets bruts :
    ```bash
    sudo python3 main.py
    ```

## Prérequis

  - **Python 3**
  - **pip** (le gestionnaire de paquets Python)
  - **Privilèges administrateur (root)** : L'exécution avec `sudo` est indispensable pour permettre à Scapy d'accéder aux sockets réseau de bas niveau.
  - **Dépendances système pour Scapy** : Sur certaines distributions Linux, vous devrez peut-être installer des bibliothèques de capture de paquets.
    ```bash
    # Pour Debian/Ubuntu
    sudo apt install python3-scapy
    ```

## Licence

Ce projet est distribué sous la **licence MIT**.

## Stack

[![Stack](https://skillicons.dev/icons?i=py,linux&theme=dark)](https://skillicons.dev)
