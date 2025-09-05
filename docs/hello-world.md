# Hello World Robot Framework

Maintenant que votre environnement est configuré, créons votre premier test Robot Framework ! Ce test simple affichera "Hello World" dans la console.

## Étape 1 : Création du fichier de test

Créez un nouveau fichier nommé `hello_world.robot` dans votre répertoire de travail :

```robot
*** Settings ***
Documentation    Mon premier test Robot Framework

*** Test Cases ***
Hello World Test
    [Documentation]    Test simple qui affiche Hello World
    Log    Hello World
    Log To Console    Hello World
```

## Étape 2 : Exécution du test

Ouvrez votre terminal dans le répertoire contenant le fichier `hello_world.robot` et exécutez la commande suivante :

```bash
# Activer l'env virtuel si besoin
# source venv/bin/activate

robot hello_world.robot
```

## Résultat attendu

Après l'exécution, vous devriez voir :

1. **Dans la console** : Le message "Hello World" affiché directement
2. **Dans le rapport** : Un fichier `report.html` sera généré avec les détails du test
3. **Dans les logs** : Un fichier `log.html` contiendra les logs détaillés

Exemple de sortie console :
```
==============================================================================
Hello World :: Mon premier test Robot Framework
==============================================================================
Hello World Test :: Test simple qui affiche Hello World               .Hello World
Hello World Test :: Test simple qui affiche Hello World               | PASS |
------------------------------------------------------------------------------
Hello World :: Mon premier test Robot Framework                       | PASS |
1 test, 1 passed, 0 failed
==============================================================================
Output:  /chemin/vers/votre/projet/output.xml
Log:     /chemin/vers/votre/projet/log.html
Report:  /chemin/vers/votre/projet/report.html
```

## Explication du code

Décortiquons le contenu de notre premier test :

### Section Settings
```robot
*** Settings ***
Documentation    Mon premier test Robot Framework
```
- Définit la documentation globale du fichier de test

### Section Test Cases
```robot
*** Test Cases ***
Hello World Test
    [Documentation]    Test simple qui affiche Hello World
    Log    Hello World
    Log To Console    Hello World
```

- **`Hello World Test`** : Nom de notre cas de test
- **`[Documentation]`** : Documentation spécifique à ce test
- **`Log`** : Mot-clé qui écrit dans les logs HTML
- **`Log To Console`** : Mot-clé qui affiche directement dans la console

## Bonnes pratiques observées

!!! tip "Conventions de nommage"
- Les fichiers Robot Framework utilisent l'extension `.robot`
- Les noms de test sont descriptifs et en anglais de préférence
- L'indentation utilise au moins 2 espaces OU 1 tabulation

!!! info "Types de logs"
- **`Log`** : Visible uniquement dans le fichier log.html
- **`Log To Console`** : Visible dans la console ET dans log.html

## Exercice pratique

Modifiez votre test pour afficher votre nom au lieu de "Hello World" :

```robot
*** Test Cases ***
Saluer Mon Nom
    [Documentation]    Test qui affiche mon nom
    Log    Bonjour [Votre Nom] !
    Log To Console    Bonjour [Votre Nom] !
```

## Prochaines étapes

Félicitations ! Vous avez créé et exécuté votre premier test Robot Framework. Dans la [prochaine section](configuration-ide.md), nous configurerons votre IDE pour améliorer votre productivité, puis nous explorerons les mots-clés de base et comment structurer des tests plus complexes.

!!! success "Premier test réussi"
Vous maîtrisez maintenant les bases de l'exécution d'un test Robot Framework !