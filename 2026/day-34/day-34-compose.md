services:

  web:
    build: .
    ports:
      - "5000:5000"

    environment:
      DB_HOST: db
      DB_NAME: testdb
      DB_USER: postgres
      DB_PASSWORD: postgres
      REDIS_HOST: redis

    depends_on:
      db:
        condition: service_healthy
      redis:
        condition: service_started

  db:
    image: postgres:16

    environment:
      POSTGRES_DB: testdb
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres

    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U $$POSTGRES_USER -d $$POSTGRES_DB"]
      interval: 10s
      timeout: 5s
      retries: 5
      start_period: 10s

    volumes:
      - postgres_data:/var/lib/postgresql/data

    restart: always

  redis:
    image: redis:7

volumes:
  postgres_data:
