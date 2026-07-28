Dockerfile-multistage:

FROM python:3.9-slim AS builder

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt --target /app/libraries

COPY . .

FROM python:3.9-slim AS deployer

WORKDIR /app

COPY --from=builder /app/libraries /app/libraries

COPY --from=builder /app .

ENV PYTHONPATH=/app/libraries
ENV MYSQL_DATABASE_HOST=mysql
ENV MYSQL_DATABASE_USER=db_user
ENV MYSQL_DATABASE_PASSWORD=Passw0rd
ENV MYSQL_DATABASE_DB=employee_db

CMD ["python3", "app.py"]


Docker-compose:

services:

  web:
    build:
      context: .
      dockerfile: Dockerfile.multistage
      container_name: simple-webapp

    ports:
      - "5000:5000"
    environment:
      MYSQL_DATABASE_HOST: ${MYSQL_DATABASE_HOST}
      MYSQL_DATABASE_USER: ${MYSQL_USER}
      MYSQL_DATABASE_PASSWORD: ${MYSQL_PASSWORD}
      MYSQL_DATABASE_DB: ${MYSQL_DATABASE}

    depends_on:
      mysql:
        condition: service_healthy

    networks:
      - webapp-network


  mysql:
    image: mysql:5.7
    environment:

      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}

    volumes:
      - mysql-data:/var/lib/mysql

    networks:
      - webapp-network

    healthcheck:
      test: ["CMD", "mysqladmin", "ping", "-h", "localhost", "-pPassw0rd"]
      interval: 5s
      timeout: 5s
      retries: 10

  volumes:
    mysql-data:

  networks:
    webapp-network:
      driver: bridge

