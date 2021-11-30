## Start Guide

### Outside Docker containers

- Create .env file `cp .env.example .env` and replace existing env variables
  (mysql/mariadb connection params)
- Install dependencies `yarn`
- Start the app `yarn start` (app will be exposed through the port 3000)

### Inside Docker containers

Just run already prepared bash script:
```bash
$ ./init
```
It will setup the project for you (starting docker-compose stack, running migrations).
The NestJS app running in dev mode will be exposed on `http://localhost` (port 80)

For IDE autocompletion to work, run `yarn` on the host machine.

## TypeORM integrated

[TypeORM](http://typeorm.io/) gives you possibility to use next db types:
`mysql`, `postgres`, `mariadb`, `sqlite`, etc. Please look at docs for more details.
The `docker-compose` template uses `mariadb`.
## Migrations

If you don't work on a production-ready project you can always change `DB_SYNC` env variable to true so you can play with NestJS without the need to write actual migrations.

**`synchronize: true` shouldn't be used in production - otherwise, you can lose production data.**

### Create Migration
Creating new migration is relatively easy and you can use typeorm CLI for that. You can run this command to create new migration:
```bash
$ docker exec -it nest yarn migration:create -n {CreateTableUsers}
```
Migration file will be placed under `src/migrations`. For more details check the existing [1611484925515-CreateUsersTable.ts](src/migrations/1611484925515-CreateUsersTable.ts)

### Run Migrations
```bash
$ docker exec -it nest yarn migration:run
```
### Revert Migrations
```bash
$ docker exec -it nest yarn migration:revert
```

## Environment Configuration

Integrated Configuration Module so you can just inject `ConfigService`
and read all environment variables from `.env` file, which is created automatically by the init script from `.env.example`.

## Swagger

RESTful APIs you can describe with already integrated Swagger.
To see all available endpoints visit http://localhost/api/docs