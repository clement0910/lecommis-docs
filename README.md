# Documentation Le Commis (Mintlify)

Documentation développeur de l'API, des redirections d'assets et des webhooks Le Commis.

## Développement local

```bash
npm i -g mint        # CLI Mintlify
mint dev             # http://localhost:3000
```

## Structure

| Dossier | Contenu |
|---|---|
| `docs.json` | Configuration Mintlify (navigation, thème, couleurs, onglet API Reference). |
| `essentials/` | Introduction, quickstart, choix d'intégration, auth, rate limiting, erreurs, bonnes pratiques. |
| `integrations/api/` | Les 4 endpoints de l'API v1. |
| `integrations/redirects/` | Redirections / URLs d'assets (plug-and-play). |
| `integrations/webhooks/` | Webhooks sortants (HMAC, événements, retries). |
| `i18n/` | Langues et internationalisation. |
| `api-reference/openapi.yaml` | **Copie synchronisée** depuis le repo de l'app (`openapi/v1/openapi.yaml`). Ne pas éditer à la main. |

## Source OpenAPI

`api-reference/openapi.yaml` est une **copie** : la source de vérité est `openapi/v1/openapi.yaml` dans le repo de l'app, **générée par Rswag** — jamais éditée à la main.

Régénérer (dans le repo de l'app) après un changement de l'API :

```bash
PATTERN="spec/requests/api/**/*_spec.rb" RAILS_ENV=test SWAGGER_DRY_RUN=0 bin/rails rswag:specs:swaggerize
```

La GitHub Action `sync-openapi.yml` (dans le repo de l'app) pousse automatiquement la spec dans ce repo (`api-reference/openapi.yaml`) à chaque push sur `master` qui touche la spec.

## Déploiement

La doc est déployée par la **Mintlify GitHub App** (content directory à la racine du repo) : tout push sur `master` met la doc en ligne.
