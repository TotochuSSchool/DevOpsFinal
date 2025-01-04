> de Maxime Masson et Mélène Dufrénois.

# Rapport

## Git

Pour notre projet, nous utilisons la méthode **Trunk-based development (TBD)**.

Les différentes branches utilisées sont :

- `main`: Contient le code finalisé et prêt pour la mise en production.
- `develop`:  Regroupe le code en cours de développement.
- `feature/nom-de-la-branche`: pour les fonctionnalités ajoutées.
- `hotfix/nom-du-bug`:  pour les corrections de bugs identifiés en production.

Pour plus de détails, nous avons documenté le nécessaire dans le fichier `git.md`.

## Ce que nous avons fait

### Docker
Nous avons créé et déployé des images Docker pour les trois applications suivantes :
- `web-client`
- `vote-api`
- `docs`

### Docker Compose

Un fichier docker-compose.yml a été créé pour exécuter l'application `vote-api`, avec la base de données associée.

### CI/CD
Voir ci-après.

### Exigences supplémentaires

Les applications sont exécutées dans des conteneurs non-root pour des raisons de sécurité.
L’image latest correspond toujours à la dernière version stable de l’application.
Les secrets (Url database, docker User/pass, Netlify Site/token, Api Key render) sont stockés dans les secrets GitHub/render afin de ne pas etre visible dans le code source.

## Comment notre projet est déployé

Comme précisé ci-dessus, le déploiement du projet est orchestré à l’aide de Docker Compose pour gérer les conteneurs. Le processus est entièrement automatisé grâce à un pipeline CI/CD configuré via GitHub Actions.

### CI/CD Pipeline

- Les pipelines sont configurés pour être déclenchés automatiquement à chaque push ou pull request.
- Le pipeline CI effectue une série de tests et de validations avant de fusionner les changements dans les branches principales.
- Le pipeline CD se charge du déploiement vers les environnements de production.


## Liens

- Projet : [\[Dépôt GitHub\]](https://github.com/TotochuSSchool/DevOpsFinal)
- Web Client: [\[URL Web Client\]](https://devopsfinal-webclient.onrender.com/)
- Vote-API : [\[URL Vote-API\]](https://devopsfinal.onrender.com/)
- Doc : [\[URL on Netlify\]](https://devops-final-doc.netlify.app/)

## Comment contribuer au projet

1. Faire un fork du projet actuel dans vos repositories et le cloner localement.
```bash
git clone <URL-du-fork>
```
2. Créer une branche permettant d'ajouter une fonctionnalité.
```bash
git checkout -b feature/nom-de-la-branche
```
3. Implémenter les nouvelles fonctionnalités.
4. Faire un commit des changements sur cette branche en utilisant Gitmoji et pousser sur la branche distante. 
```bash
git commit -m ":sparkles: New feature added"
git push
```
5. Créer une Pull Request afin de merger les changements.

---

### Détails

Au final, avec la complexité du travail demandé, nous remarquons des écarts par rapport à nos ambitions initiales, et en particulier au modèle **Trunk-Based Development (TBD)**. Les branches n'ont pas toujours été utilisées comme prévu, ce qui a affecté la fluidité du développement.

Nous avons rencontré d'autres problèmes, notamment la fonctionnalité de "like" qui ne fonctionne pas. Une cause probable réside dans la connexion avec la base de données.

Pour pousser notre projet, des éléments pouvant être mis en place et que nous envisageons pour la suite sont les tests unitaires afin d'assurer une stabilité de code mais également l'ajout de badges de statut permettant d'indiquer l'état de la CI/CD.

---