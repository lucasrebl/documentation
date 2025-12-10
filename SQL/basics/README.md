# 🏗️ SQL Basics - Structure et Manipulation de Base

Documentation des commandes SQL fondamentales pour créer et manipuler des bases de données.

![SQL](https://img.shields.io/badge/SQL-Database-blue?style=flat-square&logo=postgresql&logoColor=white)

## 🏗️ DDL - Data Definition Language

**Le DDL (Data Definition Language)** permet de définir et modifier la structure de la base de données. Il s'agit des commandes pour créer, modifier ou supprimer des bases de données, des tables, des index et des contraintes. Ces commandes affectent le schéma de la base de données, pas les données elles-mêmes.

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

**Le DML (Data Manipulation Language)** regroupe les commandes pour manipuler les données contenues dans les tables. Ces opérations permettent d'insérer de nouveaux enregistrements, de modifier des données existantes ou de les supprimer. Contrairement au DDL, le DML n'affecte pas la structure de la base de données.

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

---
[← Retour au guide principal](../README.md)