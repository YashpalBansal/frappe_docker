# Portainer Deployment Notes

This branch is prepared for a Portainer-based ERPNext deployment on Ubuntu / CasaOS.

## Quick start

1. Copy `example.env` to `.env`.
2. Review and change the default values.
3. Generate the final compose file using the official Frappe Docker method.
4. Paste the generated `docker-compose.yml` into Portainer as a Stack.

## Important

The official `compose.yaml` is designed to be combined with override files and environment variables. Do not deploy it directly without generating the final compose file first.

### Required values in `example.env`

- `ERPNEXT_VERSION=v16.51.0`
- `DB_PASSWORD`
- `FRAPPE_SITE_NAME_HEADER` or the host-based default
- `HTTP_PUBLISH_PORT` if you want a non-default published port

## Suggested workflow

```bash
cp example.env .env
# edit .env

docker compose \
  -f compose.yaml \
  -f overrides/compose.mariadb.yaml \
  -f overrides/compose.redis.yaml \
  -f overrides/compose.noproxy.yaml \
  config > docker-compose.yml
```

Then open Portainer and deploy `docker-compose.yml` from the Web Editor.
