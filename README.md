Pipeline CI/CD Complète pour Application Flask

 Objectif du Projet
Mise en place d'une pipeline d'intégration continue (CI) et de déploiement continu (CD) pour le déploiement automatisé d'une application web Flask avec garantie de qualité et sécurité.

 Fonctionnalités Implémentées

Linter
- Flake8 : Validation syntaxique du code Python (ignore E501, E303)
- Hadolint : Analyse du Dockerfile pour les meilleures pratiques

Compilation
- Construction d'image Docker avec tagging intelligent
- Artefacts de build conservés pour 1 semaine

Scan de Sécurité (Trivy)
- Analyse des vulnérabilités sur les images Docker
- Niveaux de sévérité : CRITICAL et HIGH
- Mode `allow_failure: true` pour continuation du pipeline

Tests Automatisés
- Tests unitaires et d'intégration Python
- Génération de rapports JUnit XML
- Couverture de code avec rapport coverage.xml

Vérification Qualité de Code (SonarCloud)
- Analyse statique du code avec SonarCloud
- Intégration des rapports de tests et coverage
- Quality Gate avec attente des résultats

Packaging
- Push des images vers le registry GitLab
- Tags multiples : `$CI_COMMIT_REF_SLUG` et `latest`
- Authentification sécurisée avec variables CI/CD

Déploiement Dynamique en Review
- Environnements dynamiques par branche
- Déploiement automatique sur Merge Requests
- Arrêt manuel des environnements via job `stop_review`

Staging
- Déploiement automatique sur branche `main`
- Restart policy `unless-stopped`
- Port mapping 5000:5000

 Production
- Déploiement manuel avec validation
- Port mapping 80:5000 pour accès HTTP
- Restart policy `unless-stopped`

 ests de Validation
- Vérification de santé des applications déployées
- Timeout de 50 secondes avec retries
- Validation sur les endpoints `/health`

 Modèle Gitflow Implémenté

 🔹 Branche Principale (`main`)
```yaml
rules:
  - if: $CI_COMMIT_BRANCH == "main"