# Documentation Le Commis (Mintlify)

Documentation développeur de l'API publique, des redirections d'assets et des webhooks Le Commis.

## Développement local

```bash
npm i -g mint        # CLI Mintlify
cd mintlify
mint dev             # http://localhost:3000
```

## Structure

| Dossier | Contenu |
|---|---|
| `docs.json` | Configuration Mintlify (navigation, thème, couleurs, onglet API Reference). |
| `essentials/` | Introduction, quickstart, choix d'intégration, auth, rate limiting, erreurs, bonnes pratiques. |
| `integrations/api/` | Les 4 endpoints de l'API publique v1. |
| `integrations/redirects/` | Redirections / URLs d'assets (plug-and-play). |
| `integrations/webhooks/` | Webhooks sortants (HMAC, événements, retries). |
| `i18n/` | Langues et internationalisation. |
| `examples/` | Exemples WordPress, Astro, Next.js. |
| `api-reference/openapi.yaml` | **Copie synchronisée** de `../openapi/v1/openapi.yaml`. Ne pas éditer à la main. |

## Source OpenAPI

La source de vérité est `openapi/v1/openapi.yaml` à la racine du repo, **générée par Rswag** — ne jamais éditer le YAML à la main.

Régénérer après un changement de l'API publique :

```bash
PATTERN="spec/requests/api/**/*_spec.rb" RAILS_ENV=test bin/rails rswag:specs:swaggerize
```

La GitHub Action `.github/workflows/sync-openapi.yml` recopie automatiquement la spec dans `mintlify/api-reference/openapi.yaml` à chaque push sur `master` qui touche la spec.

## Déploiement

La doc est déployée par la **Mintlify GitHub App** configurée avec `/mintlify` comme content directory : tout push sur `master` met la doc en ligne.

> À faire une fois : connecter le repo dans le dashboard Mintlify et pointer le content directory sur `mintlify/`. Ajouter de vrais `logo/light.svg`, `logo/dark.svg` et `favicon.svg` (placeholders pour l'instant).
