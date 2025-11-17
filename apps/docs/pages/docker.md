# Docker Install

Requirements:

- Docker
- Docker Compose

```docker
version: "3.8"
services:
  peppermint_postgres:
    container_name: peppermint_postgres
    image: postgres:latest
    restart: always
    volumes:
      - pgdata_live:/var/lib/postgresql # Updated for Postgres 18+
    environment:
      POSTGRES_USER: peppermint_7g3x
      POSTGRES_PASSWORD: P3pp3rM1nt!x9zQ
      POSTGRES_DB: peppermint
    ports:
      - 5432:5432
  peppermint:
    container_name: peppermint
    image: pepperlabs/peppermint:latest
    ports:
      - 1000:3000
      - 1001:5003
    # If running via Docker on a hypervisor, enable DNS.
    #    dns:
    #      - 1.1.1.1
    #      - 8.8.8.8
    restart: always
    depends_on:
      - peppermint_postgres
    environment:
      DB_USERNAME: peppermint_7g3x
      DB_PASSWORD: P3pp3rM1nt!x9zQ
      DB_HOST: peppermint_postgres
      SECRET: peppermint4life
volumes:
  pgdata_live: null
networks: {}
```

After you have created the docker-compose.yml file, run the following command:

```bash
docker-compose up -d
```

Then you can access the application at http://your-server-ip:3000

The default login credentials for the admin account are:

```
admin@admin.com
1234
```
