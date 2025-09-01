# Test de l'API Booker

Dans cet exercice pratique, vous allez apprendre à tester une API REST avec Robot Framework en utilisant l'API Booker, une API de démonstration pour la gestion de réservations d'hôtel.

## 🎯 Objectifs

À la fin de cet exercice, vous saurez :

- Installer et utiliser la RequestsLibrary
- Effectuer des requêtes HTTP (GET, POST, PUT, DELETE)
- Gérer l'authentification API
- Valider les réponses JSON
- Organiser vos tests API

## 📚 Documentation de l'API

L'API Booker est disponible à l'adresse : [https://restful-booker.herokuapp.com/](https://restful-booker.herokuapp.com/)

Documentation complète : [https://restful-booker.herokuapp.com/apidoc/index.html](https://restful-booker.herokuapp.com/apidoc/index.html)

### Endpoints principaux
- **GET /booking** - Liste toutes les réservations
- **POST /booking** - Crée une nouvelle réservation
- **GET /booking/{id}** - Récupère une réservation spécifique
- **PUT /booking/{id}** - Met à jour une réservation (authentification requise)
- **DELETE /booking/{id}** - Supprime une réservation (authentification requise)
- **POST /auth** - Génère un token d'authentification

## 📋 Exercices à réaliser

### Étape 1 : Installation de RequestsLibrary

Votre première mission est d'installer la bibliothèque nécessaire pour effectuer des requêtes HTTP.

!!! question "À faire"
Installez la bibliothèque RequestsLibrary dans votre environnement virtuel.

    **Indice :** Utilisez pip pour installer `robotframework-requests`

### Étape 2 : Configuration de base

Créez un fichier `test_api_booker.robot` avec la structure de base.

!!! question "À faire"
1. Importez la RequestsLibrary dans la section `*** Settings ***`
2. Définissez l'URL de base de l'API comme variable
3. Créez une session HTTP réutilisable

**Structure suggérée :**
```robot
*** Settings ***
# TODO: Importer la bibliothèque nécessaire

*** Variables ***
# TODO: Définir l'URL de base de l'API

*** Test Cases ***
# Vos tests iront ici

*** Keywords ***
# Vos mots-clés personnalisés iront ici
```

### Étape 3 : Créer une réservation

Implémentez un test pour créer une nouvelle réservation.

!!! question "À faire"
1. Créez un test case nommé `Créer Une Nouvelle Réservation`
2. Définissez les données de réservation (nom, prénom, prix total, etc.)
3. Effectuez une requête POST vers `/booking`
4. Vérifiez que la réponse a un statut 200
5. Vérifiez que la réponse contient un `bookingid`
6. Stockez l'ID de réservation pour les tests suivants

**Données de test suggérées :**
```json
{
    "firstname": "John",
    "lastname": "Doe",
    "totalprice": 150,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2024-01-01",
        "checkout": "2024-01-03"
    },
    "additionalneeds": "Breakfast"
}
```

!!! tip "Indices"
- Utilisez le mot-clé `POST` pour effectuer la requête
- Le paramètre `json` permet d'envoyer des données JSON
- Utilisez `Set Variable` pour stocker l'ID de réservation

### Étape 4 : Récupérer la réservation

Créez un test pour récupérer la réservation que vous venez de créer.

!!! question "À faire"
1. Créez un test case nommé `Récupérer La Réservation`
2. Utilisez l'ID de réservation stocké précédemment
3. Effectuez une requête GET vers `/booking/{id}`
4. Vérifiez le statut de la réponse
5. Validez que les données retournées correspondent à celles créées

!!! tip "Indices"
- Utilisez `GET` pour la requête
- Vérifiez les valeurs JSON avec des assertions appropriées
- Pensez à gérer le cas où l'ID n'existe pas

### Étape 5 : Authentification

Avant de pouvoir modifier ou supprimer une réservation, vous devez vous authentifier.

!!! question "À faire"
1. Créez un keyword `Obtenir Token Authentification`
2. Effectuez une requête POST vers `/auth` avec les credentials
3. Récupérez le token depuis la réponse
4. Stockez le token pour les requêtes suivantes

**Credentials par défaut :**
```json
{
    "username": "admin",
    "password": "password123"
}
```

!!! tip "Indices"
- La réponse contient un champ `token`
- Stockez le token comme variable de test ou de suite
- Vous utiliserez ce token dans les headers des requêtes suivantes

### Étape 6 : Modifier la réservation

Implémentez un test pour modifier une réservation existante.

!!! question "À faire"
1. Créez un test case `Modifier La Réservation`
2. Obtenez d'abord un token d'authentification
3. Définissez de nouvelles données de réservation
4. Effectuez une requête PUT avec le token dans les headers
5. Vérifiez que la modification a réussi

!!! tip "Indices"
- Utilisez le header `Cookie: token=VOTRE_TOKEN` pour l'authentification
- Vous pouvez aussi utiliser `Authorization: Basic YWRtaW46cGFzc3dvcmQxMjM=`
- Modifiez quelques champs comme le prix ou les dates

### Étape 7 : Supprimer la réservation

Créez un test pour supprimer la réservation.

!!! question "À faire"
1. Créez un test case `Supprimer La Réservation`
2. Utilisez l'authentification (token ou Basic Auth)
3. Effectuez une requête DELETE
4. Vérifiez que la suppression a réussi (statut 201)
5. Tentez de récupérer la réservation pour confirmer qu'elle n'existe plus

## 🔧 Structure suggérée du fichier

```robot
*** Settings ***
Library     RequestsLibrary
# TODO: Autres imports si nécessaires

*** Variables ***
${BASE_URL}    # TODO: URL de l'API
${BOOKING_ID}  # Sera défini dynamiquement

*** Test Cases ***
Test Complet API Booker
    [Documentation]    Test complet du cycle de vie d'une réservation
    Créer Une Session HTTP
    Créer Une Nouvelle Réservation
    Récupérer La Réservation
    Modifier La Réservation
    Supprimer La Réservation

*** Keywords ***
Créer Une Session HTTP
    [Documentation]    Initialise la session HTTP
    # TODO: Implémenter

Créer Une Nouvelle Réservation
    [Documentation]    Crée une nouvelle réservation via POST
    # TODO: Implémenter

# TODO: Autres keywords
```

## 🎁 Bonus (optionnel)

Si vous terminez rapidement, essayez ces défis supplémentaires :

### Défi 1 : Tests négatifs
- Testez la création d'une réservation avec des données invalides
- Testez l'accès à une réservation qui n'existe pas
- Testez la modification sans authentification

### Défi 2 : Réutilisabilité
- Créez des keywords réutilisables
- Externalisez les données de test dans des variables ou fichiers
- Implémentez une suite de tests avec setup/teardown

### Défi 3 : Validation avancée
- Validez le format des dates
- Vérifiez les types de données retournées
- Implémentez des assertions personnalisées

## 💡 Conseils pour réussir

!!! tip "Bonnes pratiques"
- Testez chaque étape individuellement avant de les combiner
- Utilisez `Log` et `Log To Console` pour déboguer
- Consultez la documentation de RequestsLibrary : [https://marketsquare.github.io/robotframework-requests/doc/RequestsLibrary.html](https://marketsquare.github.io/robotframework-requests/doc/RequestsLibrary.html)
- Vérifiez les réponses HTTP avec les status codes appropriés

!!! warning "Points d'attention"
- L'API Booker est parfois lente, ajoutez des timeouts si nécessaire
- Les IDs de réservation sont temporaires et peuvent être supprimés
- Gérez les erreurs de réseau potentielles

## 📖 Ressources utiles

- [Documentation RequestsLibrary](https://marketsquare.github.io/robotframework-requests/doc/RequestsLibrary.html)
- [Documentation API Booker](https://restful-booker.herokuapp.com/apidoc/index.html)
- [Guide Robot Framework JSON](https://robotframework.org/robotframework/latest/libraries/Collections.html)

## 🏆 Validation

Votre exercice est réussi si :

- ✅ Tous vos tests passent (statut PASS)
- ✅ Vous créez, lisez, modifiez et supprimez une réservation
- ✅ L'authentification fonctionne correctement
- ✅ Les assertions validant les données sont présentes
- ✅ Votre code est lisible et bien organisé

Bon courage ! N'hésitez pas à expérimenter et à consulter la documentation en cas de besoin.