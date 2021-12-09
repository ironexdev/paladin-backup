# Paladin

## Command reference

Generate Secrets
- `bin/docker/compose/secrets`

Start Docker
- `bin/docker/compose/up`

Stop Docker, remove containers and images (optionally add "-v" flag and remove volumes)
- `bin/docker/compose/cleanup`

Run command on API server
- `bin/docker/api-server/run <command>`

Clear api-server and http-proxy logs
- `bin/docker/clear-logs`

## Production deployment instructions

- Generate MongoDB Doctrine proxy and hydrator classes
  - Remove var/doctrine/hydrator and /var/doctrine/proxy
  - Run odm:generate:hydrators and odm:generate:proxies