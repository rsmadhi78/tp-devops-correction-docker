# TP DevOps – CI/CD avec Docker, GitHub Actions et SonarCloud

Ce dépôt contient le code et la configuration associés au TP DevOps 2025. L'objectif principal est de mettre en place un pipeline complet d'intégration et de livraison continue (CI/CD) pour une application Java utilisant Maven, Docker, GitHub Actions et SonarCloud.


##  Structure du projet

tp-devops-correction-docker/
├── simple-api/ → Code backend Java avec Maven
├── database/ → Dockerfile de la base de données PostgreSQL
├── http-server/ → Serveur HTTP Apache (httpd) personnalisé
└── .github/workflows/ → Workflows GitHub Actions (ci.yml et cd.yml)

---

## ⚙️ Étapes réalisées

### 1. Intégration Continue (CI)

Mise en place d'un workflow GitHub Actions qui :

- Se déclenche à chaque **push** ou **pull request** sur `main` ou `develop`
- Compile et teste l'application avec **Maven**
- Lance une analyse de code avec **SonarCloud**

> L’objectif est de **garantir la qualité du code avant tout déploiement**.

### 2. SonarCloud – Quality Gate

- Création d’un projet SonarCloud lié au dépôt
- Génération d’un token sécurisé stocké dans les secrets GitHub
- Intégration de la commande Sonar dans le workflow CI :

```bash
mvn -B verify sonar:sonar \
  -Dsonar.projectKey=rsmadhi78_tp-devops-correction-docker \
  -Dsonar.organization=rsmadhi-org \
  -Dsonar.host.url=https://sonarcloud.io \
  -Dsonar.login=${{ secrets.SONAR_TOKEN }}
