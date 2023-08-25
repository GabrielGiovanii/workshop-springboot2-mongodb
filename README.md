<h1 align="center">Projeto API Restful com Spring Boot NoSQL</h1>

## Sobre o Projeto
Este projeto faz parte do Curso "Java COMPLETO - Programação Orientada a Objetos + Projetos", ministrado pelo Professor Dr. Nelio Alves na plataforma Udemy.
O objeto é compreender as principais diferenças entre paradigma orientado a documentos e relacional, refletir sobre decisões de design para um banco de dados orientado
a documentos e realizar consultas com Spring Data e MongoRepository.

## Tecnologias Utilizadas
* [JavaSE 17](https://docs.oracle.com/en/java)
* [Spring Boot 2](https://docs.spring.io/spring-boot/docs/current/reference/html)
* [Spring Data MongoDB](https://docs.spring.io/spring-data/mongodb/docs/current/reference/html)
* [Apache Tomcat](https://tomcat.apache.org/tomcat-8.5-doc/index.html)
* [Maven](https://maven.apache.org/what-is-maven.html)
* [MongoDB](https://www.mongodb.com/docs)
* [Postman](https://learning.postman.com/docs/publishing-your-api/documenting-your-api)
  
## Práticas Adotadas
* Criação e definição de entidades que representam os documentos do MongoDB.
* Separação das camadas de aplicação, incluindo resource, service e repository.
* Implementação de operações CRUD (Create, Retrieve, Update, Delete) para interagir com o MongoDB.
* Utilização de DTOs (Data Transfer Objects) para transferência de dados personalizada.
* Tratamento de exceções específicas do contexto MongoDB.
* Criação de associações entre entidades usando referências DBRef.
* Execução de consultas com query methods e anotações @Query.
* Utilização do MongoDB Compass para visualização e manipulação direta dos dados.
* Exploração de conceitos de banco de dados orientado a documentos em um contexto prático.

# Como executar
- Clone o projeto
```
git clone https://github.com/GabrielGiovanii/workshop-springboot2-mongodb.git
```
- Abra o projeto na sua IDE
- Execute o projeto, porta local:
```
localhost:8080
```

## Modelo de Domínio
![modelo de dominio](https://github.com/GabrielGiovanii/workshop-springboot2-mongodb/assets/115679464/baefc2fb-d533-4ab2-909e-26005b55063a)

## API Endpoints
- User
  - Listar Users
  ```
  Get: localhost:8080/users
  
  Corpo da Resposta:
  [
      {
          "id": "64e8bbe5d32a9524d9a6d3ec",
          "name": "Maria Brown",
          "email": "maria@gmail.com"
      },
      {
          "id": "64e8bbe5d32a9524d9a6d3ed",
          "name": "Alex Green",
          "email": "alex@gmail.com"
      }
  ]
  ```
  - Listar User por id
  ```
  Get: localhost:8080/users/{id}
  
  Corpo da Resposta:
      {
          "id": "64e8bbe5d32a9524d9a6d3ec",
          "name": "Maria Brown",
          "email": "maria@gmail.com"
      }
  ```
  
  - Criar User
  ```
  Post: localhost:8080/users
  
  Corpo solicitado:
      {
          "name": "gabriel",
          "email": "gabriel@gmail.com"
      }
  ```
  
  - Atualizar User
  ```
  Put: localhost:8080/users/{id}
  
  Corpo solicitado:
    {
        "name": "bobs tucunaré",
        "email": "bobstucuna@gmail.com"
    }
  ```
  
  - Deletar User
  ```
  Delete: localhost:8080/users/{id}
  ```
  
  - Listar Posts por User
  ```
  Get: localhost:8080/users/{id}/posts
  
  Corpo solicitado:
  [
      {
          "id": "64e8bbe5d32a9524d9a6d3ef",
          "date": "2018-03-21T03:00:00.000+00:00",
          "title": "Partiu viagem",
          "body": "Vou viajar para São Paulo. Abraços!",
          "author": {
              "id": "64e8bbe5d32a9524d9a6d3ec",
              "name": "Maria Brown"
          },
          "commentDTO": [
              {
                  "text": "Boa viagem mano!",
                  "date": "2018-03-21T03:00:00.000+00:00",
                  "author": {
                      "id": "64e8bbe5d32a9524d9a6d3ed",
                      "name": "Alex Green"
                  }
              },
              {
                  "text": "Aproveite!",
                  "date": "2018-03-22T03:00:00.000+00:00",
                  "author": {
                      "id": "64e8bbe5d32a9524d9a6d3ee",
                      "name": "Bob Grey"
                  }
              }
          ]
      },
      {
          "id": "64e8bbe5d32a9524d9a6d3f0",
          "date": "2018-03-23T03:00:00.000+00:00",
          "title": "Bom dia",
          "body": "Acordei feliz hoje!",
          "author": {
              "id": "64e8bbe5d32a9524d9a6d3ec",
              "name": "Maria Brown"
          },
          "commentDTO": [
              {
                  "text": "Tenha um ótimo dia!",
                  "date": "2018-03-23T03:00:00.000+00:00",
                  "author": {
                      "id": "64e8bbe5d32a9524d9a6d3ed",
                      "name": "Alex Green"
                  }
              }
          ]
      }
  ]
  ```

- Post
  - Listar Post por id
  ```
  Get: localhost:8080/posts/{id}
  
  Corpo da Resposta:
      {
          "id": "64e8bbe5d32a9524d9a6d3f0",
          "date": "2018-03-23T03:00:00.000+00:00",
          "title": "Bom dia",
          "body": "Acordei feliz hoje!",
          "author": {
              "id": "64e8bbe5d32a9524d9a6d3ec",
              "name": "Maria Brown"
          },
          "commentDTO": [
              {
                  "text": "Tenha um ótimo dia!",
                  "date": "2018-03-23T03:00:00.000+00:00",
                  "author": {
                      "id": "64e8bbe5d32a9524d9a6d3ed",
                      "name": "Alex Green"
                  }
              }
          ]
      }
  ```
  
  - Listar Post por titlesearch
  ```
  Get: localhost:8080/posts/titlesearch?text={title%20title}
  
  Corpo da Resposta:
  [
      {
          "id": "64e8bbe5d32a9524d9a6d3f0",
          "date": "2018-03-23T03:00:00.000+00:00",
          "title": "Bom dia",
          "body": "Acordei feliz hoje!",
          "author": {
              "id": "64e8bbe5d32a9524d9a6d3ec",
              "name": "Maria Brown"
          },
          "commentDTO": [
              {
                  "text": "Tenha um ótimo dia!",
                  "date": "2018-03-23T03:00:00.000+00:00",
                  "author": {
                      "id": "64e8bbe5d32a9524d9a6d3ed",
                      "name": "Alex Green"
                  }
              }
          ]
      }
  ]
  ```
  
  - Listar Post por fullsearch
  ```
  Get: localhost:8080/posts/fullsearch?text={title%20title}&minDate={yyyy-MM-dd}&maxDate={yyyy-MM-dd}
  
  Corpo da Resposta:
  [
      {
          "id": "64e8bbe5d32a9524d9a6d3f0",
          "date": "2018-03-23T03:00:00.000+00:00",
          "title": "Bom dia",
          "body": "Acordei feliz hoje!",
          "author": {
              "id": "64e8bbe5d32a9524d9a6d3ec",
              "name": "Maria Brown"
          },
          "commentDTO": [
              {
                  "text": "Tenha um ótimo dia!",
                  "date": "2018-03-23T03:00:00.000+00:00",
                  "author": {
                      "id": "64e8bbe5d32a9524d9a6d3ed",
                      "name": "Alex Green"
                  }
              }
          ]
      }
  ]
  ```
  
## Estudante
### [Gabriel Giovani](https://www.linkedin.com/in/gabriel-giovanii)

## Autor
### [Nélio Alves](https://www.linkedin.com/in/nelio-alves)
