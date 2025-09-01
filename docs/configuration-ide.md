# Configuration des IDEs

Pour améliorer votre productivité lors du développement de tests Robot Framework, il est essentiel de configurer correctement votre environnement de développement. Cette section vous guide dans la configuration de PyCharm et VSCode.

## Configuration de PyCharm

PyCharm offre un excellent support pour Robot Framework avec des plugins dédiés.

Suivez les étapes présentées par [Set up your IDE](https://docs.robotframework.org/docs/getting_started/ide#pycharm).

### Fonctionnalités disponibles dans PyCharm

- ✅ **Coloration syntaxique** complète
- ✅ **Auto-complétion** des mots-clés
- ✅ **Navigation** vers les définitions
- ✅ **Refactoring** des mots-clés
- ✅ **Exécution directe** des tests
- ✅ **Débogage** des tests

### Configuration de l'exécution

1. Clic droit sur votre fichier `.robot`
2. **Run 'nom_fichier.robot'**
3. Ou configurez une **Run Configuration** personnalisée :
   - **Run** → **Edit Configurations**
   - **+** → **Robot Framework**
   - Configurez le chemin vers votre script et les arguments

---

## Configuration de VSCode

VSCode avec les bonnes extensions offre une excellente expérience de développement pour Robot Framework.

Suivez les étapes présentées par [Set up your IDE](https://docs.robotframework.org/docs/getting_started/ide#visual-studio-code).

### Fonctionnalités disponibles dans VSCode

- ✅ **Coloration syntaxique** avancée
- ✅ **Auto-complétion** intelligente
- ✅ **Validation** en temps réel
- ✅ **Navigation** vers les définitions
- ✅ **Outline** de la structure du fichier
- ✅ **Exécution** directe des tests
- ✅ **Intégration terminal**

### Snippets utiles pour VSCode

Créez le fichier `.vscode/robotframework.code-snippets` :

```json
{
    "Robot Test Case": {
        "prefix": "test",
        "body": [
            "${1:Test Case Name}",
            "    [Documentation]    ${2:Test description}",
            "    ${3:# Test steps here}",
            "    Log    ${4:Test completed}"
        ],
        "description": "Create a new Robot Framework test case"
    },
    "Robot Keyword": {
        "prefix": "keyword",
        "body": [
            "${1:Keyword Name}",
            "    [Documentation]    ${2:Keyword description}",
            "    [Arguments]    ${3:\\${arg1}}",
            "    ${4:# Keyword implementation}",
            "    Log    ${5:Keyword executed}"
        ],
        "description": "Create a new Robot Framework keyword"
    }
}
```

---

## Configuration commune recommandée

### Structure de projet recommandée

```
mon-projet-robot/
├── tests/
│   ├── test_suite_1.robot
│   └── test_suite_2.robot
├── resources/
│   ├── keywords.resource
│   └── variables.resource
├── libraries/
│   └── custom_library.py
├── results/
│   └── (rapports générés)
├── requirements.txt
└── robot.yaml (optionnel)
```

### Fichier robot.yaml (optionnel)

Créez un fichier `robot.yaml` à la racine de votre projet :

```yaml
tasks:
  Run all tests:
    shell: robot --outputdir results tests/
  
  Run single test:
    shell: robot --outputdir results tests/${test_file}

condaConfigFile: conda.yaml
artifactsDir: results
PATH:
  - .
PYTHONPATH:
  - .
  - libraries
```

## Conseils pour optimiser votre workflow

!!! tip "Raccourcis utiles"
**PyCharm:**

- `Ctrl+Shift+F10` : Exécuter le test sous le curseur
- `Ctrl+B` : Aller à la définition
- `Alt+Enter` : Actions rapides

**VSCode:**

- `Ctrl+Shift+P` : Palette de commandes
- `F12` : Aller à la définition
- `Ctrl+` : Terminal intégré

!!! info "Formatage automatique"
Activez le formatage automatique dans votre IDE pour maintenir une syntaxe cohérente dans vos fichiers Robot Framework.

!!! warning "Attention aux chemins"
Assurez-vous que les chemins vers votre environnement virtuel Python sont corrects dans la configuration de votre IDE.

## Test de configuration

Créez un fichier de test simple pour vérifier que votre configuration fonctionne :

```robot
*** Settings ***
Documentation    Test de configuration IDE

*** Test Cases ***
Test Configuration IDE
    [Documentation]    Vérifie que l'IDE est correctement configuré
    Log    Configuration IDE réussie
    Should Be True    True
```

Si l'auto-complétion, la coloration syntaxique et l'exécution fonctionnent correctement, votre IDE est prêt !

## Prochaines étapes

Maintenant que votre environnement de développement est configuré, vous êtes prêt à créer des tests plus complexes et à utiliser toutes les fonctionnalités avancées de Robot Framework.

Dans la [prochaine section](api-booker.md), nous allons mettre en pratique vos connaissances avec un exercice complet de test d'API REST.