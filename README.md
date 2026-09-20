# Atividade de Infraestrutura 

## Sobre o projeto

Atividade prática de Infraestrutura de TI com o objetivo de trabalhar com operações de backup e restauração de um banco de dados PostgreSQL, além da análise de instâncias de servidores JBoss e Tomcat em um ambiente de teste.

A atividade foi dividida em duas partes:

1. Criação de banco de dados, tabela, inserção de dados, dump e restore utilizando PostgreSQL.
2. Verificação de instâncias JBoss e Tomcat, incluindo status, tempo de execução e reinicialização de instâncias paradas.

Neste projeto foi realizada integralmente a primeira parte. A segunda parte não pôde ser executada devido a problemas na instalação dos servidores Tomcat e JBoss no ambiente disponível.


## Tecnologias utilizadas

- Linux Mint
- PostgreSQL
- DBeaver
- Terminal Linux
- Bash
- `pg_dump`
- `psql`

---

# 1. Criação do banco de dados

Foi utilizado o DBeaver para realizar a conexão com o PostgreSQL.

O banco utilizado na atividade foi:

atividade_infra

Dentro do banco foi criada a tabela usuario com a seguinte estrutura:

CREATE TABLE usuario (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL
);

# 2. Estrutura da tabela

| Campo | Tipo         | Restrição   |
| ----- | ------------ | ------------|
| id    | SERIAL       | PRIMARY KEY |
| nome  | VARCHAR(100) | NOT NULL    |
| email | VARCHAR(100) | NOT NULL    |


# 3. Inserção de dados
  Após a criação da tabela, foram inseridos diversos registros para possibilitar a realização e posterior validação do backup.

Exemplo:

INSERT INTO usuario (nome, email) VALUES
('douglas', 'douglas@gmail.com'),
('victor', 'victor@gmail.com'),
('wermesson', 'wermesson@gmail.com'),
('leticia', 'leticia@gmail.com');

Foram adicionados outros registros posteriormente, aumentando a quantidade de dados da tabela.

A consulta abaixo foi utilizada para verificar os registros:

- SELECT * FROM usuario;

# 4. Dump do banco de dados
  Após a criação da tabela e inserção dos dados, foi realizado um dump do banco atividade_infra.

  O dump foi realizado pelo terminal Linux utilizando o comando:
  
   "sudo -u postgres pg_dump atividade_infra > atividade_infra.bkp"

  O arquivo de backup foi salvo na pasta Documents.
  

# Explicação do comando:
  
    "sudo -u postgres"

Executa o comando utilizando o usuário postgres.

   "pg_dump"

Ferramenta do PostgreSQL utilizada para realizar o dump de um banco de dados.

  "atividade_infra"

Banco de dados que será exportado.

  ">"

Redireciona a saída do comando para um arquivo.

  "atividade_infra.bkp"

Arquivo que receberá o conteúdo do dump.


# 5. Verificação do arquivo de dump
  
  Para verificar o conteúdo gerado no arquivo de backup, foi utilizado:

    "cat atividade_infra.bkp | less"

  O comando permitiu visualizar o conteúdo do dump diretamente pelo terminal.

# 6. Exclusão do banco original

Para testar a restauração, o banco original foi removido.

Primeiramente, foi acessado o PostgreSQL pelo terminal:

  "sudo -u postgres psql"

Depois, o banco foi excluído:

  "DROP DATABASE atividade_infra;"

A existência do banco foi verificada através do comando:

  "\l"

O comando \l lista os bancos de dados disponíveis no PostgreSQL.


# 7. Criação de um novo banco vazio

Após a exclusão do banco original, foi criado novamente um banco vazio:

  "CREATE DATABASE atividade_infra TEMPLATE template0;"

Nesse momento, o banco existia novamente, porém sem os dados e a estrutura que haviam sido criados anteriormente.


# 8. Restore do banco

Com o novo banco criado, foi realizado o restore utilizando o arquivo de backup.

O comando utilizado foi:

  "sudo -u postgres psql atividade_infra < atividade_infra.bkp"
  
# Explicação do comando:

  "sudo -u postgres"

Executa o comando como o usuário postgres.

  "psql"

Cliente de terminal do PostgreSQL.

  "atividade_infra"

Banco de dados que receberá os dados restaurados.

  "<"

Redireciona o conteúdo de um arquivo para a entrada do comando.

  "atividade_infra.bkp"

Arquivo contendo o dump realizado anteriormente.


# 9. Validação do restore

Após a execução do restore, foi realizada uma nova conexão com o banco atividade_infra e os dados foram consultados.

A tabela e os registros existentes antes da exclusão do banco estavam novamente disponíveis.

Exemplo:

  "SELECT * FROM usuario;"

A restauração foi concluída com sucesso, comprovando que o dump realizado anteriormente poderia ser utilizado para recuperar a estrutura e os dados do banco.


# 10. Segunda parte - JBoss e Tomcat

A segunda parte da atividade consistia na verificação de instâncias dos servidores JBoss e Tomcat em um ambiente de teste.

O objetivo seria verificar se as instâncias estavam em execução e obter informações como:

Status da instância;
Tempo de execução (uptime);
Identificação de uma instância parada;
Reinicialização da instância caso estivesse parada por mais de 1 minuto.

Essa parte não foi implementada devido a problemas encontrados durante a instalação dos servidores JBoss e Tomcat no ambiente disponível para realização da atividade.

Abordagem planejada

A ideia inicial era utilizar as portas das instâncias como um dos meios de verificar se os servidores estavam em execução.

Conceituamente: 

Porta respondendo -> Instância em execução (running) -> Porta sem resposta -> Instância parada (stopped).

Também seria utilizado o cron do Linux para executar periodicamente o script de verificação.

Essa abordagem, entretanto, permaneceu apenas como planejamento e não foi executada na atividade.

# 10 -Resultado

A primeira parte da atividade foi concluída e validada:

- PostgreSQL configurado no ambiente;
- Banco atividade_infra criado;
- Tabela usuario criada;
- Registros inseridos;
- Dump realizado com pg_dump;
- Arquivo de backup gerado;
- Banco original removido;
- Banco vazio recriado;
- Restore realizado com psql;
- Dados restaurados e verificados.

A segunda parte não foi executada devido aos problemas de instalação do JBoss e Tomcat no ambiente disponível.
