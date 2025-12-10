# 🔧 SQL Advanced - Fonctions et Techniques Avancées

Documentation des fonctionnalités SQL avancées : fonctions, CTE, window functions et optimisation.

![SQL](https://img.shields.io/badge/SQL-Advanced-purple?style=flat-square&logo=postgresql&logoColor=white)

## 🔧 Fonctions Avancées

**Les fonctions SQL** permettent de manipuler et transformer les données directement dans les requêtes. Elles sont classées en plusieurs catégories : fonctions de chaîne (texte), fonctions de date/heure, fonctions mathématiques, et fonctions conditionnelles.

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

**Les fonctions de fenêtrage** permettent d'effectuer des calculs sur un ensemble de lignes liées à la ligne courante, sans avoir besoin de GROUP BY. Elles offrent des fonctionnalités avancées comme le classement, les moyennes mobiles, et l'accès aux lignes précédentes/suivantes.

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

## 🎯 CTE (Common Table Expressions)

**Les CTE (Common Table Expressions)** sont des tables temporaires nommées qui existent uniquement pendant l'exécution d'une requête. Elles améliorent la lisibilité des requêtes complexes en permettant de décomposer la logique en étapes. Les CTE récursives permettent de traiter des données hiérarchiques.

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

---
[← Retour au guide principal](../README.md)