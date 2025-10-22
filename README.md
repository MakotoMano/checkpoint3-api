# 📦 Checkpoint 3&4&5 — API Spring Boot (Docker & Compose)

> API Java com Spring Boot para consolidar conceitos de **REST**, **camadas de serviço/repositório**, **validação**, **testes** e **empacotamento com Docker/Docker Compose**.

[![Java 17](https://img.shields.io/badge/Java-17+-red)]() [![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-brightgreen)]() [![Maven](https://img.shields.io/badge/Maven-3.9+-blue)]() [![Docker](https://img.shields.io/badge/Docker-24+-informational)]()
[![CI](https://github.com/MakotoMano/checkpoint3-api/actions/workflows/ci.yml/badge.svg?branch=develop)](https://github.com/MakotoMano/checkpoint3-api/actions/workflows/ci.yml)
[![CD](https://github.com/MakotoMano/checkpoint3-api/actions/workflows/cd.yml/badge.svg?branch=main)](https://github.com/MakotoMano/checkpoint3-api/actions/workflows/cd.yml)
[![Release](https://github.com/MakotoMano/checkpoint3-api/actions/workflows/release.yml/badge.svg?branch=main)](https://github.com/MakotoMano/checkpoint3-api/actions/workflows/release.yml)

---

## 👥 Autores

* **Diogo Makoto Mano** – 3SIR – RM98446
* **Thiago Ratão Passerini** – 3SIR – RM551351
* **Victor Espanhol Henrique Santos** – 3SIR – RM552532

---

## 🔗 Tabela de Conteúdo

* [✨ Objetivos](#-objetivos)
* [🧰 Tech stack](#-tech-stack)
* [✅ Pré-requisitos](#-pré-requisitos)
* [▶️ Como executar (Local)](#️-como-executar-local)
* [🐳 Como executar (Docker)](#-como-executar-docker)
* [🧩 Como executar (Docker Compose)](#-como-executar-docker-compose)
* [⚙️ Configuração (.env / perfis)](#️-configuração-env--perfis)
* [📚 Swagger & Consoles](#-swagger--consoles)
* [✅ Funcionalidades (exemplos)](#-funcionalidades-exemplos)
* [🧪 Testes](#-testes)
* [🔒 Boas práticas adotadas](#-boas-práticas-adotadas)
* [☁️ Publicação no Docker Hub](#️-publicação-no-docker-hub)
* [🛠️ Comandos úteis do Docker](#️-comandos-úteis-do-docker)
* [🚀 CI/CD & Release — Checkpoint 2 (2025/3º semestre)](#-cicd--release--checkpoint-2-20253º-semestre)
* [👥 Autores](#-autores)

---

## ✨ Objetivos

* Fixar conceitos de **API REST** com **Spring Boot**.
* Praticar **camadas (Controller → Service → Repository)**, **validação**, **tratamento de erros** e **testes**.
* Aprender **empacotamento com Docker** e **orquestração com Docker Compose**.

---

## 🧰 Tech stack

* **Linguagem:** Java 17+
* **Framework:** Spring Boot (Web, Validation, JPA, Actuator)
* **Documentação:** springdoc-openapi (Swagger)
* **Persistência:** Spring Data JPA
* **Banco:** H2 (dev) e PostgreSQL (docker)
* **Build:** Maven
* **Container:** Docker / Docker Compose

---

## ✅ Pré-requisitos

* **JDK 17+**
* **Maven 3.9+** (ou `mvnw`)
* **Docker 24+** e **Docker Compose**

---

## ▶️ Como executar (Local)

1. **Clone o repositório**

```bash
git clone https://github.com/MakotoMano/checkpoint3-api.git
cd checkpoint3-api
```

2. **Rodando com Maven (perfil `dev`)**

```bash
./mvnw spring-boot:run
# ou
mvn spring-boot:run
```

3. **Acessos**

* Swagger UI: [http://localhost:8080/swagger-ui.html](http://localhost:8080/swagger-ui.html)
* (Opcional) H2 Console: [http://localhost:8080/h2-console](http://localhost:8080/h2-console)

> **Obs.:** No perfil `dev`, a app pode usar H2 (memória) para facilitar o desenvolvimento.

---

## 🐳 Como executar (Docker)

**Build da imagem**

```bash
docker build -t makotomano/checkpoint3-api:latest .
```

**Rodando a imagem publicada**

```bash
docker run --rm --name checkpoint_api \
  -p 8080:8080 \
  -e SPRING_PROFILES_ACTIVE=docker \
  -e SPRING_DATASOURCE_URL=jdbc:postgresql://host.docker.internal:5432/appdb \
  -e SPRING_DATASOURCE_USERNAME=app \
  -e SPRING_DATASOURCE_PASSWORD=app123 \
  makotomano/checkpoint3-api:latest
```

> **Linux:** se `host.docker.internal` não resolver, use o IP da sua máquina host.

---

## 🧩 Como executar (Docker Compose)

**`docker-compose.yml` (exemplo)**

```yaml
services:
  db:
    image: postgres:16
    container_name: checkpoint_db
    environment:
      POSTGRES_DB: appdb
      POSTGRES_USER: app
      POSTGRES_PASSWORD: app123
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data

  api:
    image: makotomano/checkpoint3-api:latest
    container_name: checkpoint_api
    depends_on:
      - db
    environment:
      SPRING_PROFILES_ACTIVE: docker
      SPRING_DATASOURCE_URL: jdbc:postgresql://db:5432/appdb
      SPRING_DATASOURCE_USERNAME: app
      SPRING_DATASOURCE_PASSWORD: app123
    ports:
      - "8080:8080"

volumes:
  pgdata:
```

**Subir os serviços**

```bash
docker compose up -d --build
docker compose logs -f api
docker compose down
```

---

## ⚙️ Configuração (.env / perfis)

**Exemplo `.env` (opcional)**

```env
# Perfil ativo
SPRING_PROFILES_ACTIVE=dev

# Se usar Postgres local
SPRING_DATASOURCE_URL=jdbc:postgresql://localhost:5432/checkpoint
SPRING_DATASOURCE_USERNAME=postgres
SPRING_DATASOURCE_PASSWORD=postgres
```

**Perfis sugeridos**

* `dev`: foco em desenvolvimento (pode usar H2)
* `docker`: conexão com Postgres via Compose

---

## 📚 Swagger & Consoles

* **Swagger UI:**

  * [http://localhost:8080/swagger-ui.html](http://localhost:8080/swagger-ui.html)
  * (alternativo do springdoc) [http://localhost:8080/swagger-ui/index.html](http://localhost:8080/swagger-ui/index.html)
* **H2 Console (se habilitado no `dev`):**

  * [http://localhost:8080/h2-console](http://localhost:8080/h2-console)

---

## ✅ Funcionalidades (exemplos)

* Cadastro de **[Entidade]**
* Listagem de **[Entidade]**
* Atualização de **[Entidade]**
* Exclusão de **[Entidade]**
* Health check: `GET /actuator/health`

> Substitua **[Entidade]** pelo domínio real do projeto (ex.: `Produto`, `Cliente`, etc.) e, se possível, inclua exemplos de payload no Swagger.

---

## 🧪 Testes

Rodar a suíte de testes:

```bash
./mvnw test
# ou
mvn test
```

---

## 🔒 Boas práticas adotadas

* Validação com `@Valid` e Bean Validation
* Tratamento de erros com **@ControllerAdvice / @ExceptionHandler**
* Camadas claras (**Controller**, **Service**, **Repository**)
* Uso de **DTOs** para entrada/saída
* Documentação com **Swagger (springdoc-openapi)**
* Health/metrics via **Spring Boot Actuator**

---

## ☁️ Publicação no Docker Hub

Recomendado versionar sua imagem além do `latest`.

```bash
docker login

docker tag makotomano/checkpoint3-api:latest \
  makotomano/checkpoint3-api:1.0.0

docker push makotomano/checkpoint3-api:1.0.0
docker push makotomano/checkpoint3-api:latest
```

**Docker Hub:** [https://hub.docker.com/repository/docker/makotomano/checkpoint3-api/general](https://hub.docker.com/repository/docker/makotomano/checkpoint3-api/general)

---

## 🛠️ Comandos úteis do Docker

```bash
docker ps -a

docker stop $(docker ps -aq) || true
docker rm $(docker ps -aq) || true

docker rmi $(docker images -q) || true

docker system prune -af
docker volume prune -f
docker builder prune -af
```

---

## 🚀 CI/CD & Release — Checkpoint 2 (2025/3º semestre)

### 🧭 Branches utilizadas

* `main` — estável
* `develop` — desenvolvimento
* `feature/*` — novas funcionalidades
* `hotfix/*` — correções rápidas

### 🔐 Segredos no GitHub (Actions → Secrets)

* `DOCKERHUB_USERNAME` = `makotomano`
* `DOCKERHUB_TOKEN` = Access Token do Docker Hub com **Write**

### ⚙️ Workflows (`.github/workflows`)

**CI — `ci.yml`**

* **Disparo:** `push` em `develop`, `feature/**`, `hotfix/**`
* **Tarefas:** `mvn test` e `mvn package` (Java 17)

**CD (Docker Hub) — `cd.yml`**

* **Disparo:** `pull_request` para `main`
* **Tarefas:** build Docker e **push** no Docker Hub
* **Tag gerada:** `pr-<numero-do-PR>-<shortsha>`
* **Repositório:** `makotomano/checkpoint3-api`

**Release — `release.yml`**

* **Disparo:** `push` em `main`
* **Tarefas:** gerar **CHANGELOG**, abrir **PR de release**; após merge, criar **Tag** e **GitHub Release**
* **Tipo:** `maven` (lê o `pom.xml`)

> Dica: use os *badges* no topo para visualizar o status de cada workflow.


### 🐳 Docker Hub

* **Repo:** `makotomano/checkpoint3-api`



