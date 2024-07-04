
[![Poetry](https://img.shields.io/endpoint?url=https://python-poetry.org/badge/v0.json)](https://python-poetry.org/)
[![security: bandit](https://img.shields.io/badge/security-bandit-yellow.svg)](https://github.com/PyCQA/bandit)

[![Release](https://img.shields.io/github/release/olmatz/python-project-template.svg)](https://GitHub.com/olmatz/python-project-template/releases/)
[![Téléchargements](https://img.shields.io/github/downloads/olmatz/python-project-template/total.svg)](https://GitHub.com/olmatz/python-project-template/releases/)
[![Forks](https://img.shields.io/github/forks/olmatz/python-project-template.svg?style=social&label=Fork&maxAge=2592000)](https://GitHub.com/olmatz/python-project-template/network/)
[![Stars](https://img.shields.io/github/stars/olmatz/python-project-template.svg?style=social&label=Star&maxAge=2592000)](https://GitHub.com/olmatz/python-project-template/stargazers/)

[![Contributeurs](https://img.shields.io/github/contributors/olmatz/python-project-template.svg)](https://GitHub.com/olmatz/python-project-template/graphs/contributors/)
[![Issues](https://img.shields.io/github/issues/olmatz/python-project-template.svg)](https://GitHub.com/olmatz/python-project-template/issues/)
[![PourcentageIssues](http://isitmaintained.com/badge/open/olmatz/python-project-template.svg)](http://isitmaintained.com/project/olmatz/python-project-template)
[![PullRequests](https://img.shields.io/github/issues-pr/olmatz/python-project-template.svg)](https://GitHub.com/olmatz/python-project-template/pull/)

# Nom du projet

## Description

## Installation

## Utilisation

## Contribution

### Comment contribuer
Installation spécifique pour le développement (inclus dans le pyproject.toml) : test avec [`pytest`](https://docs.pytest.org/en/stable/contents.html) et [`coverage`](https://coverage.readthedocs.io/en/latest/), documentation avec [`sphinx`](https://www.sphinx-doc.org/en/master/), sécurité avec [`bandit`](https://bandit.readthedocs.io/en/latest/)


#### Initialisation de l'environnement avec poetry
Prérequis : installation de `poetry`, voir la documentation officielle [ici](https://python-poetry.org/docs/#installation) si besoin.

:warning: **L'installation de poetry doit être réalisée dans un environnement virtuel isolé**

Pour installer les dépendances du projet (équivalent de pip requirements-dev.txt avec pip) :
```
poetry install
```

Pour ajouter un package dans poetry :
```
poetry add nom-du-package
```

Pour éxécuter le code :
```
poetry run python app.py
```

Les tests :
```
poetry run coverage run -m pytest
poetry run coverage html
```

La documentation :
```
poetry run make html
```

#### Installation des scripts pre-commit
Pour que `pre-commit` se lance automatiquement à chaque commit, il faut au préalable installer les scripts git-hook
```
poetry run pre-commit install
```

Avant chaque commit :
* Vérifier que vos modifications n'ont pas ajouté de regression dans le code, en éxécutant à minima les tests et en ajoutant de nouveaux tests si nécessaire.
* Documenter systématiquement les fonctions et classes avec les docstrings afin de générer automatiquement la documentation avec sphinx. Générer la documentation pour vérifier qu'il n'y a pas d'erreur.
* Vérifier que vous n'introduisez pas de faille de sécurité à l'aide d'un scan `bandit`. Ne jamais commit du code avec des identifiants (login/password), des clés API, des lien vers des bases de données privatives, des chemins personels, ...

Recommandation en terme de commit : suivre la nomenclature [*Conventional Commits*](https://www.conventionalcommits.org/en/v1.0.0/)

```
<type>[optional scope]: <short description>

[optional body]

[optional footer(s)]
```

### Workflow de développement
Pour chaque fonctionnalité :
1. Création d'une [issue](https://github.com/olmatz/python-project-template/issues)
2. Création d'une branche `nom_fonctionalite` à partir de la branche de développement `dev`
3. Développement dans la branche `nom_fonctionalite`
4. Réaliser les tests pour vérifier le bon fonctionnement de la nouvelle fonctionalité et la non régression du code existant
```
poetry run coverage run -m pytest
poetry run coverage html
```
5. Générer la nouvelle documentation
```
cd docs/build
poetry run make html
```
6. Vérifier que le code n'a pas de faille de sécurité
```
poetry run bandit -r src
```
7. [Merge request](https://github.com/olmatz/python-project-template/pulls) de la branche `nom_fonctionalite` vers la branche `dev`
8. Résolution de l'issue

### Description des fichiers
#### pyproject.toml
Le fichier [`pyproject.toml`](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/) est un fichier de configuration permettant de manager les dépendances et paquets d'un projet python ainsi qu'un ensemble d'outil comme les linters, type checker, ... évitant ainsi d'avoir à gérer et maintenir un fichier de configuration par outil/dépendance.

En particulier, ce fichier permet de configurer l'outil [`poetry`](https://python-poetry.org/docs/) pour la gestion des métadonnées et des dépendances python du projet (similaire à `setup.py` + `requirements.txt` + `requirements-dev.txt`).

Ce fichier configure également une grande partie des outils utilisés comme le linter [`flake8`](https://flake8.pycqa.org/en/latest/), le formateur de code [`black`](https://black.readthedocs.io/en/stable/) notamment la longueur maximale de ligne autorisée et les extensions de ligne spécifique à ignorer, des outils utilitaire comme [`isort`](https://pycqa.github.io/isort/), les outils de tests [`pytest`](https://docs.pytest.org/en/stable/contents.html) et [`coverage`](https://coverage.readthedocs.io/en/latest/), ou encore l'outil [`bandit`](https://bandit.readthedocs.io/en/latest/) permetant d'identifier les problèmes de sécurité dans le code.

#### .env
Ce fichier contient des varibales d'environnement spécifiques au projet (url de bases de données, clés API, ...). Veillez à ne pas partager de donnée sensible dans le repository publique.
Il est utilisé pour charger les varibables d'environnement dans l'application depuis [`python-dotenv`](https://github.com/theskumar/python-dotenv).

#### .gitignore
Ce fichier spécifie les fichiers et répertoire à ingorer lors de l'ajout de fichiers au système de contrôle de version Git, comme les dépendances, les fichiers système, d'environnement, ...

#### .pre-commit-config.yaml
Ce fichier configure [`pre-commit`](https://pre-commit.com/#intro), un outil qui exécute et automatise des vérifications avant chaque commit, nottament pour corriger et ainsi améliorer la qualité du code.

#### Makefile
Le `Makefile` (Unix) ou `Make.bat` (Windows) permet d'automatiser la génération de la documentation, les tests et le scan de sécurité en une seule exécution.
```
Make.bat
```