# 🔗 SQL Joins - Relations entre Tables

Documentation complète des jointures SQL pour combiner les données de plusieurs tables.

![SQL](https://img.shields.io/badge/SQL-Joins-orange?style=flat-square&logo=postgresql&logoColor=white)

## 🔗 Jointures

**Les jointures** permettent de combiner des données provenant de plusieurs tables en établissant des relations entre elles. Elles sont essentielles dans les bases de données relationnelles pour récupérer des informations liées stockées dans différentes tables. Il existe plusieurs types de jointures selon le comportement souhaité avec les enregistrements qui ne trouvent pas de correspondance.

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

**INNER JOIN** ne retourne que les enregistrements qui ont une correspondance dans les deux tables jointes. C'est le type de jointure le plus restrictif et le plus couramment utilisé.

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

**LEFT JOIN** retourne tous les enregistrements de la table de gauche, même s'ils n'ont pas de correspondance dans la table de droite. Les valeurs manquantes sont remplacées par NULL.

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

**RIGHT JOIN** retourne tous les enregistrements de la table de droite, même s'ils n'ont pas de correspondance dans la table de gauche. C'est l'inverse du LEFT JOIN.

```sql
SELECT u.nom, o.produit, o.prix
FROM users u
RIGHT JOIN orders o ON u.id = o.user_id;
```
*Retourne toutes les commandes, même sans utilisateur*

### FULL OUTER JOIN

**FULL OUTER JOIN** retourne tous les enregistrements des deux tables, qu'ils aient ou non une correspondance. Les valeurs manquantes sont remplacées par NULL des deux côtés.

```sql
SELECT u.nom, o.produit
FROM users u
FULL OUTER JOIN orders o ON u.id = o.user_id;
```
*Retourne tous les utilisateurs et toutes les commandes*

### CROSS JOIN

**CROSS JOIN** effectue un produit cartésien entre deux tables, c'est-à-dire qu'il combine chaque ligne de la première table avec chaque ligne de la seconde table. Attention : cela peut générer un très grand nombre de résultats.

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

## 📊 Exemples Pratiques de Jointures

### Exemple 1 : Commandes avec détails utilisateur
```sql
SELECT 
    u.nom as client,
    u.email,
    o.produit,
    o.prix,
    o.date_commande
FROM users u
INNER JOIN orders o ON u.id = o.user_id
WHERE o.date_commande > '2024-01-01'
ORDER BY o.date_commande DESC;
```

### Exemple 2 : Statistiques par utilisateur
```sql
SELECT 
    u.nom,
    COUNT(o.id) as nb_commandes,
    SUM(o.prix) as total_depense,
    AVG(o.prix) as panier_moyen,
    MAX(o.date_commande) as derniere_commande
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
GROUP BY u.id, u.nom
ORDER BY total_depense DESC;
```

### Exemple 3 : Produits par catégorie avec ventes
```sql
SELECT 
    c.nom as categorie,
    p.nom as produit,
    p.prix as prix_catalogue,
    COUNT(o.id) as nb_ventes,
    SUM(o.prix) as ca_realise
FROM categories c
INNER JOIN products p ON c.id = p.category_id
LEFT JOIN orders o ON p.nom = o.produit
GROUP BY c.id, c.nom, p.id, p.nom, p.prix
ORDER BY c.nom, nb_ventes DESC;
```

### Exemple 4 : Clients sans commande récente
```sql
SELECT 
    u.nom,
    u.email,
    MAX(o.date_commande) as derniere_commande,
    DATEDIFF(CURRENT_DATE, MAX(o.date_commande)) as jours_depuis
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
GROUP BY u.id, u.nom, u.email
HAVING MAX(o.date_commande) < DATE_SUB(CURRENT_DATE, INTERVAL 90 DAY)
   OR MAX(o.date_commande) IS NULL
ORDER BY jours_depuis DESC;
```

## 💡 Conseils pour les Jointures

### Performance
- Utilisez des index sur les colonnes de jointure
- Préférez INNER JOIN à LEFT JOIN quand possible
- Filtrez avec WHERE plutôt qu'avec des conditions dans le JOIN

### Lisibilité
- Utilisez toujours des alias pour les tables
- Soyez explicite avec le type de JOIN
- Organisez vos conditions de jointure logiquement

### Débogage
- Testez d'abord chaque table séparément
- Ajoutez les JOIN une par une
- Utilisez COUNT(*) pour vérifier le nombre de résultats

---
[← Retour au guide principal](../README.md)