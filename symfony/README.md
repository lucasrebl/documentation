# Création d'un projet Symfony

Ce guide explique comment créer un nouveau projet Symfony avec une configuration Docker.

## Prérequis

- PHP 8.2 ou supérieur
- Composer
- Docker et Docker Compose
- Symfony CLI (optionnel mais recommandé)

## Étapes de création

1. Créez un nouveau projet Symfony avec le squelette de base :
```bash
composer create-project symfony/skeleton:"7.x.x" nom-du-projet
cd nom-du-projet
```

2. Ajoutez les packages nécessaires pour une application web :
```bash
composer require webapp
```

## Configuration Docker

### 1. Créer le fichier `docker-compose.yml`
```yaml
services:
  database:
    image: mysql:8.0
    command: --default-authentication-plugin=mysql_native_password
    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
    ports:
      - '3306:3306'
    volumes:
      - database_data:/var/lib/mysql

  php:
    build:
      context: ./
      dockerfile: Dockerfile
    volumes:
      - ./:/var/www/html
    depends_on:
      - database

  nginx:
    image: nginx:alpine
    ports:
      - '8080:80'
    volumes:
      - ./:/var/www/html
      - ./docker/nginx/default.conf:/etc/nginx/conf.d/default.conf
    depends_on:
      - php

volumes:
  database_data:
```

### 2. Créer le fichier `Dockerfile`
```dockerfile
FROM php:8.2-fpm

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libicu-dev \
    libzip-dev

# Install PHP extensions
RUN docker-php-ext-install \
    pdo_mysql \
    intl \
    zip

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /var/www/html

# Expose port 9000
EXPOSE 9000

CMD ["php-fpm"]
```

### 3. Créer le fichier `docker/nginx/default.conf`
```nginx
server {
    listen 80;
    server_name localhost;
    root /var/www/html/public;

    location / {
        try_files $uri /index.php$is_args$args;
    }

    location ~ ^/index\.php(/|$) {
        fastcgi_pass php:9000;
        fastcgi_split_path_info ^(.+\.php)(/.*)$;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param DOCUMENT_ROOT $document_root;
        internal;
    }

    location ~ \.php$ {
        return 404;
    }

    error_log /var/log/nginx/project_error.log;
    access_log /var/log/nginx/project_access.log;
}
```

### 4. Créer et configurer le fichier `.env`
```env
# Database configuration
MYSQL_DATABASE=
MYSQL_USER=
MYSQL_PASSWORD=
MYSQL_ROOT_PASSWORD=

DATABASE_URL=

# Other configuration
DEFAULT_URI=
MESSENGER_TRANSPORT_DSN=
```

### 5. Créer et configurer le fichier `.env.local`
```env
# Database configuration
MYSQL_DATABASE=mysql_database
MYSQL_USER=mysql_user
MYSQL_PASSWORD=mysql_password
MYSQL_ROOT_PASSWORD=password

DATABASE_URL="mysql://${MYSQL_USER}:${MYSQL_PASSWORD}@database:3306/${MYSQL_DATABASE}?serverVersion=8.0"

# Other configuration
DEFAULT_URI=
MESSENGER_TRANSPORT_DSN=
```

## Structure du projet

```
nom-du-projet/
├── assets/         # Fichiers front (JS, CSS, images)
├── config/         # Configuration de l'application
├── migrations/     # Migrations de base de données
├── public/         # Point d'entrée public
├── src/           # Code source de l'application
│   ├── Controller/  # Contrôleurs
│   ├── Entity/      # Entités Doctrine
│   ├── Repository/  # Repositories
│   └── Service/     # Services métier
├── templates/     # Templates Twig
├── tests/         # Tests automatisés
├── docker/        # Configuration Docker
│   ├── nginx/     # Configuration Nginx
│   └── php/       # Configuration PHP
├── .env           # Variables d'environnement par défaut
├── .env.local     # Variables d'environnement locales
├── Dockerfile     # Configuration du conteneur PHP
└── docker-compose.yml  # Configuration Docker Compose
```

## Démarrage du projet

1. Construire et démarrer les conteneurs :
```bash
docker-compose up -d --build
```

2. Installer les dépendances :
```bash
docker-compose exec php composer install
```

3. Créer la base de données :
```bash
docker-compose exec php bin/console doctrine:database:create
docker-compose exec php bin/console doctrine:migrations:migrate
```

4. Récupérer les fixtures : 
```bash
docker-compose exec php php bin/console doctrine:fixtures:load
```

5. Accéder à l'application :
```
http://localhost:8080
```

## Scripts disponibles

```bash
# Démarrer les conteneurs
docker-compose up -d

# Arrêter les conteneurs
docker-compose down

# Accéder au conteneur PHP
docker-compose exec php bash

# Vider le cache
docker-compose exec php bin/console cache:clear

# Créer une migration
docker-compose exec php bin/console make:migration

# Exécuter les migrations
docker-compose exec php bin/console doctrine:migrations:migrate
```

## Vérification de l'installation

Pour vérifier que tout fonctionne correctement :

1. Vérifier que tous les conteneurs sont en cours d'exécution :
```bash
docker-compose ps
```

2. Vérifier les logs des conteneurs :
```bash
docker-compose logs
```

3. Vérifier la configuration Symfony :
```bash
docker-compose exec php bin/console about
```

## Commandes utiles Symfony

```bash
# Créer un contrôleur
docker-compose exec php bin/console make:controller

# Créer une entité
docker-compose exec php bin/console make:entity

# Créer un formulaire
docker-compose exec php bin/console make:form
```

## Configuration IDE recommandée

- PHPStorm avec les plugins Symfony
- VS Code avec les extensions :
  - PHP Intelephense
  - Symfony for VSCode
  - PHP Debug
  - Twig Language 2
