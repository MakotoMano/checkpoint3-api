
# 📦 Checkpoint 3

**Checkpoint 3** é um projeto desenvolvido em Java, utilizando o framework Spring Boot, com o objetivo de [insira aqui o objetivo do projeto, por exemplo: "gerenciar uma lista de tarefas", "simular um sistema bancário", etc.].

----------

## 🚀 Tecnologias Utilizadas

-   Java 17
    
-   Spring Boot
    
-   Maven
    
-   Spring Data JPA
    
-   H2 Database (banco de dados em memória)
    
-   Lombok
    


----------

## ▶️ Como Executar o Projeto

1.  **Clone o repositório:**
    
    bash
    
    CopiarEditar
    
    `git clone https://github.com/MakotoMano/checkpoint3.git cd checkpoint3` 
    
2.  **Execute o projeto com Maven:**
    
    arduino
    
    CopiarEditar
    
    `./mvnw spring-boot:run` 
    
3.  **Acesse a aplicação:**
    
    -   Swagger UI: [http://localhost:8080/swagger-ui.html](http://localhost:8080/swagger-ui.html)
        
    -   H2 Console: [http://localhost:8080/h2-console](http://localhost:8080/h2-console)
        

----------

## ✅ Funcionalidades

-   Cadastro de [entidade]
    
-   Listagem de [entidade]
    
-   Atualização de [entidade]
    
-   Exclusão de [entidade]
    
-   Outras funcionalidades relevantes
    

_Nota: Substitua [entidade] pelas entidades específicas do seu projeto, como "usuários", "produtos", etc._

## Executar via imagem publicada (Docker Hub):

docker run --rm --name checkpoint_api \
  -p 8080:8080 \
  -e SPRING_PROFILES_ACTIVE=docker \
  -e SPRING_DATASOURCE_URL=jdbc:postgresql://host.docker.internal:5432/appdb \
  -e SPRING_DATASOURCE_USERNAME=app \
  -e SPRING_DATASOURCE_PASSWORD=app123 \
  seuusuario/checkpoint3-api:latest

## Executar via docker-compose:

- docker compose up -d --build

## Swagger:

- http://localhost:8080/swagger-ui.html
(com springdoc; se preferir o path padrão: /swagger-ui/index.html).

## Comandos para publicar no Docker Hub:

- docker login
- docker tag makotomano/checkpoint3-api:latest makotomano/checkpoint3-api:1.0.0
- docker push makotomano/checkpoint3-api:1.0.0

link dockerhub: https://hub.docker.com/repository/docker/makotomano/checkpoint3-api/general

# Comandos para subir as imagens do docker compose

- docker-compose up -d
- docker-compose logs -f api
- docker-compose down
----------

## 🔒 Validações e Boas Práticas

-   Utilização de `@Valid` para validação de entradas
    
-   Separação de responsabilidades em camadas (Controller, Service, Repository)
    
-   Uso de DTOs para transferência de dados
    
-   Documentação da API com Swagger


Diogo Makoto Mano - 3SIR - RM98446
Thiago Ratão Passerini - 3SIR - RM551351
Victor Espanhol Henrique Santos - 3SIR - RM552532
