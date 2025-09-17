# 🌸 Jeu Robot Flower Princess

Bienvenue dans cet exercice ludique où vous allez programmer un robot pour qu'il livre une fleur à une princesse ! Ce défi combine l'apprentissage de Robot Framework avec un jeu de plateau stratégique.

## 🎯 Objectifs

À la fin de cet exercice, vous saurez :

- Utiliser Docker Compose
- Interagir avec des APIs de jeu en temps réel
- Gérer l'état d'un jeu tour par tour
- Implémenter un algorithme de pathfinding simple

## 🕰️ Durée

4h à 8h

## 🎮 Règles du jeu

**Robot Flower Princess** est un jeu de plateau stratégique pour 1 joueur.

### Objectif
🤖 **Mission :** Faire livrer une fleur à une princesse par votre robot !

### Éléments du plateau
- 🤖 **Robot (R)** : Votre personnage contrôlé
- 🌸 **Fleur (F)** : À récupérer et livrer
- 👸 **Princesse (P)** : Destination finale
- 🗑️ **Déchet (D)** : Cases à nettoyer
- ⬜ **Vide (V)** : Cases libres

### Actions possibles
1. **Se déplacer** : 1 case dans 4 directions (H/B/G/D)
2. **Nettoyer** : Transformer une case déchet en case libre
3. **Porter** : Ramasser la fleur
4. **Déposer** : Livrer la fleur (uniquement sur la case princesse)

### Contraintes
- ⚠️ Le robot ne peut se déplacer que sur les cases vides
- ⚠️ Le robot ne peut pas nettoyer s'il porte la fleur
- ⚠️ Un mouvement invalide fait perdre la partie
- ✅ Victoire quand la fleur est sur la case princesse

## 🐳 Installation avec Docker

### Étape 1 : Fichier Docker Compose

Créez un fichier `docker-compose.yml` pour orchestrer les services :

```yaml
services:
  backend:
    image: picardremi/robot-flower-princess:master
    ports:
      - "8000:8000"
    networks:
      - robot-flower-princess-network

  frontend:
    image: picardremi/robot-flower-princess-ui:latest
    ports:
      - "3000:80"
    depends_on:
      - backend
    networks:
      - robot-flower-princess-network

networks:
  robot-flower-princess-network:
    driver: bridge
```

### Étape 2 : Lancement des services

```bash
# Démarrer les services
docker-compose up -d

# Vérifier que les services sont en cours d'exécution
docker-compose ps

# Voir les logs si nécessaire
docker-compose logs -f

# Redémarrer les services
docker-compose restart

# Nettoyer et relancer
docker-compose down && docker-compose up -d
```

### Étape 3 : Vérification

Une fois les services démarrés, vérifiez l'accès :

