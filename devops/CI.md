# Integration continue

> ❌ A travailler

> ✔️ Auto validation par l'étudiant

## 🎓 J'ai compris et je peux expliquer

- les enjeux de l'integration continue ✔️

La CI est une méthode de développement de logiciel DevOps avec laquelle les développeurs intègrent régulièrement leurs modifications de code à un référentiel centralisé (par exemple un repository GitHub), ensuite des opérations de création (build du projet) et de test sont automatiquement lancées.

La CI regroupe un ensemble d’actions automatisées permettant de tester l'application et d'assurer son bon fonctionnement. Pour faire de la CI on lance des actions nommées GitHub Actions à chaque changement de l’application, par exemple sur un push ou une PR (pull request).

- la mise en place d'une github action ✔️

GitHub Actions est une plateforme d’intégration et de livraison continue (CI/CD). Les GitHub Actions permettent d’automatiser l’exécution d’opérations en déterminant des comportements a adopter sur certains événements Git. Par exemple, à chaque push sur main (branche principale équivalente à la production), ou à chaque pull request, il est possible de lancer des tests ou opérations en créant des GitHub Actions.

- Les termes employés :
  Un ensemble d'opérations est appelé workflow. Un workflow est un ensemble de jobs nommés que l'on paramètre et exécute sur certains événements Git.

Pour créer un workflow, il est nécessaire de créer un dossier à la racine de son projet nommé.github dans lequel il faut ajouter un second dossier nommé workflows. Dans ce sous-dossier, on ajoute un fichier .yml permettant d'implémenter des GitHubActions. L'indentation du code est très importante sinon, le test ne fonctionnera pas.

Un fichier .yml est composé de différentes parties. Il utilise des clés pour structurer le code. Voici quelques clés :

- **name** : donne le nom du test.

- **on** : précise sur quel type d'événement les jobs vont se lancer (pull_request, push...). Il est possible de combiner plusieurs événements.

- **jobs** : englobe l'ensemble des GitHubActions.

- **nom** du jobs : nom donné à la GitHub Action

- **runs-on** : décrit l’environnement de base sur lequel va tourner le job. Il se lance sur des machines virtuelles du système de GitHub.

- **steps** : décrit les étapes de notre job. Il existe deux types d'étapes, les run et les uses.

  - **uses** : utilisation de script prédéfinis par GitHub Actions. On les retrouve sur des dépôts GitHub ou sur le site de docker.

  - **run** : partie "manuelle", ou l'on ajoute sa propre logique et ses propres commandes (exemple : npm i pour installer les dépendances de l'application)

## 💻 J'utilise

### Un exemple personnel commenté ✔️

```yml
name: jest-and-docker-ci

on: push

jobs:
  test-front:
    runs-on: ubuntu-latest
    steps:
      - name: Check out code
        uses: actions/checkout@v2
      - name: Goto client and run tests
        run: cd client && npm i && npm test
  docker:
    needs: test-front
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    steps:
      - name: Set up QEMU
        uses: docker/setup-qemu-action@v2
      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v2
      - name: Login to Docker Hub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}
      - name: Build and push
        uses: docker/build-push-action@v4
        with:
          push: true
          context: "{{defaultContext}}:client"
          tags: ${{ secrets.DOCKERHUB_USERNAME }}/quete1902:latest
```

Cet extrait de code présente un fichier .yml. Il contient 2 GitHub Actions (jobs) nommés test front et docker.

La première GitHub Action a pour objectif d'automatiser les lancements des test dans la partie client (frontend) à la création d’un commit (push).

La deuxieme GitHub Actions a pour objectif de builder une image docker et de l’envoyer ensuite sur le registre dockerHub. Cette GitHub Action a besoin que la première GitHub Action s'exécute avec succès pour se lancer (clé needs). Elle s'executera après l'evenement push (commit) sur la branche main (clé if).
Dans cette étape, l'image docker est placée dans le registre DockerHub pour permettre à notre serveur de production de récupérer la dernière image de notre application. À chaque envoi de code sur notre branche main, le serveur de production sera mis à jour automatiquement avec la dernière version de notre application. Nous préparons la CD avec le déploiement automatique, également appelé déploiement continu.

### Utilisation dans un projet ✔️

[lien github](...)

Description :

### Utilisation en production si applicable❌ / ✔️

[lien du projet](...)

Description :

### Utilisation en environement professionnel ❌

Description :

## 🌐 J'utilise des ressources

- lien documentation GitHub Actions : https://docs.github.com/fr/actions
- lien syntaxe pour configurer une GitHub Actions : https://docs.github.com/fr/actions/using-workflows/workflow-syntax-for-github-actions

### Titre

- lien
- description

## 🚧 Je franchis les obstacles

### Point de blocage ❌ / ✔️

Description:

Plan d'action : (à valider par le formateur)

- action 1 ❌ / ✔️
- action 2 ❌ / ✔️
- ...

Résolution :

## 📽️ J'en fais la démonstration

- J'ai ecrit un [tutoriel](...) ❌ / ✔️
- J'ai fait une [présentation](...) ❌ / ✔️
