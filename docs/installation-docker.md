# Installation avec Docker

Docker offre une méthode simple et portable pour utiliser Robot Framework sans installer Python directement sur votre système. Cette approche garantit un environnement cohérent sur tous les systèmes.

## Prérequis

Assurez-vous d'avoir Docker installé sur votre système :

- **Windows/macOS** : [Docker Desktop](https://www.docker.com/products/docker-desktop)
- **Linux** : [Docker Engine](https://docs.docker.com/engine/install/)

Vérifiez l'installation :
```bash
docker --version
```

## Méthode 1 : Utilisation de l'image officielle

### Image Robot Framework officielle

L'image officielle `robotframework/rfdocker` contient Robot Framework avec de nombreuses bibliothèques utiles pré-installées.

```bash
# Télécharger l'image
docker pull robotframework/rfdocker

# Vérifier l'installation
docker run --rm --entrypoint robot robotframework/rfdocker --version

# Ou simplement
docker run --rm robotframework/rfdocker --version
```

### Exécution d'un test simple

Créer un dossier vide avec le nouveau projet `hello-robot-in-docker`.

Puis dans ce dossier, initialiser l'environnement virtuel :

Créez un fichier `hello_docker.robot` :

```robot
*** Settings ***
Documentation    Test Robot Framework avec Docker

*** Test Cases ***
Hello Docker Test
    [Documentation]    Test simple avec Docker
    Log    Hello from Docker!
    Log To Console    Robot Framework fonctionne dans Docker!
```

Exécutez le test avec Docker :

```bash
docker run --rm -v "$(pwd)":/robot robotframework/rfdocker /robot/hello_docker.robot
```

!!! note "Explication de la commande"
- `--rm` : Supprime le conteneur après exécution
- `-v "$(pwd)":/robot` : Monte le répertoire courant dans le conteneur
- Les fichiers de sortie (par exemple `log.html`) sont placés dans le répertoire courant (ils sont écrasés à chaque lancement)
- `robotframework/rfdocker` : L'image à utiliser
- `/robot/hello_docker.robot` : Chemin absolu du test à lancer
- Inutile de préciser la commande `robot` car c'est l'entrypoint par défaut

<br/>

Une version plus explicite (entrypoint et workdir précisés) :

```bash
docker run --rm --entrypoint robot -w /robot -v "$(pwd)":/robot robotframework/rfdocker hello_docker.robot
```

## Méthode 2 : Créer votre propre image Docker

### Dockerfile personnalisé

Créer un dossier vide avec le nouveau projet `hello-robot-in-my-docker`.

Puis dans ce dossier, initialiser l'environnement virtuel :

Créez un `Dockerfile` pour votre projet :

```dockerfile
# Utilisez l'image Python officielle
FROM python:3.13-slim

# Définir le répertoire de travail
WORKDIR /robot

# Copier le fichier des dépendances
COPY requirements.txt .

# Installer Robot Framework et les dépendances
RUN pip install --no-cache-dir -r requirements.txt

# Copier les fichiers de test
COPY . .

# Définir la commande par défaut
CMD ["robot", "--outputdir", "results", "tests/"]
```

### Fichier requirements.txt

```txt
robotframework==7.3.2
```

### Fichier de test

Créez le répertoire `tests`.

Créez un fichier `tests/hello_docker.robot` :

```robot
*** Settings ***
Documentation    Test Robot Framework avec mon image Docker

*** Test Cases ***
Hello Docker Test
    [Documentation]    Test simple avec Docker
    Log    Hello from Docker!
    Log To Console    Robot Framework fonctionne dans mon image Docker!
```

### Construction et exécution

```bash
# Construire l'image
docker build -t mon-robot-framework .

# Exécuter les tests
docker run --rm -v "$(pwd)":/robot mon-robot-framework
```

Les fichiers de sortie sont présents dans le dossier `results` car l'option `--outputdir` a été spécifiée.

## Avantages de Docker pour Robot Framework

!!! success "Avantages"
- **Portabilité** : Même environnement sur tous les systèmes
- **Isolation** : Pas de conflit avec les dépendances système
- **Reproductibilité** : Tests identiques en développement et production
- **Facilité de déploiement** : Intégration simple dans CI/CD
- **Versions multiples** : Testez avec différentes versions facilement

!!! tip "Bonnes pratiques"
- Utilisez des tags de version spécifiques pour la production
- Montez seulement les répertoires nécessaires
- Utilisez `.dockerignore` pour exclure les fichiers inutiles
- Définissez des volumes pour persister les résultats

## Dépannage

### Problèmes courants

**Erreur de permission sur Linux/macOS** :
```bash
# Ajoutez l'utilisateur actuel au groupe docker
sudo usermod -aG docker $USER
# Redémarrez votre session
```

**Problème de montage de volume sur Windows** :
```bash
# Utilisez le chemin Windows complet
docker run --rm -v "C:/path/to/tests:/robot" robotframework/rfdocker robot tests/
```

**Tests qui ne trouvent pas les fichiers** :
```bash
# Vérifiez le répertoire de travail dans le conteneur
docker run --rm -v "$(pwd)":/robot -w /robot robotframework/rfdocker robot tests/
```

## Prochaines étapes

Maintenant que vous savez utiliser Robot Framework avec Docker, vous pouvez créer des environnements de test reproductibles et les intégrer facilement dans vos pipelines CI/CD. Dans la [prochaine section](hello-world.md), nous verrons comment créer votre premier test.