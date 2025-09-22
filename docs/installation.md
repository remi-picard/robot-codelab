# Installation de l'environnement

Cette première étape vous guide dans l'installation et la configuration de Robot Framework sur votre système.

## Étape 1 : Création de l'environnement virtuel Python

Il est fortement recommandé d'utiliser un environnement virtuel Python pour isoler les dépendances de votre projet.

Créer un dossier vide avec le nouveau projet `hello-robot`.

Puis dans ce dossier, initialiser l'environnement virtuel :

```bash
python3 -m venv venv
source venv/bin/activate
```

<br/>

!!! note "Note pour Windows"
Sur Windows, utilisez la commande suivante pour activer l'environnement virtuel :
```cmd
venv\Scripts\activate
```

<br/>

!!! tip "Conseils"
Vous devriez voir `(venv)` apparaître au début de votre ligne de commande, indiquant que l'environnement virtuel est actif.

Vous pouvez sortir à tout moment de l'environnement virtuel avec la commande `deactivate`.

## Étape 2 : Installation de Robot Framework

Une fois votre environnement virtuel activé, installez Robot Framework avec pip :

```bash
pip install robotframework==7.3.2
```

Cette commande installera la dernière version stable de Robot Framework ainsi que ses dépendances.

## Étape 3 : Test de la ligne de commande

Vérifiez que l'installation s'est déroulée correctement en testant la commande `robot` :

```bash
robot --help
```

Si l'installation est réussie, vous devriez voir l'aide de Robot Framework s'afficher avec toutes les options disponibles.

## Vérification de l'installation

Vous pouvez également vérifier la version installée avec :

```bash
robot --version
```

## Prochaines étapes

Félicitations ! Votre environnement Robot Framework est maintenant prêt.

**Alternatives d'installation :**

- Si vous préférez utiliser Docker, consultez la page [Installation avec Docker](installation-docker.md)
- Sinon, continuez avec la [création de votre premier test](hello-world.md)

!!! success "Installation terminée"
Votre environnement Robot Framework est maintenant configuré et prêt à l'emploi !