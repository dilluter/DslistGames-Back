DSList - Lista de Games
Sobre
O DSList é uma API REST desenvolvida em Java com Spring Boot, projetada para organizar e classificar uma lista de games.

Status: Concluído em 24 de maio de 2025.

### Nota sobre o Histórico de Commits
Este repositório foi criado em Outubro de 2025 com o objetivo de isolar este projeto específico.
Anteriormente, o código fazia parte de um repositório maior de estudos e aprendizado, que continha diversas outras aplicações em Java. Por conta dessa migração, o histórico de commits que documenta todo o processo de desenvolvimento não está presente aqui.
O código nesta branch `main` representa a versão final e funcional do projeto. O histórico de desenvolvimento original pode ser consultado no repositório antigo: [Projetos_Java](https://github.com/dilluter/Projetos_Java.git).

### Funcionalidades Principais
Listagem de Games: Exibe todos os jogos disponíveis no banco de dados.

Listagem por Categoria: Exibe os jogos agrupados por listas (ex: "Aventura e RPG", "Jogos de Plataforma").

Ordenação de Posições: Permite mover um jogo para uma nova posição dentro de uma lista específica.

Tecnologias Utilizadas
Backend: Java 21, Spring Boot, Spring Data JPA

Banco de Dados: PostgreSQL (Desenvolvimento/Produção) e H2 (Testes)

Gerenciador de Pacotes: Maven

Ambiente: Docker e Docker Compose para o banco de dados

Como Executar o Projeto
Siga os passos abaixo para configurar e rodar a aplicação em seu ambiente local.

Pré-requisitos
Java 17 ou superior

Maven

Docker e Docker Compose

1. Clone o Repositório
Bash

git clone <https://github.com/dilluter/DslistGames-Back.git>
cd dslist
2. Configure e Inicie o Banco de Dados com Docker
Para facilitar a configuração, o projeto utiliza um contêiner Docker para o banco de dados PostgreSQL.

Utilize o script docker-compose.yml fornecido neste Gist: docker-compose.yml for postgres

Salve o conteúdo do link como um arquivo docker-compose.yml na raiz do projeto e execute o seguinte comando no terminal:

Bash

docker-compose up -d
Este comando irá iniciar um contêiner PostgreSQL com as credenciais padrão usadas no projeto (postgres/1234567).

3. Execute a Aplicação
O projeto utiliza perfis do Spring Boot para gerenciar as configurações de ambiente. Para o ambiente de desenvolvimento, ativaremos o perfil dev.

Execute o comando Maven abaixo na raiz do projeto:

Bash

mvn spring-boot:run -Dspring-boot.run.profiles=dev
A aplicação estará disponível em http://localhost:8080.

4. Povoamento de Dados (Seed)
Ao iniciar com o perfil dev, o Spring Boot executará automaticamente o arquivo import.sql para popular o banco de dados com listas e jogos de exemplo.

Configuração
As configurações da aplicação são gerenciadas através dos arquivos application-{profile}.properties.

spring.profiles.active=${APP_PROFILE:test}: Define o perfil padrão como test. Pode ser sobrescrito por uma variável de ambiente APP_PROFILE ou pelo comando Maven, como mostrado acima.

cors.origins: Controla as origens permitidas para requisições Cross-Origin (CORS). O padrão é http://localhost:5173 e http://localhost:3000. Pode ser alterado via variável de ambiente CORS_ORIGINS.

Ambientes:

test (Padrão): Usa um banco de dados em memória H2. O console do H2 pode ser acessado em http://localhost:8080/h2-console.

dev: Conecta-se a uma instância do PostgreSQL local (gerenciada via Docker).

prod: Projetado para produção, busca as credenciais do banco de dados a partir de variáveis de ambiente (DB_URL, DB_USERNAME, DB_PASSWORD).

Endpoints da API
Aqui estão os principais endpoints disponíveis na API:

Método	Endpoint	Descrição
GET	/lists	Retorna todas as listas de games.
GET	/lists/{listId}/games	Retorna os games de uma lista específica, ordenados por posição.
POST	/lists/{listId}/replacement	Move um game para uma nova posição dentro da lista.

Exportar para as Planilhas
Exemplo de corpo da requisição para POST /lists/{listId}/replacement:

JSON

{
  "sourceIndex": 2,
  "destinationIndex": 0
}
