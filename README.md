# Security Analysis CI/CD Pipeline

Ce projet configure un pipeline CI/CD avec des outils d'analyse statique (SonarQube) et dynamique (OWASP ZAP) pour une application web ou des microservices. Le pipeline est conçu pour intégrer des vérifications de sécurité à chaque étape du développement et du déploiement.

## Objectifs

- **Analyse Statique (SAST)** : Identifier les vulnérabilités de sécurité dans le code source avant qu'il ne soit déployé.
- **Analyse Dynamique (DAST)** : Tester les applications déployées en environnement de staging pour détecter les vulnérabilités de sécurité en temps réel.

## Structure du Projet

security-analysis-cicd/ 
│ ├── .github/ 
│ ├── workflows/ 
│ │ ├── ci.yml
│ │ └── cd.yml
│ ├── jenkins/ 
│ └── Jenkinsfile
│ ├── src/ 
│ └── (Code source de ton projet) 
│ └── README.md


## Prérequis

1. **SonarQube** : Serveur SonarQube configuré pour analyser le code source.
2. **OWASP ZAP** : Outil de test de sécurité des applications web.
3. **Jenkins** : Serveur Jenkins pour orchestrer les pipelines CI/CD.

## Configuration

### GitHub Actions

1. **Analyse Statique avec SonarQube**
   - Fichier : `.github/workflows/ci.yml`
   - Description : Exécute une analyse statique du code lors des commits et des demandes de tirage.
   - **Variables à configurer** :
     - `<your-project-key>` : Clé du projet SonarQube.
     - `<your-sonar-url>` : URL de ton serveur SonarQube.
     - Ajoute le token SonarQube (`SONARQUBE_TOKEN`) dans les secrets GitHub.

2. **Tests de Pénétration avec OWASP ZAP**
   - Fichier : `.github/workflows/cd.yml`
   - Description : Effectue des tests de pénétration automatisés sur les versions déployées en environnement de staging.
   - **Variables à configurer** :
     - `http://your-staging-url` : URL de l'environnement de staging où l'application est déployée.

### Jenkins

- Fichier : `jenkins/Jenkinsfile`
- Description : Pipeline Jenkins pour le build, l'analyse statique avec SonarQube, le déploiement et les tests de sécurité avec OWASP ZAP.
- **Variables à configurer** :
  - `<your-project-key>` : Clé du projet SonarQube.
  - `http://your-staging-url` : URL de l'environnement de staging.

## Installation et Exécution

1. **Configurer SonarQube** :
   - Installe et configure SonarQube selon [la documentation officielle](https://docs.sonarqube.org/latest/).

2. **Configurer OWASP ZAP** :
   - Installe OWASP ZAP sur le serveur de staging ou sur l'environnement où les tests seront exécutés.

3. **Configurer Jenkins** :
   - Installe et configure Jenkins selon [la documentation officielle](https://www.jenkins.io/doc/).
   - Assure-toi que les plugins nécessaires pour SonarQube et OWASP ZAP sont installés.

4. **Configurer les Secrets GitHub** :
   - Ajoute les secrets nécessaires dans les paramètres du dépôt GitHub (`SONARQUBE_TOKEN` pour SonarQube).

5. **Exécuter les Pipelines** :
   - Les workflows GitHub Actions s'exécuteront automatiquement à chaque commit ou demande de tirage.
   - Le pipeline Jenkins peut être déclenché manuellement ou configuré pour s'exécuter automatiquement.

## Exemples de Commandes

- **Lancer l'analyse statique avec SonarQube localement** :

  ```
  mvn clean verify sonar:sonar -Dsonar.projectKey=<your-project-key> -Dsonar.host.url=<your-sonar-url> -Dsonar.login=<your-sonar-token>
  ``` 

## Lancer OWASP ZAP en mode daemon :

  ```
  zap.sh -daemon -port 8080
  ``` 

## Contribution
Les contributions sont les bienvenues ! Veuillez ouvrir une demande de tirage pour toute modification ou ajout. Assurez-vous de suivre les bonnes pratiques de développement et d'inclure des tests pour les nouvelles fonctionnalités.
