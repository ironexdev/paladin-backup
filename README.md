# Paladin 

This project is Work in Progress

## How to init development environment

1) Create devstack folder (ie devstack-paladin) and run `git clone git@github.com:ironexdev/paladin.git` in it

2) Init submodules
- `bin/init`
- Run from the devstack folder

3) Add following to etc/hosts
- `127.0.0.1 paladin.local`
- `127.0.0.1 mongo.paladin.local`
- `127.0.0.1 redis.paladin.local`

4) Generate Secrets
- `bin/docker/compose/secrets`
- This command will complain "No such file or directory", but files with secrets should be created anyway.

5) Start Docker
- `bin/docker/compose/up`

6) Install dependencies
- `bin/docker/api-server/composer install`

### Development notes
- App uses Custom (Base) and GraphQL API, MongoDB and Redis.
- Server logs can be found in docker/logs.
- App is protected against CSRF - every request (except GET) has to contain X-CSRF-Token header with previously obtained value from calling <api>/csrf endpoint. This value is stored in a Session.
- Used Docker services
  - api-server
  - http-proxy
  - mongo
  - mongo-express
  - redis
  - redis-admin
- It is recommended to use pretty_print function for data dumping in development.
  - Response generated by this function also contains required CORS headers for XHR debugging.

## Command Reference

`bin/init`
- Pull submodules and add bin/docker symlink to docker submodule in order to make bin/docker commands work. 

`bin/submodule-update`
- Pull submodules

`bin/docker/api-server/composer <command>`
- Run composer in api-server container

`bin/docker/api-server/console`
- Run Symfony Console command in api-server container

`bin/docker/api-server/run <command>`
- Run command on API server

`bin/docker/api-server/xdebug`
- Set PHP Xdebug mode (https://xdebug.org/docs/all_settings#mode) in api-server container

`bin/docker/compose/build <service>`
- Build or rebuild services

`bin/docker/compose/cleanup`
- Stop Docker, remove containers and images (optionally add "-v" flag and remove volumes)

`bin/docker/compose/down <service>`
- Stop one or more running services

`bin/docker/compose/restart <service>`
- Restart one or more services

`bin/docker/compose/secrets`
- Generate Docker secrets

`bin/docker/compose/up`
- Build images if needed and create and start services

`bin/docker/clear-logs`
- Clear api-server and http-proxy logs

## Production deployment notes

- Generate MongoDB Doctrine proxy and hydrator classes
  - Remove var/doctrine/hydrator and /var/doctrine/proxy
  - Run odm:generate:hydrators and odm:generate:proxies