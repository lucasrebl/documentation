# 🗃️ SQL - Guide Complet des Commandes

Une documentation exhaustive des commandes SQL avec des exemples pratiques pour la gestion de bases de données.

![SQL](https://img.shields.io/badge/SQL-Database-blue?style=flat-square&logo=postgresql&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=flat-square&logo=postgresql&logoColor=white)

## 📖 Description

SQL (Structured Query Language) est un langage de programmation conçu pour :
- Gérer et manipuler des bases de données relationnelles
- Créer, modifier et supprimer des structures de données
- Insérer, mettre à jour et récupérer des données
- Contrôler l'accès et les permissions
- Optimiser les performances des requêtes

## 🏗️ DDL - Data Definition Language

### Gestion des bases de données
```sql
CREATE DATABASE ma_base;
```
*Crée une nouvelle base de données*

```sql
DROP DATABASE ma_base;
```
*Supprime une base de données existante*

```sql
USE ma_base;
```
*Sélectionne une base de données pour utilisation*

```sql
SHOW DATABASES;
```
*Affiche toutes les bases de données*

### Création de tables
```sql
CREATE TABLE utilisateurs (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nom VARCHAR(100) NOT NULL,
    email VARCHAR(255) UNIQUE,
    age INT,
    date_creation TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
*Crée une table avec contraintes*

```sql
CREATE TABLE IF NOT EXISTS produits (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nom VARCHAR(200) NOT NULL,
    prix DECIMAL(10,2),
    stock INT DEFAULT 0
);
```
*Crée une table seulement si elle n'existe pas*

### Modification de tables
```sql
ALTER TABLE utilisateurs ADD COLUMN telephone VARCHAR(15);
```
*Ajoute une nouvelle colonne*

```sql
ALTER TABLE utilisateurs DROP COLUMN age;
```
*Supprime une colonne*

```sql
ALTER TABLE utilisateurs MODIFY COLUMN nom VARCHAR(150);
```
*Modifie le type d'une colonne*

```sql
ALTER TABLE utilisateurs RENAME COLUMN nom TO nom_complet;
```
*Renomme une colonne*

```sql
ALTER TABLE utilisateurs RENAME TO users;
```
*Renomme une table*

### Suppression de tables
```sql
DROP TABLE utilisateurs;
```
*Supprime une table*

```sql
DROP TABLE IF EXISTS utilisateurs;
```
*Supprime une table si elle existe*

```sql
TRUNCATE TABLE utilisateurs;
```
*Vide une table (plus rapide que DELETE)*

### Index
```sql
CREATE INDEX idx_email ON utilisateurs(email);
```
*Crée un index simple*

```sql
CREATE UNIQUE INDEX idx_unique_email ON utilisateurs(email);
```
*Crée un index unique*

```sql
CREATE INDEX idx_composite ON utilisateurs(nom, email);
```
*Crée un index composite*

```sql
DROP INDEX idx_email ON utilisateurs;
```
*Supprime un index*

### Contraintes
```sql
ALTER TABLE utilisateurs ADD CONSTRAINT ck_age CHECK (age >= 0);
```
*Ajoute une contrainte de vérification*

```sql
ALTER TABLE commandes ADD CONSTRAINT fk_user 
FOREIGN KEY (user_id) REFERENCES utilisateurs(id);
```
*Ajoute une clé étrangère*

```sql
ALTER TABLE utilisateurs DROP CONSTRAINT ck_age;
```
*Supprime une contrainte*

## 📊 DML - Data Manipulation Language

### Insertion de données
```sql
INSERT INTO utilisateurs (nom, email, age) 
VALUES ('Jean Dupont', 'jean@email.com', 30);
```
*Insère un enregistrement*

```sql
INSERT INTO utilisateurs (nom, email, age) VALUES 
('Marie Martin', 'marie@email.com', 25),
('Pierre Durand', 'pierre@email.com', 35),
('Sophie Moreau', 'sophie@email.com', 28);
```
*Insère plusieurs enregistrements*

```sql
INSERT INTO utilisateurs_backup 
SELECT * FROM utilisateurs WHERE age > 25;
```
*Insère à partir d'une requête SELECT*

### Mise à jour de données
```sql
UPDATE utilisateurs SET age = 31 WHERE id = 1;
```
*Met à jour un enregistrement spécifique*

```sql
UPDATE utilisateurs SET age = age + 1;
```
*Met à jour tous les enregistrements*

```sql
UPDATE utilisateurs 
SET nom = 'Jean-Pierre Dupont', email = 'jp@email.com' 
WHERE id = 1;
```
*Met à jour plusieurs colonnes*

```sql
UPDATE produits 
SET prix = prix * 1.1 
WHERE categorie = 'Electronique';
```
*Met à jour avec calcul*

### Suppression de données
```sql
DELETE FROM utilisateurs WHERE id = 1;
```
*Supprime un enregistrement spécifique*

```sql
DELETE FROM utilisateurs WHERE age < 18;
```
*Supprime selon une condition*

```sql
DELETE FROM utilisateurs;
```
*Supprime tous les enregistrements*

## 🔍 DQL - Data Query Language

### Sélection de base
```sql
SELECT * FROM utilisateurs;
```
*Sélectionne toutes les colonnes*

```sql
SELECT nom, email FROM utilisateurs;
```
*Sélectionne des colonnes spécifiques*

```sql
SELECT DISTINCT age FROM utilisateurs;
```
*Sélectionne les valeurs uniques*

```sql
SELECT nom AS nom_utilisateur, age AS 'Âge' FROM utilisateurs;
```
*Utilise des alias*

### Conditions WHERE
```sql
SELECT * FROM utilisateurs WHERE age > 25;
```
*Condition simple*

```sql
SELECT * FROM utilisateurs WHERE age BETWEEN 20 AND 40;
```
*Condition BETWEEN*

```sql
SELECT * FROM utilisateurs WHERE nom IN ('Jean', 'Marie', 'Pierre');
```
*Condition IN*

```sql
SELECT * FROM utilisateurs WHERE nom LIKE 'Jean%';
```
*Recherche avec motifs (commence par "Jean")*

```sql
SELECT * FROM utilisateurs WHERE nom LIKE '%martin%';
```
*Contient "martin"*

```sql
SELECT * FROM utilisateurs WHERE email IS NOT NULL;
```
*Vérification de NULL*

```sql
SELECT * FROM utilisateurs 
WHERE age > 25 AND (nom LIKE 'Jean%' OR nom LIKE 'Marie%');
```
*Conditions complexes*

### Tri et limitation
```sql
SELECT * FROM utilisateurs ORDER BY age;
```
*Tri croissant*

```sql
SELECT * FROM utilisateurs ORDER BY age DESC;
```
*Tri décroissant*

```sql
SELECT * FROM utilisateurs ORDER BY nom, age DESC;
```
*Tri multiple*

```sql
SELECT * FROM utilisateurs LIMIT 10;
```
*Limite le nombre de résultats*

```sql
SELECT * FROM utilisateurs LIMIT 10 OFFSET 20;
```
*Pagination (MySQL/PostgreSQL)*

```sql
SELECT TOP 10 * FROM utilisateurs;
```
*Limite (SQL Server)*

### Fonctions d'agrégation
```sql
SELECT COUNT(*) FROM utilisateurs;
```
*Compte le nombre d'enregistrements*

```sql
SELECT COUNT(DISTINCT age) FROM utilisateurs;
```
*Compte les valeurs uniques*

```sql
SELECT AVG(age) AS age_moyen FROM utilisateurs;
```
*Calcule la moyenne*

```sql
SELECT MIN(age), MAX(age) FROM utilisateurs;
```
*Valeurs minimale et maximale*

```sql
SELECT SUM(prix) FROM produits;
```
*Somme des valeurs*

### Regroupement
```sql
SELECT age, COUNT(*) 
FROM utilisateurs 
GROUP BY age;
```
*Regroupement simple*

```sql
SELECT age, COUNT(*) as nombre
FROM utilisateurs 
GROUP BY age 
HAVING COUNT(*) > 1;
```
*Regroupement avec condition HAVING*

```sql
SELECT YEAR(date_creation) as annee, COUNT(*) as nb_users
FROM utilisateurs 
GROUP BY YEAR(date_creation)
ORDER BY annee DESC;
```
*Regroupement par année*

## 🔗 Jointures

### Tables d'exemple
```sql
-- Table users
CREATE TABLE users (
    id INT PRIMARY KEY,
    nom VARCHAR(100),
    email VARCHAR(255)
);

-- Table orders
CREATE TABLE orders (
    id INT PRIMARY KEY,
    user_id INT,
    produit VARCHAR(100),
    prix DECIMAL(10,2),
    date_commande DATE
);

-- Table categories
CREATE TABLE categories (
    id INT PRIMARY KEY,
    nom VARCHAR(100)
);

-- Table products
CREATE TABLE products (
    id INT PRIMARY KEY,
    nom VARCHAR(100),
    category_id INT,
    prix DECIMAL(10,2)
);
```

### INNER JOIN
```sql
SELECT u.nom, o.produit, o.prix
FROM users u
INNER JOIN orders o ON u.id = o.user_id;
```
*Retourne uniquement les utilisateurs qui ont des commandes*

```sql
SELECT u.nom, COUNT(o.id) as nb_commandes, SUM(o.prix) as total
FROM users u
INNER JOIN orders o ON u.id = o.user_id
GROUP BY u.id, u.nom;
```
*Jointure avec agrégation*

### LEFT JOIN
```sql
SELECT u.nom, o.produit, o.prix
FROM users u
LEFT JOIN orders o ON u.id = o.user_id;
```
*Retourne tous les utilisateurs, même sans commandes*

```sql
SELECT u.nom, COALESCE(COUNT(o.id), 0) as nb_commandes
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
GROUP BY u.id, u.nom;
```
*Compte les commandes, 0 si aucune*

### RIGHT JOIN
```sql
SELECT u.nom, o.produit, o.prix
FROM users u
RIGHT JOIN orders o ON u.id = o.user_id;
```
*Retourne toutes les commandes, même sans utilisateur*

### FULL OUTER JOIN
```sql
SELECT u.nom, o.produit
FROM users u
FULL OUTER JOIN orders o ON u.id = o.user_id;
```
*Retourne tous les utilisateurs et toutes les commandes*

### CROSS JOIN
```sql
SELECT u.nom, p.nom as produit
FROM users u
CROSS JOIN products p;
```
*Produit cartésien (toutes les combinaisons)*

### Jointures multiples
```sql
SELECT 
    u.nom as utilisateur,
    p.nom as produit,
    c.nom as categorie,
    o.prix,
    o.date_commande
FROM users u
INNER JOIN orders o ON u.id = o.user_id
INNER JOIN products p ON o.produit = p.nom
INNER JOIN categories c ON p.category_id = c.id
WHERE o.date_commande > '2024-01-01';
```
*Jointure de 4 tables*

### Auto-jointure
```sql
-- Table employees avec manager_id
SELECT 
    e1.nom as employe,
    e2.nom as manager
FROM employees e1
LEFT JOIN employees e2 ON e1.manager_id = e2.id;
```
*Jointure d'une table avec elle-même*

## 🔄 Sous-requêtes

### Sous-requête dans WHERE
```sql
SELECT nom, age 
FROM utilisateurs 
WHERE age > (SELECT AVG(age) FROM utilisateurs);
```
*Utilisateurs plus âgés que la moyenne*

```sql
SELECT nom 
FROM utilisateurs 
WHERE id IN (
    SELECT user_id 
    FROM orders 
    WHERE prix > 100
);
```
*Utilisateurs avec des commandes > 100€*

### Sous-requête corrélée
```sql
SELECT u.nom, u.email
FROM users u
WHERE EXISTS (
    SELECT 1 
    FROM orders o 
    WHERE o.user_id = u.id AND o.prix > 50
);
```
*Utilisateurs avec au moins une commande > 50€*

```sql
SELECT u.nom,
    (SELECT COUNT(*) FROM orders o WHERE o.user_id = u.id) as nb_commandes
FROM users u;
```
*Nombre de commandes par utilisateur*

### Sous-requête avec ANY/ALL
```sql
SELECT nom, prix
FROM products
WHERE prix > ANY (
    SELECT prix 
    FROM orders 
    WHERE date_commande > '2024-01-01'
);
```
*Produits plus chers que n'importe quelle commande récente*

```sql
SELECT nom, prix
FROM products
WHERE prix > ALL (
    SELECT prix 
    FROM orders 
    WHERE user_id = 1
);
```
*Produits plus chers que toutes les commandes de l'utilisateur 1*

## 🔧 Fonctions Avancées

### Fonctions de chaîne
```sql
SELECT 
    CONCAT(nom, ' - ', email) as info,
    UPPER(nom) as nom_majuscule,
    LENGTH(nom) as longueur_nom,
    SUBSTRING(email, 1, POSITION('@' IN email) - 1) as username
FROM utilisateurs;
```
*Manipulation de chaînes*

```sql
SELECT 
    REPLACE(nom, 'Jean', 'John') as nom_anglais,
    TRIM(nom) as nom_propre,
    LEFT(nom, 3) as initiales
FROM utilisateurs;
```
*Plus de fonctions de chaîne*

### Fonctions de date
```sql
SELECT 
    nom,
    date_creation,
    YEAR(date_creation) as annee,
    MONTH(date_creation) as mois,
    DAYOFWEEK(date_creation) as jour_semaine,
    DATEDIFF(CURRENT_DATE, date_creation) as jours_depuis_creation
FROM utilisateurs;
```
*Manipulation de dates*

```sql
SELECT 
    COUNT(*) as total,
    DATE_FORMAT(date_creation, '%Y-%m') as mois_annee
FROM utilisateurs
GROUP BY DATE_FORMAT(date_creation, '%Y-%m')
ORDER BY mois_annee;
```
*Regroupement par mois*

### Fonctions conditionnelles
```sql
SELECT 
    nom,
    age,
    CASE 
        WHEN age < 18 THEN 'Mineur'
        WHEN age < 65 THEN 'Adulte'
        ELSE 'Senior'
    END as categorie_age
FROM utilisateurs;
```
*Expression CASE*

```sql
SELECT 
    nom,
    COALESCE(telephone, 'Non renseigné') as tel,
    NULLIF(age, 0) as age_valide
FROM utilisateurs;
```
*Gestion des valeurs NULL*

### Fonctions de fenêtrage (Window Functions)
```sql
SELECT 
    nom,
    age,
    ROW_NUMBER() OVER (ORDER BY age) as rang,
    RANK() OVER (ORDER BY age) as rang_ex_aequo,
    DENSE_RANK() OVER (ORDER BY age) as rang_dense
FROM utilisateurs;
```
*Fonctions de classement*

```sql
SELECT 
    nom,
    age,
    AVG(age) OVER () as age_moyen_global,
    AVG(age) OVER (PARTITION BY YEAR(date_creation)) as age_moyen_annee
FROM utilisateurs;
```
*Moyennes avec fenêtrage*

```sql
SELECT 
    nom,
    age,
    LAG(age, 1) OVER (ORDER BY date_creation) as age_precedent,
    LEAD(age, 1) OVER (ORDER BY date_creation) as age_suivant
FROM utilisateurs;
```
*Accès aux lignes précédentes/suivantes*

## 🔐 DCL - Data Control Language

### Gestion des utilisateurs
```sql
CREATE USER 'nouveau_user'@'localhost' IDENTIFIED BY 'mot_de_passe';
```
*Crée un nouvel utilisateur*

```sql
DROP USER 'ancien_user'@'localhost';
```
*Supprime un utilisateur*

```sql
ALTER USER 'user'@'localhost' IDENTIFIED BY 'nouveau_mot_de_passe';
```
*Change le mot de passe*

### Gestion des permissions
```sql
GRANT SELECT ON ma_base.* TO 'user'@'localhost';
```
*Accorde le droit de lecture*

```sql
GRANT INSERT, UPDATE, DELETE ON ma_base.utilisateurs TO 'user'@'localhost';
```
*Accorde des droits spécifiques*

```sql
GRANT ALL PRIVILEGES ON ma_base.* TO 'admin'@'localhost';
```
*Accorde tous les droits*

```sql
REVOKE DELETE ON ma_base.utilisateurs FROM 'user'@'localhost';
```
*Retire un droit*

```sql
SHOW GRANTS FOR 'user'@'localhost';
```
*Affiche les permissions d'un utilisateur*

## 🔄 Transactions

### Gestion des transactions
```sql
START TRANSACTION;

UPDATE comptes SET solde = solde - 100 WHERE id = 1;
UPDATE comptes SET solde = solde + 100 WHERE id = 2;

COMMIT;
```
*Transaction réussie*

```sql
START TRANSACTION;

UPDATE produits SET stock = stock - 1 WHERE id = 1;

IF (SELECT stock FROM produits WHERE id = 1) < 0 THEN
    ROLLBACK;
ELSE
    COMMIT;
END IF;
```
*Transaction avec vérification*

```sql
SET AUTOCOMMIT = 0;
-- Vos requêtes
COMMIT;
SET AUTOCOMMIT = 1;
```
*Désactive l'auto-commit*

### Points de sauvegarde
```sql
START TRANSACTION;

INSERT INTO logs VALUES ('Début opération');
SAVEPOINT sp1;

UPDATE comptes SET solde = solde - 50 WHERE id = 1;
SAVEPOINT sp2;

UPDATE comptes SET solde = solde + 50 WHERE id = 2;

-- En cas d'erreur, retour au point sp2
ROLLBACK TO sp2;

COMMIT;
```
*Utilisation des savepoints*

## 📊 Optimisation et Performance

### Analyse des requêtes
```sql
EXPLAIN SELECT * FROM utilisateurs WHERE age > 25;
```
*Analyse le plan d'exécution*

```sql
EXPLAIN ANALYZE 
SELECT u.nom, COUNT(o.id) 
FROM utilisateurs u 
LEFT JOIN commandes o ON u.id = o.user_id 
GROUP BY u.nom;
```
*Analyse avec statistiques d'exécution*

### Optimisation des index
```sql
-- Index sur colonne fréquemment recherchée
CREATE INDEX idx_age ON utilisateurs(age);

-- Index composite pour requêtes multi-colonnes
CREATE INDEX idx_nom_age ON utilisateurs(nom, age);

-- Index partiel (PostgreSQL)
CREATE INDEX idx_actifs ON utilisateurs(nom) WHERE actif = true;
```
*Stratégies d'indexation*

### Requêtes optimisées
```sql
-- Éviter SELECT *
SELECT nom, email FROM utilisateurs WHERE id = 1;

-- Utiliser LIMIT pour limiter les résultats
SELECT nom FROM utilisateurs ORDER BY date_creation DESC LIMIT 10;

-- Utiliser EXISTS plutôt qu'IN pour de gros volumes
SELECT u.nom 
FROM users u 
WHERE EXISTS (
    SELECT 1 FROM orders o WHERE o.user_id = u.id
);
```
*Bonnes pratiques*

## 🎯 CTE (Common Table Expressions)

### CTE Simple
```sql
WITH utilisateurs_actifs AS (
    SELECT nom, email, age 
    FROM utilisateurs 
    WHERE derniere_connexion > DATE_SUB(NOW(), INTERVAL 30 DAY)
)
SELECT * FROM utilisateurs_actifs WHERE age > 25;
```
*CTE basique*

### CTE Récursive
```sql
WITH RECURSIVE hierarchie AS (
    -- Cas de base
    SELECT id, nom, manager_id, 0 as niveau
    FROM employes 
    WHERE manager_id IS NULL
    
    UNION ALL
    
    -- Cas récursif
    SELECT e.id, e.nom, e.manager_id, h.niveau + 1
    FROM employes e
    INNER JOIN hierarchie h ON e.manager_id = h.id
)
SELECT * FROM hierarchie ORDER BY niveau, nom;
```
*CTE récursive pour hiérarchie*

### CTE Multiple
```sql
WITH 
commandes_2024 AS (
    SELECT user_id, SUM(prix) as total
    FROM orders
    WHERE YEAR(date_commande) = 2024
    GROUP BY user_id
),
top_clients AS (
    SELECT user_id, total
    FROM commandes_2024
    WHERE total > 1000
)
SELECT u.nom, tc.total
FROM users u
INNER JOIN top_clients tc ON u.id = tc.user_id;
```
*CTE multiples*

## 🔄 Requêtes Avancées Pratiques

### Calcul de rang et percentiles
```sql
SELECT 
    nom,
    age,
    NTILE(4) OVER (ORDER BY age) as quartile,
    PERCENT_RANK() OVER (ORDER BY age) as percentile,
    CUME_DIST() OVER (ORDER BY age) as distribution_cumulative
FROM utilisateurs;
```
*Statistiques avancées*

### Pivot et Unpivot
```sql
-- Pivot (transformation colonnes en lignes)
SELECT 
    YEAR(date_commande) as annee,
    SUM(CASE WHEN MONTH(date_commande) = 1 THEN prix END) as janvier,
    SUM(CASE WHEN MONTH(date_commande) = 2 THEN prix END) as fevrier,
    SUM(CASE WHEN MONTH(date_commande) = 3 THEN prix END) as mars
FROM orders
GROUP BY YEAR(date_commande);
```
*Transformation pivot manuelle*

### Détection de doublons
```sql
-- Trouver les doublons
SELECT email, COUNT(*) as nb_occurrences
FROM utilisateurs
GROUP BY email
HAVING COUNT(*) > 1;

-- Supprimer les doublons (garder le plus récent)
DELETE u1 FROM utilisateurs u1
INNER JOIN utilisateurs u2
WHERE u1.id < u2.id AND u1.email = u2.email;
```
*Gestion des doublons*

### Requêtes de comparaison temporelle
```sql
WITH ventes_mensuelles AS (
    SELECT 
        DATE_FORMAT(date_commande, '%Y-%m') as mois,
        SUM(prix) as total
    FROM orders
    GROUP BY DATE_FORMAT(date_commande, '%Y-%m')
)
SELECT 
    mois,
    total,
    LAG(total, 1) OVER (ORDER BY mois) as mois_precedent,
    total - LAG(total, 1) OVER (ORDER BY mois) as difference,
    ROUND(
        (total - LAG(total, 1) OVER (ORDER BY mois)) / 
        LAG(total, 1) OVER (ORDER BY mois) * 100, 2
    ) as pourcentage_evolution
FROM ventes_mensuelles;
```
*Analyse de l'évolution temporelle*

## ⚡ Bonnes Pratiques et Optimisation

### Règles de performance
1. **Index appropriés** : Créez des index sur les colonnes de recherche fréquente
2. **Évitez SELECT *** : Sélectionnez uniquement les colonnes nécessaires
3. **Utilisez LIMIT** : Limitez les résultats quand c'est possible
4. **Optimisez les JOIN** : Préférez INNER JOIN à LEFT JOIN quand possible
5. **Évitez les sous-requêtes** : Préférez les JOIN aux sous-requêtes
6. **Utilisez EXPLAIN** : Analysez vos requêtes avant la mise en production

### Conventions de nommage
```sql
-- Tables : pluriel, minuscules
CREATE TABLE utilisateurs (...);
CREATE TABLE commandes (...);

-- Colonnes : descriptives, minuscules
nom_utilisateur, date_creation, prix_unitaire

-- Index : préfixe + table + colonnes
idx_utilisateurs_email, idx_commandes_date_user

-- Contraintes : préfixe + table + type
pk_utilisateurs, fk_commandes_user, ck_age_positive
```

### Sécurité
```sql
-- Utilisez des requêtes préparées (dans votre application)
PREPARE stmt FROM 'SELECT * FROM utilisateurs WHERE id = ?';
SET @user_id = 1;
EXECUTE stmt USING @user_id;

-- Échappez les valeurs utilisateur
-- Accordez uniquement les permissions nécessaires
-- Utilisez des connexions sécurisées (SSL/TLS)
```

## 🆘 Requêtes de Maintenance

### Sauvegarde et restauration
```sql
-- Sauvegarde (commande système)
mysqldump -u root -p ma_base > sauvegarde.sql

-- Restauration
mysql -u root -p ma_base < sauvegarde.sql

-- Sauvegarde d'une table
mysqldump -u root -p ma_base ma_table > table_backup.sql
```

### Statistiques de base
```sql
-- Taille des tables
SELECT 
    table_name,
    ROUND(((data_length + index_length) / 1024 / 1024), 2) AS 'Taille (MB)'
FROM information_schema.TABLES
WHERE table_schema = 'ma_base'
ORDER BY (data_length + index_length) DESC;

-- Nombre d'enregistrements par table
SELECT 
    table_name,
    table_rows
FROM information_schema.TABLES
WHERE table_schema = 'ma_base';
```

### Maintenance des index
```sql
-- Reconstruction des index (MySQL)
ALTER TABLE ma_table ENGINE=InnoDB;

-- Analyse des statistiques
ANALYZE TABLE ma_table;

-- Vérification de l'intégrité
CHECK TABLE ma_table;

-- Réparation si nécessaire
REPAIR TABLE ma_table;
```

---
*Cette documentation couvre les aspects essentiels de SQL. Pour des fonctionnalités spécifiques à votre SGBD (MySQL, PostgreSQL, SQL Server, etc.), consultez la documentation officielle.*
