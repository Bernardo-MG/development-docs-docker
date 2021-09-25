# Dependencies Between Images

```text
services:
    db:
        image: dbimage:latest
        healthcheck:
            test: check_health_script
            interval: 30s
            timeout: 10s
            retries: 5
    db-seeder:
        image: dbloader:latest
        depends_on:
            db:
                condition: service_healthy
        links:
            - "db"
```

With this health condition the DB seeder will run once the DB has started. This way it will always be able to connect to the DB.

