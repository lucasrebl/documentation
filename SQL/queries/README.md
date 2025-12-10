# 🔍 SQL Queries - Consultation et Recherche de Données

Documentation complète des requêtes SELECT et techniques de consultation des données.

![SQL](https://img.shields.io/badge/SQL-Queries-green?style=flat-square&logo=postgresql&logoColor=white)

## 🔍 DQL - Data Query Language

**Le DQL (Data Query Language)** est dédié à la récupération et consultation des données. La commande SELECT est au cœur du DQL et permet d'interroger la base de données pour extraire des informations selon des critères spécifiques. C'est la partie la plus utilisée de SQL dans le développement d'applications.

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

**Les conditions WHERE** permettent de filtrer les résultats selon des critères spécifiques. Elles définissent quels enregistrements doivent être sélectionnés, mis à jour ou supprimés en fonction de conditions logiques.

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

**Le tri (ORDER BY)** organise les résultats selon un ou plusieurs critères, en ordre croissant ou décroissant. **La limitation (LIMIT)** restreint le nombre de résultats retournés, utile pour la pagination ou pour éviter de surcharger l'application avec trop de données.

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

**Les fonctions d'agrégation** effectuent des calculs sur un ensemble de valeurs et retournent une valeur unique. Elles permettent de calculer des statistiques comme le nombre d'enregistrements, la moyenne, la somme, les valeurs minimales et maximales d'une colonne.

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

**Le regroupement (GROUP BY)** permet de rassembler les enregistrements ayant des valeurs identiques dans certaines colonnes pour leur appliquer des fonctions d'agrégation. **HAVING** filtre les groupes après regroupement, contrairement à WHERE qui filtre avant.

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

## 🔄 Sous-requêtes

**Les sous-requêtes** (ou requêtes imbriquées) sont des requêtes SELECT intégrées dans une autre requête SQL. Elles permettent d'utiliser le résultat d'une requête comme condition ou source de données pour une requête principale. Elles peuvent être utilisées dans les clauses WHERE, FROM, SELECT, ou HAVING.

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

**Les sous-requêtes corrélées** font référence à des colonnes de la requête externe. Elles sont évaluées pour chaque ligne de la requête principale, ce qui les rend plus lentes mais parfois nécessaires pour des logiques complexes.

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

---
[← Retour au guide principal](../README.md)