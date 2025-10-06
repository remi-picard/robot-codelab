# Test de l'API Booker

Dans cet exercice pratique, vous allez apprendre à tester une API REST avec Robot Framework en utilisant l'API Booker, une API de démonstration pour la gestion de réservations d'hôtel.

## 🎯 Objectifs

À la fin de cet exercice, vous saurez :

- Installer et utiliser la RequestsLibrary
- Effectuer des requêtes HTTP (GET, POST, PUT, DELETE)
- Gérer l'authentification API
- Valider les réponses JSON
- Organiser vos tests API

## 🕰️ Durée

1h à 1h30

## 📚 Documentation de l'API

L'API Booker est disponible à l'adresse : [https://restful-booker.herokuapp.com/](https://restful-booker.herokuapp.com/){target="_blank"}

Documentation complète : [https://restful-booker.herokuapp.com/apidoc/index.html](https://restful-booker.herokuapp.com/apidoc/index.html){target="_blank"}

### Endpoints principaux
- **GET /booking** - Liste toutes les réservations
- **POST /booking** - Crée une nouvelle réservation
- **GET /booking/{id}** - Récupère une réservation spécifique
- **PUT /booking/{id}** - Met à jour une réservation (authentification requise)
- **DELETE /booking/{id}** - Supprime une réservation (authentification requise)
- **POST /auth** - Génère un token d'authentification

## 📋 Exercices à réaliser

### Étape 1 : Installation de RequestsLibrary

Votre première mission est d'installer la librairie nécessaire pour effectuer des requêtes HTTP.

!!! question "À faire"
Installez la librairie RequestsLibrary dans votre environnement virtuel.

??? tip "Afficher les indices"
    Utilisez pip pour installer `robotframework-requests`

### Étape 2 : Configuration de base

Créez un fichier `booker.robot` avec la structure de base.

!!! question "À faire"
1. Importez la RequestsLibrary dans la section `*** Settings ***`
2. Définissez l'URL de base de l'API comme variable

**Structure suggérée :**

```robot
*** Settings ***
# TODO: Importer la librairie nécessaire

*** Variables ***
# TODO: Définir l'URL de base de l'API

*** Test Cases ***
# Vos tests iront ici

*** Keywords ***
# Vos Keywords personnalisés iront ici
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

!!! warning "Erreur 500"
    - L'API Booker renvoie une erreur 500 Internal Server Error (au lieu de renvoyer une erreur 400), si un des champs est mal orthographié
    - vérifiez bien tous les champs `firstname`, `lastname` ... (attention à la casse)

??? tip "Afficher les indices"
    - Utilisez le mot-clé `POST` pour effectuer la requête
    - Le paramètre `json` permet d'envoyer des données JSON
    - Le paramètre `verify=${False}` permet de bypasser la vérification du certificat SSL
    - Utilisez `Set Variable` pour stocker l'ID de réservation

### Étape 4 : Récupérer la réservation

Compléter le test précédent pour récupérer la réservation que vous venez de créer.

!!! question "À faire"
1. Renommez le test `Créer Une Nouvelle Réservation` en `Créer Et Récupérer Une Réservation`
2. Utilisez l'ID de réservation stocké précédemment
3. Effectuez une requête GET vers `/booking/{id}`
4. Vérifiez le statut de la réponse
5. Validez que les données retournées correspondent à celles créées

??? tip "Afficher les indices"
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

??? tip "Afficher les indices"
    - La réponse contient un champ `token`
    - Stockez le token comme variable de test ou de suite
    - Vous utiliserez ce token dans les headers des requêtes suivantes

### Étape 6 : Modifier la réservation

Implémentez un test pour modifier une réservation existante.

!!! question "À faire"
1. Renommez le test case `Créer Et Récupérer Une Réservation` en `Créer Récupérer Et Modifier Une Réservation`
2. Obtenez d'abord un token d'authentification
3. Définissez de nouvelles données de réservation
4. Effectuez une requête PUT avec le token dans les headers
5. Vérifiez que la modification a réussi

??? tip "Afficher les indices"
    - Utilisez le header `Cookie: token=VOTRE_TOKEN` pour l'authentification
    - Vous pouvez aussi utiliser `Authorization: Basic YWRtaW46cGFzc3dvcmQxMjM=`
    - Modifiez quelques champs comme le prix ou les dates

### Étape 7 : Supprimer la réservation

Créez un test pour supprimer la réservation.

!!! question "À faire"
1. Renommez le test case `Créer Récupérer Et Modifier Une Réservation` en `Créer Récupérer Modifier Et Supprimer Une Réservation`
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
    Créer Une Nouvelle Réservation
    Récupérer La Réservation
    Modifier La Réservation
    Supprimer La Réservation

*** Keywords ***
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
- Consultez la documentation de RequestsLibrary, notamment le Keyword `GET` où sont documentés les arguments `**kwargs`
- Vérifiez les réponses HTTP avec les status codes appropriés

!!! warning "Points d'attention"
- L'API Booker est parfois lente, ajoutez des timeouts si nécessaire
- Les IDs de réservation sont temporaires et peuvent être supprimés

## 📖 Ressources utiles

- [RequestsLibrary](https://marketsquare.github.io/robotframework-requests/doc/RequestsLibrary.html#GET){target="_blank"}
- [BuiltIn](https://robotframework.org/robotframework/latest/libraries/BuiltIn.html){target="_blank"}
- [Collections](https://robotframework.org/robotframework/latest/libraries/Collections.html){target="_blank"}

## 🏆 Validation

Votre exercice est réussi si :

- ✅ Tous vos tests passent (statut PASS)
- ✅ Vous créez, lisez, modifiez et supprimez une réservation
- ✅ L'authentification fonctionne correctement
- ✅ Les assertions validant les données sont présentes
- ✅ Votre code est lisible et bien organisé

Bon courage ! N'hésitez pas à expérimenter et à consulter la documentation en cas de besoin.

## Prochaines étapes

Une fois que vous maîtrisez les tests d'API, découvrez les tests d'interface utilisateur dans l'[exercice TODO MVC](todo-mvc.md) !