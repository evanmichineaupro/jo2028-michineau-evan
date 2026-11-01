# Site web JO 2028 (PHP / MySQL)

Application web des Jeux Olympiques de Los Angeles 2028 : consultation publique (sports, calendrier, résultats) et espace administrateur (gestion complète des données).

## Installation en local (MAMP / WAMP)
1. Copier le dossier dans `htdocs` (MAMP) ou `www` (WAMP).
2. Dans phpMyAdmin, créer la base `michineau_evan_jo2028` (interclassement utf8_general_ci).
3. Importer `database/db-jo.sql` puis `database/test-data-jo.sql`.
4. Vérifier les identifiants MySQL dans `database/database.php`.
5. Ouvrir `http://localhost/jo2028-michineau-evan/`.

## Comptes de test
| Login | Mot de passe |
|---|---|
| admin | admin123 |
| john_doe | password123 |
| jane_doe | pass123 |

## Organisation
- `pages/` : pages publiques ; `pages/admin/` : espace administrateur (un dossier par gestion : users, sports, places, countries, genders, events, athletes, results)
- `pages/admin/includes/` : fichiers communs (accès, jeton CSRF, fonctions, menu)
- `database/` : connexion PDO, authentification, scripts SQL

## Tests unitaires (PHPUnit)
1. Installer PHP en ligne de commande (inclus dans WAMP) et Composer (https://getcomposer.org/download/).
2. Dans le dossier du projet : `composer install` (crée le dossier `vendor/`).
3. Dans phpMyAdmin, créer la base `michineau_evan_jo2028_test` et y importer uniquement `database/db-jo.sql` (base séparée : les vraies données ne sont jamais touchées).
4. Vérifier les identifiants MySQL dans `tests/BddTestCase.php` (mot de passe `root` pour MAMP, vide pour WAMP).
5. Lancer : `vendor\bin\phpunit --testdox` (Windows) ou `vendor/bin/phpunit --testdox` (Mac/Linux).
6. Résultat attendu : `OK (14 tests, 24 assertions)`.

Les tests couvrent : la sécurité (échappement XSS, hachage Bcrypt), la validation des dates et heures, et la gestion des sports (ajout, doublon, modification, suppression, intégrité).
