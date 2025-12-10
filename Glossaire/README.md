# 📚 Glossaire Technique - Développeur Full Stack

Dictionnaire complet des termes techniques essentiels pour le développement web et la collaboration en entreprise.

![Tech](https://img.shields.io/badge/Tech-Glossary-blue?style=flat-square)
![Full Stack](https://img.shields.io/badge/Full_Stack-Developer-green?style=flat-square)
![Enterprise](https://img.shields.io/badge/Enterprise-Ready-orange?style=flat-square)

## 📖 Description

Ce glossaire regroupe tous les termes techniques, acronymes et concepts qu'un développeur full stack doit maîtriser pour évoluer en entreprise. Des bases aux concepts avancés, en passant par le jargon métier et les méthodologies.

---

## 🌐 Développement Web - Concepts de Base

### Frontend / Client-Side
**Le frontend** désigne la partie visible et interactive d'une application web avec laquelle l'utilisateur interagit directement.

- **UI (User Interface)** : Interface utilisateur - l'aspect visuel de l'application
- **UX (User Experience)** : Expérience utilisateur - la facilité et plaisir d'utilisation
- **DOM (Document Object Model)** : Représentation en arbre des éléments HTML d'une page
- **SPA (Single Page Application)** : Application qui charge une seule page HTML et met à jour le contenu dynamiquement
- **PWA (Progressive Web App)** : Application web qui se comporte comme une app native
- **Responsive Design** : Design qui s'adapte automatiquement à tous les écrans
- **Mobile-First** : Approche de design en commençant par les écrans mobiles

### Backend / Server-Side
**Le backend** est la partie serveur d'une application qui gère la logique métier, les données et les communications.

- **API (Application Programming Interface)** : Interface permettant la communication entre applications
- **REST (Representational State Transfer)** : Architecture pour les APIs web utilisant HTTP
- **CRUD (Create, Read, Update, Delete)** : Opérations de base sur les données
- **Endpoint** : URL spécifique d'une API qui répond à des requêtes
- **Middleware** : Couche logicielle qui s'exécute entre la requête et la réponse
- **ORM (Object-Relational Mapping)** : Technique pour convertir des données entre systèmes incompatibles
- **MVC (Model-View-Controller)** : Pattern architectural séparant logique, présentation et contrôle

### Full Stack
**Un développeur full stack** maîtrise à la fois le frontend et le backend, capable de développer une application complète.

---

## 🗄️ Bases de Données

### Types de Bases de Données
- **SGBD (Système de Gestion de Base de Données)** : Logiciel pour gérer les bases de données
- **SQL (Structured Query Language)** : Langage de requête pour bases de données relationnelles
- **NoSQL** : Bases de données non-relationnelles (documents, graphes, clé-valeur)
- **ACID (Atomicity, Consistency, Isolation, Durability)** : Propriétés des transactions de BDD

### Concepts Clés
- **Schéma** : Structure organisationnelle de la base de données
- **Table** : Structure de données en lignes et colonnes (relationnel)
- **Collection** : Équivalent de table dans NoSQL (documents)
- **Clé primaire** : Identifiant unique d'un enregistrement
- **Clé étrangère** : Référence vers une clé primaire d'une autre table
- **Index** : Structure pour accélérer les requêtes
- **Migration** : Modification de la structure de la base de données
- **Seed** : Données initiales pour alimenter la base

---

## 🔧 Outils et Technologies

### Gestionnaires de Versions
- **Git** : Système de contrôle de version distribué
- **Repository (Repo)** : Espace de stockage d'un projet avec son historique
- **Commit** : Enregistrement des modifications dans l'historique
- **Branch** : Branche de développement parallèle
- **Merge** : Fusion de branches
- **Pull Request (PR)** : Demande de fusion avec review de code
- **Fork** : Copie personnelle d'un repository

### Gestion de Packages
- **Package Manager** : Outil de gestion des dépendances (npm, pip, composer)
- **Dépendance** : Librarie externe nécessaire au projet
- **Dev Dependencies** : Dépendances utilisées seulement en développement
- **Lock File** : Fichier verrouillant les versions exactes des dépendances
- **Semantic Versioning (SemVer)** : Convention de nommage des versions (MAJOR.MINOR.PATCH)

### Build et Bundling
- **Build** : Processus de transformation du code source en version finale
- **Bundler** : Outil qui regroupe les fichiers en un ou plusieurs bundles
- **Transpilation** : Conversion de code d'un langage vers un autre
- **Minification** : Réduction de la taille des fichiers pour la production
- **Tree Shaking** : Élimination du code non utilisé
- **Hot Reload** : Rechargement automatique lors des modifications
- **Watch Mode** : Surveillance des fichiers pour rebuild automatique

---

## 🏗️ Architecture et Patterns

### Architecture Logicielle
- **Monolithe** : Application développée comme une seule unité déployable
- **Microservices** : Architecture divisant l'application en services indépendants
- **SOA (Service-Oriented Architecture)** : Architecture orientée services
- **Event-Driven Architecture** : Architecture basée sur les événements
- **CQRS (Command Query Responsibility Segregation)** : Séparation lecture/écriture
- **DDD (Domain-Driven Design)** : Conception pilotée par le domaine métier

### Design Patterns
- **Singleton** : Pattern garantissant une seule instance d'une classe
- **Factory** : Pattern de création d'objets
- **Observer** : Pattern de notification automatique des changements
- **Strategy** : Pattern d'interchangeabilité d'algorithmes
- **Dependency Injection** : Technique d'inversion de dépendances
- **Repository Pattern** : Abstraction de l'accès aux données

---

## 🚀 DevOps et Déploiement

### Intégration Continue
- **CI/CD (Continuous Integration/Continuous Deployment)** : Automatisation build/déploiement
- **Pipeline** : Séquence automatisée d'étapes de développement
- **Build Server** : Serveur automatisant les builds et tests
- **Artifact** : Résultat packagé d'un build
- **Release** : Version stable déployée en production

### Conteneurisation et Orchestration
- **Docker** : Plateforme de conteneurisation d'applications
- **Container** : Unité d'exécution légère contenant une application
- **Image** : Template pour créer des containers
- **Dockerfile** : Fichier de configuration pour construire une image
- **Kubernetes (K8s)** : Orchestrateur de containers
- **Pod** : Plus petite unité déployable dans Kubernetes

### Environnements
- **Development (Dev)** : Environnement de développement local
- **Staging** : Environnement de test proche de la production
- **Production (Prod)** : Environnement final accessible aux utilisateurs
- **UAT (User Acceptance Testing)** : Tests d'acceptation utilisateur
- **Blue-Green Deployment** : Technique de déploiement sans interruption

---

## 🔐 Sécurité

### Authentification et Autorisation
- **Authentication** : Vérification de l'identité d'un utilisateur
- **Authorization** : Contrôle des permissions d'accès
- **JWT (JSON Web Token)** : Standard pour les tokens d'authentification
- **OAuth** : Protocol d'autorisation pour accès tiers
- **SSO (Single Sign-On)** : Connexion unique pour plusieurs applications
- **2FA/MFA (Two-Factor/Multi-Factor Authentication)** : Authentification à plusieurs facteurs

### Sécurité Web
- **HTTPS** : HTTP sécurisé avec chiffrement SSL/TLS
- **CORS (Cross-Origin Resource Sharing)** : Politique de partage de ressources
- **XSS (Cross-Site Scripting)** : Injection de scripts malveillants
- **CSRF (Cross-Site Request Forgery)** : Attaque par requête forgée
- **SQL Injection** : Injection de code SQL malveillant
- **OWASP** : Organisation définissant les risques de sécurité web

---

## 📊 Performance et Monitoring

### Performance
- **Caching** : Mise en cache pour accélérer l'accès aux données
- **CDN (Content Delivery Network)** : Réseau de serveurs pour distribuer le contenu
- **Load Balancing** : Répartition de charge entre plusieurs serveurs
- **Lazy Loading** : Chargement différé des ressources
- **Code Splitting** : Division du code en plusieurs chunks
- **Compression** : Réduction de taille des fichiers (Gzip, Brotli)

### Monitoring et Analytics
- **Logs** : Fichiers d'enregistrement des événements système
- **Metrics** : Données quantitatives sur les performances
- **APM (Application Performance Monitoring)** : Surveillance des performances applicatives
- **Health Check** : Vérification automatique de l'état du système
- **Uptime** : Pourcentage de temps où le service est disponible
- **SLA (Service Level Agreement)** : Accord sur le niveau de service

---

## 🧪 Tests et Qualité

### Types de Tests
- **Unit Test** : Test d'une unité de code isolée
- **Integration Test** : Test de l'interaction entre composants
- **E2E Test (End-to-End)** : Test du parcours utilisateur complet
- **Regression Test** : Test de non-régression après modifications
- **Load Test** : Test de performance sous charge
- **A/B Testing** : Test de deux versions pour comparer les performances

### Outils et Pratiques
- **TDD (Test-Driven Development)** : Développement guidé par les tests
- **BDD (Behavior-Driven Development)** : Développement guidé par le comportement
- **Mock** : Simulation d'un composant pour les tests
- **Stub** : Version simplifiée d'un composant pour les tests
- **Code Coverage** : Pourcentage de code couvert par les tests
- **Static Analysis** : Analyse du code sans l'exécuter

---

## 👥 Méthodologies et Collaboration

### Méthodes Agiles
- **Scrum** : Framework agile avec sprints et cérémonies
- **Sprint** : Période de développement de 1-4 semaines
- **Product Owner (PO)** : Responsable de la vision produit
- **Scrum Master** : Facilitateur de l'équipe Scrum
- **Daily Standup** : Réunion quotidienne de synchronisation
- **Retrospective** : Réunion d'amélioration continue
- **User Story** : Description fonctionnelle du point de vue utilisateur
- **Epic** : Grande fonctionnalité divisée en plusieurs User Stories
- **Backlog** : Liste priorisée des fonctionnalités à développer

### Kanban et Gestion
- **Kanban** : Méthode visuelle de gestion des flux de travail
- **WIP (Work In Progress)** : Limite du travail en cours
- **Burndown Chart** : Graphique de progression du travail restant
- **Velocity** : Mesure de la capacité de livraison de l'équipe
- **Technical Debt** : Code sous-optimal à refactoriser plus tard
- **Refactoring** : Amélioration de la structure du code sans changer sa fonctionnalité

---

## 📱 Technologies Frontend

### Frameworks et Libraries
- **Framework** : Structure complète pour développer une application
- **Library** : Collection de fonctions réutilisables
- **Component** : Élément réutilisable d'interface utilisateur
- **State Management** : Gestion de l'état global de l'application
- **Virtual DOM** : Représentation virtuelle du DOM pour optimiser les performances
- **Hydration** : Processus d'ajout d'interactivité au HTML statique

### Concepts Modernes
- **JAMstack (JavaScript, APIs, Markup)** : Architecture web moderne
- **SSR (Server-Side Rendering)** : Rendu côté serveur
- **SSG (Static Site Generation)** : Génération de site statique
- **ISR (Incremental Static Regeneration)** : Régénération statique incrémentale
- **Micro-Frontend** : Architecture frontend en modules indépendants

---

## ⚙️ Technologies Backend

### APIs et Services
- **GraphQL** : Langage de requête pour APIs
- **gRPC** : Framework RPC haute performance
- **WebSocket** : Protocol de communication bidirectionnelle
- **Webhook** : Callback HTTP pour notifications temps réel
- **Rate Limiting** : Limitation du nombre de requêtes par utilisateur
- **Pagination** : Division des résultats en pages

### Architecture et Patterns
- **Serverless** : Architecture sans gestion de serveur
- **FaaS (Function as a Service)** : Exécution de fonctions à la demande
- **Event Sourcing** : Stockage des événements plutôt que de l'état
- **Message Queue** : File d'attente pour traitement asynchrone
- **Pub/Sub** : Pattern publication/abonnement pour messaging

---

## 🏢 Termes Entreprise et Métier

### Rôles et Équipes
- **CTO (Chief Technology Officer)** : Directeur technique
- **Tech Lead** : Leader technique d'une équipe
- **DevOps Engineer** : Spécialiste intégration développement/opérations
- **Site Reliability Engineer (SRE)** : Ingénieur fiabilité des systèmes
- **Data Engineer** : Ingénieur données
- **QA (Quality Assurance)** : Assurance qualité/testeur
- **Business Analyst** : Analyste métier

### Processus Business
- **MVP (Minimum Viable Product)** : Version minimale d'un produit
- **POC (Proof of Concept)** : Preuve de faisabilité
- **ROI (Return on Investment)** : Retour sur investissement
- **KPI (Key Performance Indicator)** : Indicateur clé de performance
- **SaaS (Software as a Service)** : Logiciel en tant que service
- **B2B (Business to Business)** : Commerce entre entreprises
- **B2C (Business to Consumer)** : Commerce vers les consommateurs

### Gestion de Projet
- **Milestone** : Jalons importants du projet
- **Deadline** : Date limite de livraison
- **Scope Creep** : Dérive du périmètre du projet
- **Stakeholder** : Partie prenante du projet
- **Go-Live** : Mise en production
- **Post-Mortem** : Analyse après incident
- **Rollback** : Retour à la version précédente

---

## 🔤 Acronymes Essentiels

### Développement
- **ACID** : Atomicity, Consistency, Isolation, Durability
- **SOLID** : Principes de programmation orientée objet
- **DRY** : Don't Repeat Yourself
- **KISS** : Keep It Simple, Stupid
- **YAGNI** : You Ain't Gonna Need It
- **CRUD** : Create, Read, Update, Delete
- **CORS** : Cross-Origin Resource Sharing

### Infrastructure
- **AWS** : Amazon Web Services
- **GCP** : Google Cloud Platform
- **IaaS** : Infrastructure as a Service
- **PaaS** : Platform as a Service
- **CDN** : Content Delivery Network
- **DNS** : Domain Name System
- **SSL/TLS** : Secure Sockets Layer/Transport Layer Security

### Méthodologies
- **CI/CD** : Continuous Integration/Continuous Deployment
- **TDD** : Test-Driven Development
- **BDD** : Behavior-Driven Development
- **MVP** : Minimum Viable Product
- **POC** : Proof of Concept
- **UAT** : User Acceptance Testing

---

## 💡 Conseils pour Mémoriser

### Techniques d'apprentissage
1. **Contextualisez** : Utilisez les termes dans des projets réels
2. **Pratiquez** : Expérimentez avec les technologies mentionnées
3. **Enseignez** : Expliquez les concepts à d'autres développeurs
4. **Lisez** : Suivez blogs, documentation et articles techniques
5. **Participez** : Rejoignez des communautés et forums

### Ressources recommandées
- **MDN Web Docs** : Documentation web de référence
- **Stack Overflow** : Communauté de développeurs
- **GitHub** : Exploration de projets open source
- **Tech Blogs** : Medium, Dev.to, CSS-Tricks
- **Podcasts** : Syntax, CodePen Radio, Shop Talk Show

---

*Ce glossaire évolue avec les technologies. N'hésitez pas à le consulter régulièrement et à contribuer en proposant de nouveaux termes !*