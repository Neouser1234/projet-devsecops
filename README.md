Projet 1 — Mise en place d'un pipeline CI/CD sécurisé
1. Présentation du projet
Ce projet consiste à mettre en place un pipeline d'intégration et de déploiement continus (CI/CD) avec Jenkins, afin d'automatiser les principales étapes du cycle de vie d'une application web et de préparer l'intégration de contrôles de sécurité.
2. Objectifs
Mettre en place un serveur Jenkins.
Héberger le code source dans un dépôt GitHub.
Préparer une application web de démonstration.
Définir un pipeline Jenkins comprenant les étapes de récupération du code, de build, de test, de sécurité et de déploiement.
Préparer l'intégration des outils développés par les membres du groupe.
3. Technologies utilisées
Jenkins : orchestration du pipeline CI/CD.
Git et GitHub : gestion des versions et hébergement du code source.
HTML : interface de l'application web.
Docker : préparation de la conteneurisation de l'application.
SonarQube : analyse de la qualité et de la sécurité du code, prévue dans le cadre du projet.
OWASP ZAP : tests de sécurité web, prévus dans le cadre du projet.
4. Structure du dépôt
projet-devsecops/
├── application/
│   ├── index.html
│   └── Dockerfile
├── Jenkinsfile
└── README.md
5. Fonctionnement du pipeline
Le pipeline Jenkins contient les étapes suivantes :
Checkout : récupération du code depuis GitHub.
Build : vérification de la présence des fichiers nécessaires à l'application.
Test : vérification automatisée d'un élément attendu dans la page HTML.
Analyse de code - SonarQube : emplacement prévu pour l'intégration de l'analyse de code.
Tests de sécurité web - OWASP ZAP : emplacement prévu pour l'intégration des tests de sécurité web.
Deploy : emplacement prévu pour la mise en place du déploiement automatisé.
Les étapes SonarQube, OWASP ZAP et Deploy sont actuellement des points d'intégration préparatoires. Les outils et le déploiement réel restent à configurer.
6. Répartition des responsabilités
Membre 1 : installation de Jenkins, dépôt GitHub, application web et squelette du pipeline.
Membre 2 : analyse de la qualité et de la sécurité du code avec SonarQube ou un outil équivalent.
Membre 3 : tests de sécurité web avec OWASP ZAP ou un outil équivalent.
Membre 4 : déploiement, tests complémentaires et validation de l'intégration.
7. État d'avancement
Le dépôt GitHub est opérationnel et le pipeline Jenkins exécute actuellement avec succès les vérifications de base. Les étapes destinées aux autres membres sont identifiées et restent à intégrer avec leurs contributions respectives.
8. Dépôt GitHub
https://github.com/Neouser1234/projet-devsecops
