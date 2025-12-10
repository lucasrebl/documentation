# 🏷️ Types de Données SQL

Guide complet des types de données SQL avec cas d'usage et bonnes pratiques pour chaque SGBD.

![SQL](https://img.shields.io/badge/SQL-DataTypes-blue?style=flat-square)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=flat-square)

---

## 📖 Introduction

Le choix du bon type de données est crucial pour :
- **Performance** : Optimisation de l'espace de stockage et vitesse des requêtes
- **Intégrité** : Validation automatique des données
- **Fonctionnalités** : Accès aux fonctions spécifiques du type
- **Évolutivité** : Faciliter les modifications futures

---

## 🔢 Types Numériques

### Entiers (Integer Types)

#### TINYINT
**Taille** : 1 byte (-128 à 127 ou 0 à 255 si UNSIGNED)
```sql
-- Exemples d'usage
status TINYINT,           -- Statuts (0=inactif, 1=actif)
age TINYINT UNSIGNED,     -- Âge (0-255)
priority TINYINT DEFAULT 0 -- Priorité (-128 à 127)
```
**🎯 Cas d'usage** :
- Booléens (0/1)
- Statuts avec peu de valeurs
- Âges, notes, pourcentages
- Drapeaux et indicateurs

#### SMALLINT
**Taille** : 2 bytes (-32,768 à 32,767 ou 0 à 65,535 si UNSIGNED)
```sql
-- Exemples d'usage
year SMALLINT,            -- Années
port_number SMALLINT UNSIGNED, -- Ports réseau
quantity SMALLINT DEFAULT 0    -- Quantités limitées
```
**🎯 Cas d'usage** :
- Années, mois
- Ports, codes courts
- Quantités modérées
- Identifiants de petites listes

#### MEDIUMINT (MySQL)
**Taille** : 3 bytes (-8,388,608 à 8,388,607)
```sql
-- Exemples d'usage
population MEDIUMINT UNSIGNED, -- Population de villes
views_count MEDIUMINT DEFAULT 0 -- Compteurs moyens
```
**🎯 Cas d'usage** :
- Compteurs moyens
- Populations de villes
- Statistiques modérées

#### INT / INTEGER
**Taille** : 4 bytes (-2,147,483,648 à 2,147,483,647)
```sql
-- Exemples d'usage
user_id INT AUTO_INCREMENT PRIMARY KEY,
salary INT UNSIGNED,           -- Salaires en centimes
stock_quantity INT DEFAULT 0   -- Stocks
```
**🎯 Cas d'usage** :
- **Clés primaires** (le plus courant)
- Montants en centimes
- Stocks, compteurs importants
- Identifiants de référence

#### BIGINT
**Taille** : 8 bytes (très grande plage)
```sql
-- Exemples d'usage
transaction_id BIGINT AUTO_INCREMENT,
timestamp_ms BIGINT,          -- Timestamp en millisecondes  
facebook_id BIGINT UNSIGNED,  -- IDs de réseaux sociaux
file_size BIGINT             -- Tailles de fichiers en bytes
```
**🎯 Cas d'usage** :
- **Très gros volumes de données**
- Timestamps précis
- IDs de systèmes externes
- Tailles de fichiers, compteurs massifs

### Nombres Décimaux

#### DECIMAL / NUMERIC
**Précision exacte** - Stockage fixe selon la précision
```sql
-- Syntaxe : DECIMAL(précision, échelle)
price DECIMAL(10,2),          -- Prix : 99999999.99
percentage DECIMAL(5,2),      -- Pourcentage : 999.99%  
latitude DECIMAL(10,8),       -- Coordonnées GPS précises
exchange_rate DECIMAL(15,6)   -- Taux de change précis
```
**🎯 Cas d'usage** :
- **Argent et prix** (obligatoire pour éviter erreurs d'arrondi)
- Pourcentages précis
- Coordonnées GPS
- Calculs financiers

#### FLOAT
**Taille** : 4 bytes - Précision approximative
```sql
-- Exemples d'usage  
temperature FLOAT,            -- Températures
weight_kg FLOAT,             -- Poids approximatifs
cpu_usage FLOAT             -- Statistiques de performance
```
**🎯 Cas d'usage** :
- Mesures scientifiques
- Statistiques approximatives
- **⚠️ Éviter pour l'argent** (erreurs d'arrondi)

#### DOUBLE
**Taille** : 8 bytes - Précision approximative élevée
```sql
-- Exemples d'usage
scientific_calculation DOUBLE, -- Calculs scientifiques
gps_precision DOUBLE,         -- Coordonnées très précises  
statistical_average DOUBLE   -- Moyennes calculées
```
**🎯 Cas d'usage** :
- Calculs scientifiques complexes
- Coordonnées haute précision
- Analyses statistiques avancées

---

## 📝 Types Texte et Caractères

### Chaînes de Caractères Fixes

#### CHAR(n)
**Taille fixe** - Toujours n caractères (complété par des espaces)
```sql
-- Exemples d'usage
country_code CHAR(2),         -- Codes pays : 'FR', 'US'
gender CHAR(1),              -- Genre : 'M', 'F', 'O'  
currency_code CHAR(3),       -- Devises : 'EUR', 'USD'
status_flag CHAR(1) DEFAULT 'A' -- Statuts : 'A'ctif, 'I'nactif
```
**🎯 Cas d'usage** :
- **Codes standardisés** de longueur fixe
- Drapeaux de statut
- Identifiants courts et fixes
- **Performance optimale** pour longueur constante

### Chaînes de Caractères Variables

#### VARCHAR(n)
**Taille variable** - Jusqu'à n caractères
```sql
-- Exemples d'usage
username VARCHAR(50),         -- Noms d'utilisateur
email VARCHAR(320),          -- Emails (longueur max RFC)
first_name VARCHAR(100),     -- Prénoms  
product_name VARCHAR(255),   -- Noms de produits
slug VARCHAR(255)           -- URLs friendly
```
**🎯 Cas d'usage** :
- **Noms, emails, titres** (le plus courant)
- URLs, slugs
- Données de longueur modérée et variable
- **Choix par défaut** pour texte court-moyen

### Texte Long

#### TEXT
**Stockage de texte long** - Jusqu'à 65,535 caractères
```sql
-- Exemples d'usage
description TEXT,            -- Descriptions de produits
comment TEXT,               -- Commentaires  
article_excerpt TEXT,       -- Extraits d'articles
settings_json TEXT         -- Configuration JSON
```
**🎯 Cas d'usage** :
- Descriptions, commentaires
- Contenu de longueur moyenne
- Configurations JSON courtes

#### MEDIUMTEXT (MySQL)
**Texte très long** - Jusqu'à ~16 millions de caractères
```sql
-- Exemples d'usage
article_content MEDIUMTEXT,  -- Contenu d'articles complets
log_data MEDIUMTEXT,        -- Logs détaillés
html_template MEDIUMTEXT    -- Templates HTML
```
**🎯 Cas d'usage** :
- Articles, blogs complets
- Templates HTML/CSS
- Logs détaillés

#### LONGTEXT (MySQL)
**Texte massif** - Jusqu'à ~4 milliards de caractères
```sql
-- Exemples d'usage  
file_content LONGTEXT,      -- Contenu de fichiers
backup_data LONGTEXT,       -- Sauvegardes texte
full_document LONGTEXT     -- Documents complets
```
**🎯 Cas d'usage** :
- Stockage de fichiers texte
- Sauvegardes complètes
- **Usage rare** - préférer stockage fichier

---

## 📅 Types Date et Temps

### DATE
**Format** : 'YYYY-MM-DD' - Stocke uniquement la date
```sql
-- Exemples d'usage
birth_date DATE,            -- Dates de naissance
hire_date DATE,             -- Dates d'embauche  
expiry_date DATE,          -- Dates d'expiration
event_date DATE           -- Dates d'événements
```
**🎯 Cas d'usage** :
- **Dates sans heure** (anniversaires, échéances)
- Planification d'événements
- Historique par jour

### TIME  
**Format** : 'HH:MM:SS' - Stocke uniquement l'heure
```sql
-- Exemples d'usage
opening_time TIME,          -- Heures d'ouverture : '09:00:00'
meeting_duration TIME,      -- Durée : '01:30:00'
daily_reminder TIME        -- Rappels quotidiens
```
**🎯 Cas d'usage** :
- Horaires d'ouverture
- Durées
- Planification récurrente

### DATETIME
**Format** : 'YYYY-MM-DD HH:MM:SS' - Date et heure complètes
```sql
-- Exemples d'usage
created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
updated_at DATETIME ON UPDATE CURRENT_TIMESTAMP,
appointment_datetime DATETIME,   -- Rendez-vous précis
log_timestamp DATETIME         -- Horodatage de logs
```
**🎯 Cas d'usage** :
- **Audit trails** (créé/modifié le)
- Rendez-vous, événements précis
- Logs temporels
- **Choix standard** pour horodatage

### TIMESTAMP
**Format** : 'YYYY-MM-DD HH:MM:SS' - Avec gestion timezone
```sql
-- Exemples d'usage
last_login TIMESTAMP,          -- Dernière connexion
session_start TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
api_call_time TIMESTAMP       -- Horodatage API
```
**🎯 Cas d'usage** :
- **Applications multi-timezone**
- Sessions utilisateurs
- APIs internationales
- Synchronisation système

### YEAR
**Format** : YYYY - Année seulement (MySQL)
```sql
-- Exemples d'usage
graduation_year YEAR,         -- Année de diplôme
car_year YEAR,               -- Année de fabrication
fiscal_year YEAR            -- Année fiscale
```
**🎯 Cas d'usage** :
- Années de référence
- Historiques annuels
- Classifications temporelles

---

## ✅ Types Booléens et Logiques

### BOOLEAN / BOOL
**Valeurs** : TRUE (1) ou FALSE (0)
```sql
-- Exemples d'usage
is_active BOOLEAN DEFAULT TRUE,    -- Statut actif/inactif
is_verified BOOLEAN DEFAULT FALSE, -- Email vérifié
has_discount BOOLEAN,              -- Éligible remise
is_premium BOOLEAN DEFAULT FALSE  -- Compte premium
```
**🎯 Cas d'usage** :
- **Drapeaux de statut** (actif, vérifié, publié)
- Permissions (peut_editer, peut_voir)
- États binaires simples

### BIT(n)
**Stockage de bits** - n bits (1 à 64)
```sql
-- Exemples d'usage  
permissions BIT(8),           -- 8 permissions différentes
feature_flags BIT(16),        -- Drapeaux de fonctionnalités
status_bits BIT(4)           -- 4 statuts combinés
```
**🎯 Cas d'usage** :
- **Permissions multiples** en un champ
- Drapeaux de fonctionnalités
- Optimisation d'espace pour booléens multiples

---

## 💾 Types Binaires et Objets

### BINARY(n) / VARBINARY(n)
**Données binaires** fixes ou variables
```sql
-- Exemples d'usage
hash_value BINARY(32),        -- Hash SHA-256
file_signature VARBINARY(255), -- Signatures de fichiers
encrypted_data VARBINARY(500) -- Données chiffrées
```
**🎯 Cas d'usage** :
- Hashes, signatures cryptographiques
- Données chiffrées courtes
- Identifiants binaires

### BLOB Types
**Stockage d'objets binaires volumineux**

#### TINYBLOB - jusqu'à 255 bytes
```sql
small_icon TINYBLOB          -- Petites icônes
```

#### BLOB - jusqu'à 65KB  
```sql
profile_picture BLOB,        -- Photos de profil
document_thumb BLOB         -- Miniatures documents
```

#### MEDIUMBLOB - jusqu'à 16MB
```sql  
audio_file MEDIUMBLOB,      -- Fichiers audio courts
presentation MEDIUMBLOB     -- Présentations
```

#### LONGBLOB - jusqu'à 4GB
```sql
video_content LONGBLOB,     -- Fichiers vidéo
backup_archive LONGBLOB    -- Archives complètes
```

**🎯 Cas d'usage** :
- **⚠️ Usage déconseillé** - préférer stockage fichier
- Petits fichiers intégrés (icônes, signatures)
- Systèmes sans accès système de fichiers

---

## 🎨 Types Spécialisés

### JSON (MySQL 5.7+, PostgreSQL 9.3+)
**Stockage et requêtage JSON natif**
```sql
-- Exemples d'usage
user_preferences JSON,       -- Préférences utilisateur
product_specs JSON,         -- Spécifications produit  
api_response JSON,          -- Réponses API
metadata JSON              -- Métadonnées flexibles
```

```sql
-- Requêtes JSON
SELECT JSON_EXTRACT(user_preferences, '$.theme') as theme
FROM users;

-- Mise à jour JSON  
UPDATE products 
SET product_specs = JSON_SET(product_specs, '$.color', 'red')
WHERE id = 1;
```

**🎯 Cas d'usage** :
- **Configuration utilisateur flexible**
- Métadonnées variables
- APIs REST (stockage réponses)
- Schémas évolutifs

### ENUM
**Liste de valeurs prédéfinies**
```sql
-- Exemples d'usage
status ENUM('draft', 'published', 'archived') DEFAULT 'draft',
priority ENUM('low', 'medium', 'high', 'urgent') DEFAULT 'medium',
size ENUM('XS', 'S', 'M', 'L', 'XL', 'XXL'),
gender ENUM('male', 'female', 'other', 'prefer_not_to_say')
```

**🎯 Cas d'usage** :
- **Statuts fixes** avec valeurs limitées
- Tailles, couleurs prédéfinies
- Classifications fermées
- **⚠️ Difficile à modifier** - préférer tables de référence

### SET (MySQL)
**Ensemble de valeurs multiples**
```sql
-- Exemples d'usage
skills SET('php', 'javascript', 'python', 'java', 'react'),
permissions SET('read', 'write', 'delete', 'admin'),
features SET('ssl', 'backup', 'cdn', 'analytics')
```

**🎯 Cas d'usage** :
- Compétences multiples
- Permissions combinées
- Fonctionnalités activées

---

## 🎯 Guide de Choix par Cas d'Usage

### 💰 Données Financières
```sql
-- ✅ OBLIGATOIRE : DECIMAL pour éviter erreurs d'arrondi
price DECIMAL(10,2),          -- Prix jusqu'à 99,999,999.99
tax_rate DECIMAL(5,4),        -- Taux : 0.1975 (19.75%)
account_balance DECIMAL(15,2) -- Soldes comptes
```

### 👤 Données Utilisateur
```sql
-- Profil utilisateur type
user_id INT AUTO_INCREMENT PRIMARY KEY,
username VARCHAR(50) UNIQUE NOT NULL,
email VARCHAR(320) UNIQUE NOT NULL,    -- RFC 5321 max length
password_hash VARCHAR(255),            -- Hashes bcrypt/argon2
first_name VARCHAR(100),
last_name VARCHAR(100), 
birth_date DATE,
is_active BOOLEAN DEFAULT TRUE,
created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
updated_at DATETIME ON UPDATE CURRENT_TIMESTAMP
```

### 🛍️ E-commerce
```sql
-- Produit e-commerce
product_id INT AUTO_INCREMENT PRIMARY KEY,
sku VARCHAR(100) UNIQUE,               -- SKU unique
name VARCHAR(255) NOT NULL,
description TEXT,
price DECIMAL(10,2) NOT NULL,
stock_quantity INT UNSIGNED DEFAULT 0,
weight_kg DECIMAL(8,3),               -- Poids en kg
is_active BOOLEAN DEFAULT TRUE,
category_id INT,
created_at DATETIME DEFAULT CURRENT_TIMESTAMP
```

### 📊 Analytics et Logs
```sql
-- Event tracking
event_id BIGINT AUTO_INCREMENT PRIMARY KEY,  -- Gros volume
user_id INT,
event_type VARCHAR(50),
timestamp_ms BIGINT,                   -- Timestamp précis
ip_address VARCHAR(45),                -- IPv6 compatible
user_agent TEXT,                       -- User agents longs
metadata JSON,                         -- Données flexibles
created_at DATETIME DEFAULT CURRENT_TIMESTAMP
```

### 🏢 Système d'Entreprise
```sql
-- Employé entreprise  
employee_id INT AUTO_INCREMENT PRIMARY KEY,
employee_number VARCHAR(20) UNIQUE,    -- Numéro employé
first_name VARCHAR(100) NOT NULL,
last_name VARCHAR(100) NOT NULL,
email VARCHAR(320) UNIQUE,
department_id SMALLINT,                -- Peu de départements
salary DECIMAL(12,2),                  -- Salaire précis
hire_date DATE,
is_manager BOOLEAN DEFAULT FALSE,
permissions SET('read', 'write', 'admin', 'hr'),
status ENUM('active', 'inactive', 'terminated') DEFAULT 'active'
```

---

## ⚡ Conseils de Performance

### 🎯 Optimisation par Type

#### Entiers
- **TINYINT** pour booléens et petites listes
- **INT** pour clés primaires standard  
- **BIGINT** seulement si nécessaire (gros volume)
- **UNSIGNED** quand les valeurs négatives sont impossibles

#### Texte
- **VARCHAR(n)** avec n approprié (ni trop petit, ni trop grand)
- **CHAR(n)** pour longueur fixe garantie
- **TEXT** seulement pour contenu vraiment long
- **Éviter LONGTEXT** sauf cas exceptionnels

#### Dates
- **DATE** pour dates seules
- **DATETIME** pour horodatage complet
- **TIMESTAMP** pour applications multi-timezone
- **Indexer les colonnes de date** fréquemment filtrées

### 📈 Bonnes Pratiques

#### Choix de Taille
```sql
-- ❌ Mauvais : trop large
user_id BIGINT,              -- INT suffit dans la plupart des cas
username VARCHAR(1000),      -- VARCHAR(50) suffit

-- ✅ Bon : taille appropriée  
user_id INT AUTO_INCREMENT,
username VARCHAR(50),
email VARCHAR(320)           -- Taille max email RFC
```

#### Index et Performance
```sql
-- ✅ Index sur colonnes fréquemment filtrées
CREATE INDEX idx_created_at ON orders(created_at);
CREATE INDEX idx_status_user ON orders(status, user_id);

-- ✅ Clés composites dans le bon ordre
CREATE INDEX idx_user_date ON logs(user_id, created_at);
```

#### Valeurs par Défaut
```sql
-- ✅ Valeurs par défaut appropriées
created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
is_active BOOLEAN DEFAULT TRUE,
status ENUM('draft', 'published') DEFAULT 'draft',
priority TINYINT DEFAULT 0
```

---

## 🔄 Migration et Évolution

### Changement de Type Sécurisé
```sql
-- ✅ Extension de taille (safe)
ALTER TABLE users MODIFY COLUMN username VARCHAR(100);

-- ⚠️ Réduction de taille (vérifier d'abord)
-- Vérifier les données existantes avant :
SELECT MAX(LENGTH(username)) FROM users;
ALTER TABLE users MODIFY COLUMN username VARCHAR(50);

-- ⚠️ Changement de type (peut perdre données)
ALTER TABLE products MODIFY COLUMN price DECIMAL(12,2);
```

### Stratégie de Migration
1. **Analyser** les données existantes
2. **Tester** sur environnement de développement
3. **Sauvegarder** avant migration production
4. **Monitorer** après changement

---

## 📚 Compatibilité SGBD

| Type | MySQL | PostgreSQL | SQL Server | Oracle |
|------|-------|------------|------------|---------|
| INT | ✅ | INTEGER | INT | NUMBER |
| VARCHAR(n) | ✅ | ✅ | ✅ | VARCHAR2(n) |
| TEXT | ✅ | ✅ | NVARCHAR(MAX) | CLOB |
| DECIMAL(p,s) | ✅ | NUMERIC(p,s) | DECIMAL(p,s) | NUMBER(p,s) |
| DATETIME | ✅ | TIMESTAMP | DATETIME2 | DATE |
| BOOLEAN | ✅ | ✅ | BIT | NUMBER(1) |
| JSON | ✅ | ✅ | NVARCHAR(MAX) | JSON* |

**Note** : Consultez la documentation spécifique de votre SGBD pour les fonctionnalités avancées et les différences de comportement.

---

*Cette documentation couvre les types de données les plus utilisés. Pour des besoins spécifiques, référez-vous à la documentation officielle de votre SGBD.*