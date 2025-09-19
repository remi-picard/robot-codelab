# Test de l'interface TODO MVC

Dans cet exercice pratique, vous allez apprendre à automatiser les tests d'interface utilisateur avec Robot Framework en utilisant la Browser Library moderne et l'application TODO MVC React.

## 🎯 Objectifs

À la fin de cet exercice, vous saurez :

- Installer et configurer Browser Library avec Playwright
- Automatiser des interactions avec une interface web
- Localiser des éléments avec différents sélecteurs
- Gérer l'état des éléments (visible, enabled, etc.)
- Prendre des captures d'écran pour le débogage
- Organiser vos tests UI de manière efficace

## 🕰️ Durée

2h à 3h

## 🌐 Application à tester

Nous utiliserons l'application TODO MVC React disponible à l'adresse :
[https://todomvc.com/examples/react/dist](https://todomvc.com/examples/react/dist){target="_blank"}

Cette application permet de :

- ✅ Créer des tâches
- ✅ Marquer des tâches comme terminées
- ✅ Filtrer les tâches (All, Active, Completed)
- ✅ Supprimer des tâches individuelles
- ✅ Supprimer toutes les tâches terminées

## 📋 Exercices à réaliser

### Étape 1 : Installation de Browser Library et Playwright

Votre première mission est d'installer les outils nécessaires pour l'automatisation web moderne.

!!! question "À faire"
1. Installez Browser Library dans votre environnement virtuel
2. Installez les navigateurs Playwright

??? tip "Afficher les indices"
    - Utilisez `pip install robotframework-browser`
    - Exécutez `rfbrowser init` après l'installation

!!! warning "Note importante"
L'installation de Playwright peut prendre plusieurs minutes car elle télécharge les navigateurs.

### Étape 2 : Configuration de base et premier test

Créez un fichier `todo_mvc.robot` avec la structure de base.

!!! question "À faire"
1. Importez la Browser Library dans la section `*** Settings ***`
2. Définissez l'URL de l'application comme variable
3. Créez un test simple pour ouvrir l'application et vérifier qu'elle se charge
4. Vérifiez que le titre de la page contient "TodoMVC"

**Structure suggérée :**
```robot
*** Settings ***
# TODO: Importer Browser Library

*** Variables ***
# TODO: Définir l'URL de l'application TODO MVC

*** Test Cases ***
# Vos tests iront ici

*** Keywords ***
# Vos mots-clés personnalisés iront ici
```

??? tip "Afficher les indices"
    - Utilisez `New Page` pour initialiser le navigateur

### Étape 3 : Créer une tâche

Implémentez un test pour ajouter une nouvelle tâche à la liste.

!!! question "À faire"
1. Créez un test case `Créer Une Nouvelle Tâche`
2. Localisez le champ de saisie des tâches
3. Saisissez le texte d'une nouvelle tâche
4. Appuyez sur Entrée pour valider
5. Vérifiez que la tâche apparaît dans la liste

??? tip "Afficher les indices"
    - Le champ de saisie a un placeholder "What needs to be done?"
    - Utilisez `Fill Text` pour saisir le texte
    - Utilisez `Keyboard Key` avec "Enter" pour valider
    - Vérifiez la présence de la tâche avec `Get Text` ou `Get Element`

### Étape 4 : Lister les tâches

Créez un test pour vérifier que vous pouvez récupérer la liste des tâches existantes.

!!! question "À faire"
1. Créez plusieurs tâches de test
2. Récupérez la liste de toutes les tâches affichées
3. Vérifiez le nombre de tâches créées
4. Validez le contenu des tâches

??? tip "Afficher les indices"
    - Les tâches sont dans des éléments `<li>` avec la classe `todo`
    - Utilisez `Get Elements` pour récupérer plusieurs éléments
    - Comptez les éléments avec `Get Length`
    - Parcourez la liste pour vérifier le contenu

### Étape 5 : Filtrer les tâches

Implémentez un test pour utiliser les filtres de l'application (All, Active, Completed).

!!! question "À faire"
1. Créez plusieurs tâches de test
2. Marquez certaines tâches comme terminées
3. Testez le filtre "Active" (tâches non terminées)
4. Testez le filtre "Completed" (tâches terminées)
5. Testez le filtre "All" (toutes les tâches)
6. Vérifiez que le bon nombre de tâches est affiché pour chaque filtre

??? tip "Afficher les indices"
    - Les filtres sont des liens en bas de l'application
    - Une tâche est marquée comme terminée en cliquant sur le cercle à gauche
    - Les tâches terminées ont la classe CSS `completed`
    - Utilisez `Click` pour interagir avec les filtres

### Étape 6 : Terminer une tâche

Créez un test pour marquer une tâche comme terminée et vérifier le changement d'état.

!!! question "À faire"
1. Créez une tâche de test
2. Cliquez sur le bouton de completion (cercle) de la tâche
3. Vérifiez que la tâche a la classe `completed`
4. Vérifiez que le texte de la tâche est barré
5. Testez également le "dé-marquage" d'une tâche terminée

??? tip "Afficher les indices"
    - Le bouton de completion est un `input[type="checkbox"]`
    - Une tâche terminée a un style `text-decoration: line-through`
    - Utilisez des assertions sur les classes CSS ou les styles

### Étape 7 : Supprimer une tâche

Implémentez un test pour supprimer une tâche individuelle.

!!! question "À faire"
1. Créez une tâche de test
2. Survolez la tâche pour révéler le bouton de suppression
3. Cliquez sur le bouton de suppression
4. Vérifiez que la tâche a disparu de la liste
5. Vérifiez que le compteur de tâches a été mis à jour

??? tip "Afficher les indices"
    - Le bouton de suppression n'apparaît qu'au survol (`hover`)
    - Utilisez `Hover` pour déclencher l'affichage du bouton
    - Le bouton a généralement une classe comme `destroy`
    - Vérifiez l'absence avec des assertions négatives

### Étape 8 : Supprimer toutes les tâches terminées

Créez un test pour utiliser la fonction "Clear completed".

!!! question "À faire"
1. Créez plusieurs tâches de test
2. Marquez certaines tâches comme terminées
3. Cliquez sur le bouton "Clear completed"
4. Vérifiez que seules les tâches terminées ont été supprimées
5. Vérifiez que les tâches actives restent présentes

??? tip "Afficher les indices"
    - Le bouton "Clear completed" n'apparaît que s'il y a des tâches terminées
    - Comptez les tâches avant et après l'opération
    - Vérifiez que les tâches restantes sont toutes actives

## 🔧 Structure suggérée du fichier

```robot
*** Settings ***
Library     Browser
# TODO: Autres imports si nécessaires

*** Variables ***
${TODO_URL}    https://todomvc.com/examples/react/dist
${TIMEOUT}     10s

*** Test Cases ***
Test Complet TODO MVC
    [Documentation]    Test complet de l'application TODO MVC
    Setup Navigateur
    Créer Une Nouvelle Tâche
    Lister Les Tâches
    Filtrer Les Tâches
    Terminer Une Tâche
    Supprimer Une Tâche
    Supprimer Toutes Les Tâches Terminées
    [Teardown]    Fermer Navigateur

*** Keywords ***
Setup Navigateur
    [Documentation]    Initialise le navigateur et ouvre l'application
    # TODO: Implémenter

Créer Une Nouvelle Tâche
    [Documentation]    Ajoute une nouvelle tâche à la liste
    # TODO: Implémenter

Fermer Navigateur
    [Documentation]    Ferme proprement le navigateur
    # TODO: Implémenter

# TODO: Autres keywords
```

## 🎁 Bonus (optionnel)

Si vous terminez rapidement, essayez ces défis supplémentaires :

### Défi 1 : Tests de validation
- Testez la création de tâches vides (doit être rejetée)
- Testez la création de tâches avec des caractères spéciaux
- Testez le comportement avec de très longues tâches

### Défi 2 : Edition inline
- Implémentez l'édition d'une tâche existante (double-clic)
- Testez l'annulation d'édition avec Escape
- Testez la sauvegarde d'édition avec Entrée

### Défi 3 : Interactions avancées
- Implémentez le "toggle all" (marquer/démarquer toutes les tâches)
- Testez les raccourcis clavier
- Ajoutez des assertions sur le compteur de tâches

### Défi 4 : Multi-navigateurs
- Exécutez vos tests sur Chrome, Firefox et Safari
- Comparez les comportements entre navigateurs
- Gérez les spécificités de chaque navigateur

## 💡 Conseils pour réussir

!!! tip "Bonnes pratiques UI"

- Utilisez des attentes explicites (`Wait For Elements State`)
- Prenez des captures d'écran aux étapes importantes
- Utilisez des sélecteurs robustes (ID > classe > XPath)
- Gérez les temps d'attente appropriés

!!! tip "Debug et développement"
```robot
# Capture d'écran pour debug
Take Screenshot    debug_step_${TEST_NAME}.png

# Pause pour inspection manuelle
Pause Execution    Inspectez l'état current
    
# Log des éléments trouvés
${elements}=    Get Elements    css=.todo
Log    Nombre d'éléments trouvés: ${elements.length}
```

!!! warning "Points d'attention"

- L'application TODO MVC peut être réinitialisée à chaque rechargement
- Certains éléments ne sont visibles qu'en cas d'interaction (hover, focus)
- Les sélecteurs CSS peuvent varier selon l'implémentation
- Gérez les états transitoires (animations, chargements)

## 📖 Ressources utiles

- [Browser Library](https://marketsquare.github.io/robotframework-browser/Browser.html){target="_blank"}
- [Playwright](https://playwright.dev/docs/intro){target="_blank"}
- [Guide des sélecteurs CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors){target="_blank"}
- [Exemples / Comparaison](https://robotframework-browser.org/#examples){target="_blank"}

## 🛠️ Sélecteurs utiles

Voici quelques indices sur les sélecteurs que vous pourriez utiliser :

```robot
# Exemples de sélecteurs (à adapter selon l'implémentation)
${INPUT_FIELD}           css=.new-todo
${TODO_LIST}             css=.todo-list
${TODO_ITEMS}            css=.todo-list li
${TOGGLE_ALL}            css=.toggle-all
${FILTERS}               css=.filters a
${CLEAR_COMPLETED}       css=.clear-completed
${TODO_COUNT}            css=.todo-count
```

## 🏆 Validation

Votre exercice est réussi si :

- ✅ Tous vos tests passent dans au moins un navigateur
- ✅ Vous pouvez créer, lister, filtrer, terminer et supprimer des tâches
- ✅ Vos sélecteurs sont robustes et ne cassent pas facilement
- ✅ Vous gérez correctement les attentes et les états des éléments
- ✅ Votre code est organisé avec des keywords réutilisables
- ✅ Vous prenez des captures d'écran aux moments appropriés

## 🔍 Stratégies de débogage

```robot
*** Keywords ***
Debug État Application
    [Documentation]    Helper pour déboguer l'état de l'application
    Take Screenshot    debug_etat_actuel.png
    ${todos}=    Get Elements    css=.todo-list li
    Log    Nombre de tâches: ${todos.length}
    FOR    ${todo}    IN    @{todos}
        ${text}=    Get Text    ${todo}
        ${classe}=    Get Attribute    ${todo}    class
        Log    Tâche: "${text}" - Classes: ${classe}
    END
```

Bon courage ! N'hésitez pas à expérimenter avec différents navigateurs et à personnaliser vos tests selon vos besoins.

## Prochaines étapes

Après avoir maîtrisé l'automation d'interface utilisateur, relevez un défi plus ludique avec le [Jeu Robot Flower Princess](robot-flower-princess.md) qui combine APIs, algorithmes et stratégie !