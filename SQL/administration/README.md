# 🔐 SQL Administration - Gestion et Maintenance

Documentation pour l'administration des bases de données : utilisateurs, transactions et maintenance.

![SQL](https://img.shields.io/badge/SQL-Admin-red?style=flat-square&logo=postgresql&logoColor=white)

## 🔐 DCL - Data Control Language

**Le DCL (Data Control Language)** gère les permissions et l'accès aux données. Il permet de créer des utilisateurs, d'attribuer ou de révoquer des droits d'accès, et de contrôler qui peut faire quoi dans la base de données. C'est essentiel pour la sécurité.

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

**Les transactions** garantissent l'intégrité des données en regroupant plusieurs opérations en une unité atomique. Soit toutes les opérations réussissent (COMMIT), soit aucune n'est appliquée (ROLLBACK). Elles respectent les propriétés ACID : Atomicité, Cohérence, Isolation, Durabilité.

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

## 🔍 Monitoring et Diagnostic

### Processus en cours
```sql
-- MySQL
SHOW PROCESSLIST;

-- PostgreSQL
SELECT * FROM pg_stat_activity;

-- SQL Server
SELECT * FROM sys.dm_exec_requests;
```

### Verrous et blocages
```sql
-- MySQL - Voir les verrous
SHOW ENGINE INNODB STATUS;

-- PostgreSQL - Voir les verrous
SELECT * FROM pg_locks;

-- Tuer une requête bloquante (MySQL)
KILL QUERY process_id;
```

### Performance des requêtes
```sql
-- MySQL - Requêtes lentes
SHOW VARIABLES LIKE 'slow_query_log';
SET GLOBAL slow_query_log = 'ON';

-- PostgreSQL - Statistiques des requêtes
SELECT query, calls, total_time, mean_time
FROM pg_stat_statements
ORDER BY total_time DESC
LIMIT 10;
```

## ⚙️ Configuration et Optimisation

### Variables système importantes
```sql
-- MySQL
SHOW VARIABLES LIKE 'innodb_buffer_pool_size';
SHOW VARIABLES LIKE 'max_connections';
SHOW VARIABLES LIKE 'query_cache_size';

-- Modification temporaire
SET SESSION sort_buffer_size = 1048576;

-- Modification globale
SET GLOBAL max_connections = 200;
```

### Analyse de performance
```sql
-- Statistiques des index (MySQL)
SELECT 
    table_schema,
    table_name,
    index_name,
    cardinality
FROM information_schema.statistics
WHERE table_schema = 'ma_base'
ORDER BY cardinality DESC;

-- Index non utilisés (PostgreSQL)
SELECT 
    schemaname,
    tablename,
    indexname,
    idx_tup_read,
    idx_tup_fetch
FROM pg_stat_user_indexes
WHERE idx_tup_read = 0;
```

## 🛡️ Sécurité et Bonnes Pratiques

### Sécurisation des accès
```sql
-- Créer un utilisateur avec droits limités
CREATE USER 'app_user'@'%' IDENTIFIED BY 'strong_password';
GRANT SELECT, INSERT, UPDATE ON myapp.* TO 'app_user'@'%';

-- Utilisateur en lecture seule
CREATE USER 'readonly'@'%' IDENTIFIED BY 'readonly_pass';
GRANT SELECT ON myapp.* TO 'readonly'@'%';

-- Révoquer les permissions par défaut
REVOKE ALL ON *.* FROM 'app_user'@'%';
```

### Audit et logging
```sql
-- Activer l'audit général (MySQL)
SET GLOBAL general_log = 'ON';
SET GLOBAL general_log_file = '/var/log/mysql/general.log';

-- Log des requêtes de modification uniquement
SET GLOBAL log_output = 'TABLE';
SET GLOBAL general_log = 'ON';
```

### Chiffrement et SSL
```sql
-- Vérifier le support SSL
SHOW VARIABLES LIKE 'have_ssl';

-- Créer un utilisateur nécessitant SSL
CREATE USER 'secure_user'@'%' 
IDENTIFIED BY 'password' 
REQUIRE SSL;

-- Connexion avec certificat client
CREATE USER 'cert_user'@'%'
IDENTIFIED BY 'password'
REQUIRE X509;
```

## 📊 Scripts d'Administration Utiles

### Nettoyage automatique
```sql
-- Supprimer les logs anciens
DELETE FROM logs WHERE date_creation < DATE_SUB(NOW(), INTERVAL 90 DAY);

-- Archiver les données anciennes
INSERT INTO commandes_archive 
SELECT * FROM commandes 
WHERE date_commande < DATE_SUB(NOW(), INTERVAL 1 YEAR);

DELETE FROM commandes 
WHERE date_commande < DATE_SUB(NOW(), INTERVAL 1 YEAR);
```

### Vérification de l'intégrité
```sql
-- Vérifier les clés étrangères orphelines
SELECT o.id, o.user_id 
FROM orders o
LEFT JOIN users u ON o.user_id = u.id
WHERE u.id IS NULL;

-- Statistiques de fragmentation
SELECT 
    table_name,
    data_free,
    ROUND(data_free/1024/1024, 2) AS fragmentation_mb
FROM information_schema.tables
WHERE table_schema = 'ma_base'
AND data_free > 0;
```

### Maintenance programmée
```sql
-- Script de maintenance hebdomadaire
DELIMITER //
CREATE PROCEDURE maintenance_hebdomadaire()
BEGIN
    -- Optimiser les tables
    OPTIMIZE TABLE users, orders, products;
    
    -- Analyser les statistiques
    ANALYZE TABLE users, orders, products;
    
    -- Nettoyer les logs
    DELETE FROM error_logs 
    WHERE created_at < DATE_SUB(NOW(), INTERVAL 30 DAY);
    
    -- Statistiques de fin
    SELECT 'Maintenance terminée' as status, NOW() as timestamp;
END //
DELIMITER ;

-- Programmer avec un événement
CREATE EVENT maintenance_event
ON SCHEDULE EVERY 1 WEEK STARTS '2024-01-01 02:00:00'
DO CALL maintenance_hebdomadaire();
```

---
[← Retour au guide principal](../README.md)