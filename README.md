# 🌱 Backend SeedTech - Sistema de Gestão Agrícola

Este é o backend desenvolvido em **Spring Boot** para o sistema SeedTech. O projeto gerencia o relacionamento entre agricultores, sementes, condições climáticas e recomendações de plantio, respeitando regras rígidas de integridade de banco de dados (SQL).

## 🚀 Tecnologias Utilizadas

* **Java 17**
* **Spring Boot 3+** (Web, Data JPA)
* **MySQL** (Banco de dados relacional)
* **Insomnia** (Testes de API)

---

## ⚙️ Configuração do Banco de Dados

Antes de rodar, certifique-se de que o MySQL está rodando e configure o arquivo `src/main/resources/application.properties`:

```properties
spring.application.name=backendlogin
spring.datasource.url=jdbc:mysql://localhost:3306/seedtech?useSSL=false&serverTimezone=UTC&allowPublicKeyRetrieval=true
spring.datasource.username=root
spring.datasource.password=SUA_SENHA_AQUI

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect
Nota: É recomendado importar o arquivo banco_atualizado.sql no MySQL Workbench para garantir que as tabelas e os IDs (Auto Increment) estejam configurados corretamente.

🔄 Ordem de Execução (CRUD)
Devido às Chaves Estrangeiras (Foreign Keys), é necessário seguir uma ordem estrita para cadastrar (POST) e apagar (DELETE) dados, caso contrário ocorrerá o Erro 500 (Constraint Violation).

🟢 1. Ordem de Criação (POST)
Crie os dados nesta sequência para popular o banco ("De cima para baixo").

Usuario (/api/usuarios) - Cria o acesso/login.

Agricultor (/api/agricultores) - ID Manual (ex: AG001).

Semente (/api/sementes) - ID Manual (ex: SEM001).

ClimaExtremo (/api/clima-extremos) - ID Manual (ex: CL001).

CondicaoSolo (/api/condicoes-solo) - ID Manual (ex: SOLO001).

SoloAmostra (/api/solo-amostras) - Depende de Agricultor e CondicaoSolo.

ComparaCondicao (/api/compara-condicoes) - Depende de Semente e Clima.

Recomendacao (/api/recomendacoes) - Depende de SoloAmostra.

RecomendacaoHistorico (/api/recomendacao-historicos) - Depende de Recomendacao.

Feedback (/api/feedbacks) - Depende de Agricultor e Recomendacao.

🔴 2. Ordem de Limpeza (DELETE)
Para limpar o banco, apague nesta sequência inversa ("De baixo para cima").

Feedback

RecomendacaoHistorico

Recomendacao

SoloAmostra

ComparaCondicao

(Agora as tabelas independentes estão liberadas):

Agricultor

Semente

ClimaExtremo

CondicaoSolo

Usuario

🔑 Endpoints Principais
Autenticação
POST /api/auth/login

Body: { "username": "admin", "senha": "123" }

Exemplo de Fluxo (Agricultor)
Listar: GET /api/agricultores

Criar: POST /api/agricultores

Atualizar: PUT /api/agricultores/{id}

Deletar: DELETE /api/agricultores/{id}

📦 Como Executar
Clone este repositório ou extraia o arquivo .zip.

Importe o projeto na sua IDE (Spring Tools Suite, IntelliJ, etc).

Atualize as dependências do Maven (Botão direito no projeto -> Maven -> Update Project).

Execute a classe BackendloginApplication.java como Java Application.

Importe a coleção insomnia_seedtech.json no Insomnia para testar as rotas.

👨‍💻 Autores
Arthur Alexandre, Lucas Ferreira Gomes, Felipe Diogo, Hugo Pires, Júlio Augusto, Wesley Telles
