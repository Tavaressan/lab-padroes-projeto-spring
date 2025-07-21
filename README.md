# Desafio de Padrões de Projeto com Spring Boot

API REST para cadastro de clientes aplicando os padrões Singleton, Strategy e Facade, desenvolvida como Desafio de Projeto para o Santander Bootcamp 2025 na plataforma DIO.

## 📝 Descrição do Projeto

Este projeto consiste na criação de uma API REST utilizando Java e o ecossistema Spring para ilustrar a aplicação prática e otimizada dos Padrões de Projeto (Design Patterns) do "Gang of Four" (GoF). O foco foi a implementação dos padrões **Singleton**, **Strategy** e **Facade** em um contexto real.

A API gerencia um CRUD (Create, Read, Update, Delete) de clientes e seus respectivos endereços. Uma funcionalidade chave é a integração com a API externa **ViaCEP**, que é consumida para buscar e validar endereços a partir de um CEP informado, demonstrando a capacidade de comunicação entre microsserviços.

Além da implementação base proposta no desafio, o projeto foi aprimorado com:
-   **Lombok:** Para reduzir o código boilerplate (getters, setters, construtores).
-   **Tratamento de Erros:** Implementação de uma lógica mais robusta na camada de serviço para lidar com cenários como clientes não encontrados.
-   **Documentação com Swagger:** Adição do SpringDoc para gerar uma documentação interativa da API.

## 🚀 Tecnologias Utilizadas

-   **Java 17**
-   **Spring Boot**
-   **Spring Data JPA**
-   **Spring Web**
-   **Spring Cloud OpenFeign** (Para consumo da API ViaCEP)
-   **H2 Database** (Banco de dados em memória para testes e desenvolvimento)
-   **Lombok** (Para simplificação do código)
-   **Maven** (Gerenciador de dependências)
-   **SpringDoc OpenAPI (Swagger)** (Para documentação da API)

## 🎨 Padrões de Projeto Aplicados

O principal objetivo deste projeto é demonstrar o uso de Design Patterns em uma aplicação Spring.

### Singleton
O padrão Singleton garante que uma classe tenha apenas uma instância e fornece um ponto de acesso global a ela. No ecossistema Spring, os componentes gerenciados pelo contêiner de Injeção de Dependência (como `@RestController`, `@Service`, `@Repository`) são, por padrão, **Singletons**. A injeção com `@Autowired` garante que a mesma instância de um serviço ou repositório seja utilizada em toda a aplicação, otimizando o uso de recursos.

### Strategy
O padrão Strategy permite definir uma família de algoritmos, encapsular cada um deles e torná-los intercambiáveis. No projeto, a interface `ClienteService` define o contrato (a **Strategy**) para as operações de negócio relacionadas a clientes. A classe `ClienteServiceImpl` fornece a implementação concreta dessa estratégia, que poderia ser facilmente substituída por outra implementação sem impactar o `Controller`.

### Facade
O padrão Facade fornece uma interface unificada para um conjunto de interfaces em um subsistema. A classe `ClienteServiceImpl` atua como uma **Facade**, simplificando a interação do `Controller` com a complexidade dos subsistemas. Ela abstrai a lógica de:
1.  Consultar a API externa do ViaCEP.
2.  Verificar se um endereço já existe no banco de dados.
3.  Persistir ou atualizar dados em múltiplos repositórios (`ClienteRepository` e `EnderecoRepository`).

## ⚙️ Como Executar o Projeto

### Pré-requisitos
-   Java 17 ou superior
-   Maven 3.8 ou superior

### Passos

1.  **Clone o repositório:**

```Shell Scriptgit
clone https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git
```

Substitua SEU-USUARIO/SEU-REPOSITORIO pelo caminho do seu projeto no GitHub.

2. **Navegue até o diretório do projeto:**
```Shell Script
cd lab-padroes-projeto-spring3
```
3. **Execute a aplicação com o Maven:**
```Shell Script
mvn spring-boot:run
```
A API estará disponível em `http://localhost:8080`.

## Acessando Recursos
• **Documentação Swagger UI:** 

Para visualizar e interagir com os endpoints da API de forma amigável, acesse a documentação gerada pelo SpringDoc no seu navegador: http://localhost:8080/swagger-ui.html

• **Banco de Dados H2 Console:** 

Para acessar o banco de dados em memória e visualizar as tabelas `CLIENTE` e `ENDERECO`, acesse: http://localhost:8080/h2-console

Utilize as seguintes credenciais para conectar:

  •JDBC URL: jdbc:h2:mem:testdb
  
  •User Name: sa•Password: (deixe em branco)
  
## Endpoints da API

Aqui estão os principais endpoints disponíveis para teste via Swagger, Postman ou cURL.

`POST /clientes` 

Cria um novo cliente. O endereço é buscado e preenchido automaticamente a partir do CEP informado.

Exemplo de Request Body:

```JSON
{
  "nome": "Vitor Tavares",
  "endereco": {
    "cep": "58010120"
  }
}
```

`GET /clientes` 

Retorna uma lista com todos os clientes cadastrados.

`GET /clientes/{id}` 

Busca um cliente específico pelo seu ID.

`PUT /clientes/{id}`

Atualiza os dados de um cliente existente.

Exemplo de Request Body:
```JSON
{
  "nome": "Vitor",
  "endereco": {
    "cep": "01001001"
  }
}
```
`DELETE /clientes/{id}` 

Exclui um cliente pelo seu ID.

## 👨‍💻 Autor

Desenvolvido por Vitor Tavares Chaves.

[LinkedIn](https://www.linkedin.com/in/vitor-tavares-chaves-500967236/)