- 📖 **API Swagger** : [http://localhost:8000/docs](http://localhost:8000/docs)
- 🎮 **Interface de jeu** : [http://localhost:3000](http://localhost:3000)

!!! tip "Conseil de débogage"
Utilisez l'interface web pour suivre visuellement l'avancement de votre partie pendant que Robot Framework joue !

## 📋 Exercices à réaliser

### Étape 1 : Configuration de base

Créez un fichier `robot_flower_princess.robot` avec la configuration de base.

!!! question "À faire"
1. Importez RequestsLibrary
2. Définissez l'URL de base de l'API
3. Créez une session HTTP
4. Testez la connexion à l'API

**Structure suggérée :**
```robot
*** Settings ***
# TODO: Importer RequestsLibrary

*** Variables ***
${API_BASE_URL}    http://localhost:8000

*** Test Cases ***
# Vos tests de jeu iront ici

*** Keywords ***
# Vos stratégies de jeu iront ici
```

### Étape 2 : Créer et explorer une partie

Implémentez les fonctions de base pour interagir avec l'API de jeu.

!!! question "À faire"
1. Créez un keyword pour démarrer une nouvelle partie
2. Récupérez l'ID de la partie créée
3. Créez un keyword pour récupérer l'état du plateau
4. Affichez le plateau sous forme lisible

!!! tip "Indices"
- `POST /games` retourne un JSON avec l'ID de la partie `game_id`
- `GET /games/{game_id}/board` retourne le plateau sous forme de chaîne.

### Étape 3 : Analyser le plateau

Créez des fonctions pour comprendre l'état du jeu.

!!! question "À faire"
1. Localisez les positions du robot, de la fleur et de la princesse
2. Identifiez les cases vides et les déchets
3. Créez une représentation interne du plateau
4. Implémentez une fonction pour calculer la distance entre deux points

!!! tip "Indices"
- Le plateau est une chaîne avec des retours à la ligne. Chaque ligne représente une rangée du plateau.
- Utilisez `Split String` pour traiter ligne par ligne
- Utilisez `Split String To Characters` pour récupérer les caractères (pièces) de chaque ligne
- Stockez les positions comme coordonnées (x, y)

### Étape 4 : Mouvements de base

Implémentez les actions de base du robot.

!!! question "À faire"
1. Créez un keyword pour déplacer le robot
2. Créez un keyword pour nettoyer une case
3. Créez un keyword pour ramasser la fleur
4. Créez un keyword pour déposer la fleur
5. Gérez les erreurs d'actions invalides

!!! tip "Indices"
- TOUTES les actions prennent une direction : Haut/Bas/Gauche/Droite (`H` / `B` / `G` / `D`)
- Vérifiez toujours le statut de la réponse

### Étape 5 : Navigation intelligente

Implémentez un algorithme pour naviguer vers une destination.

!!! question "À faire"
1. Créez un algorithme de pathfinding simple
2. Naviguez du robot vers la fleur
3. Gérez les obstacles (déchets) en les nettoyant

!!! tip "Indices"
- Commencez par un algorithme glouton (se rapprocher à chaque étape)
- Si une case déchet bloque, nettoyez-la d'abord
- Utilisez une boucle WHILE pour la navigation continue
- Arrêtez-vous quand vous atteignez la destination

### Étape 6 : Stratégie complète

Implémentez une stratégie complète pour gagner au jeu.

!!! question "À faire"
1. Combinez toutes les fonctions précédentes
2. Naviguez vers la fleur et ramassez-la
3. Naviguez vers la princesse avec la fleur
4. Déposez la fleur sur la case princesse
5. Vérifiez la victoire

!!! tip "Indices"
- Une partie se joue en deux phases : récupérer puis livrer
- Le robot ne peut pas nettoyer s'il porte la fleur
- Planifiez le chemin retour avant de récupérer la fleur

## 🔧 Structure minimale du test

```robot
*** Settings ***
Library     RequestsLibrary
Library     String
Library     Collections

*** Variables ***
${API_BASE_URL}    http://localhost:8000
${UI_URL}          http://localhost:3000

*** Test Cases ***
Jouer Une Partie Complète
    [Documentation]    Résoudre automatiquement une partie du jeu
    ${game_id}=    Démarrer Nouvelle Partie
    
    Log To Console    🎮 Partie créée ! Suivez sur ${UI_URL}
    Log To Console    📋 Game ID: ${game_id}
    
    Afficher Plateau Initial
    Résoudre Partie
    Vérifier Victoire

*** Keywords ***
Démarrer Nouvelle Partie
    [Documentation]    Crée une nouvelle partie et retourne l'ID
    # TODO: Implémenter
    [Return]    ${game_id}

Afficher Plateau Initial
    [Documentation]    Affiche l'état initial du plateau
    # TODO: Implémenter

Résoudre Partie
    [Documentation]    Stratégie complète pour gagner
    # Phase 1: Aller chercher la fleur
    Naviguer Vers Fleur
    Ramasser Fleur
    
    # Phase 2: Livrer à la princesse
    Naviguer Vers Princesse
    Livrer Fleur À Princesse

Naviguer Vers Fleur
    [Documentation]    Navigation intelligente vers la fleur
    # TODO: Implémenter pathfinding

Vérifier Victoire
    [Documentation]    Vérifie si la partie est gagnée
    # TODO: Implémenter
```

## 🎁 Défis bonus

### Défi 1 : Organisation
- Ajouter des ressources
- Utiliser les dataclasses Python 🐍

### Défi 2 : Optimisation
- Minimisez le nombre de mouvements total

### Défi 3 : Visualisation avancée
- Enregistrez chaque mouvement avec capture d'écran de l'UI avec Playwright

## 📖 API Reference complète

### Endpoints disponibles

| Méthode | Endpoint | Description |
|---------|----------|-------------|
| POST | `/games` | Créer une nouvelle partie |
| GET | `/games/{game_id}/board` | Récupérer l'état du plateau |
| POST | `/games/{game_id}/move` | Déplacer le robot |
| POST | `/games/{game_id}/clean` | Nettoyer une case |
| POST | `/games/{game_id}/pickup` | Ramasser la fleur |
| POST | `/games/{game_id}/drop` | Déposer la fleur |

### Paramètres de direction
- **H** : Haut
- **B** : Bas
- **G** : Gauche
- **D** : Droite

### Codes de plateau
- **R** : Robot 🤖
- **F** : Fleur 🌸
- **P** : Princesse 👸
- **D** : Déchet 🗑️
- **V** : Vide ⬜

## 🏆 Validation

Votre exercice est réussi si :
- ✅ Votre robot peut naviguer sur le plateau
- ✅ Vous avez affiché le plateau de façon claire
- ✅ Votre robot récupère la fleur automatiquement
- ✅ Votre robot livre la fleur à la princesse

Amusez-vous bien avec ce défi ! C'est l'occasion de combiner logique algorithmique et maîtrise de Robot Framework dans un contexte ludique et motivant 🎮🤖🌸