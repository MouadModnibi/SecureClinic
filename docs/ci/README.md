# Guide CI — SecureClinic


Fichier du workflow : `.github/workflows/ci.yml`

## 1. Quand la CI s'exécute-t-elle ?

| Événement | CI exécutée ? |
|---|---|
| Pull Request vers `main` | Oui |
| Merge (push) sur `main` | Oui |
| Push sur une autre branche sans PR | Non |

## 2. Règles des branches

- `main` est protégée : **aucun push direct**. Toute modification passe par une Pull Request.
- Une PR ne peut être fusionnée que si :
  - tous les checks CI obligatoires sont verts ;
  - au moins **1 coéquipier l'a approuvée**.
- Nommage des branches :

| Préfixe | Usage | Exemple |
|---|---|---|
| `feature/` | Nouvelle fonctionnalité | `feature/patient-booking` |
| `fix/` | Correction de bug | `fix/login-lockout` |
| `ci/` | Modification de la pipeline | `ci/add-gitleaks` |
| `docs/` | Documentation | `docs/threat-model` |



Préfixes de commit : `feat:`, `fix:`, `ci:`, `docs:`, `test:`, `chore:`.

## 4. Jobs CI actuels

| Nom du job | Dossier | Rôle |
|---|---|---|
| `backend-tests` | `backend/` | PHP 8.3, `composer install`, `php artisan test` (SQLite en mémoire) |
| `frontend-build` | `frontend/` | Node 22, `npm ci`, lint, tests, `npm run build` |
| `mobile-check` | `mobile/` | Node 22, `npm ci`, lint, tests |

Un job est **ignoré** (reste vert) tant que son dossier ne contient pas de `composer.json` / `package.json`.

**Les noms des jobs ne doivent jamais être renommés** : la protection de branche les exige par leur nom.
