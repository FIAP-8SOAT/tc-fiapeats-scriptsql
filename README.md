# tc-fiapeats-scriptsql


# Deploy SQL Scripts to RDS

Este repositório contém um pipeline automatizado para executar scripts SQL em um banco de dados **PostgreSQL** hospedado no **Amazon RDS**.

## Fluxo de Trabalho

O pipeline é acionado automaticamente sempre que houver um **push** no branch `main`. Ele executa os scripts SQL localizados no diretório `scripts/` em ordem alfabética.

## Tecnologias Utilizadas

- **GitHub Actions**: Para orquestrar o pipeline de CI/CD.
- **PostgreSQL Client**: Para executar os scripts SQL.
- **Amazon RDS**: Banco de dados hospedado na AWS.

## Configuração do Pipeline

### Estrutura do Projeto

O projeto deve seguir a seguinte estrutura:

```plaintext
.
├── .github/
│   └── workflows/
│       └── deploy-sql.yml   # Pipeline do GitHub Actions
└── scripts/
    ├── 001-create-tables.sql
    ├── 002-insert-data.sql
    └── ...
```

### Secrets Necessárias

Para conectar-se ao banco de dados, você precisa configurar as **secrets** no repositório do GitHub:

| Nome da Secret      | Descrição                          |
|---------------------|-----------------------------------|
| `DB_HOST`          | Endpoint do banco de dados RDS   |
| `DB_NAME`          | Nome do banco de dados           |
| `DB_USER`          | Usuário do banco de dados         |
| `DB_PASSWORD`      | Senha do banco de dados          |

### YAML do Pipeline

O arquivo `deploy-sql.yml` está localizado em `.github/workflows/` e possui as seguintes etapas:

1. **Checkout do Repositório**: Faz o download do código para o ambiente de execução.
2. **Instalação do Cliente PostgreSQL**: Instala o cliente para executar os comandos `psql`.
3. **Execução dos Scripts SQL**: Executa os arquivos `.sql` do diretório `scripts/` em ordem alfabética.

## Como Adicionar Scripts

1. Crie um arquivo SQL no diretório `scripts/`.
2. Nomeie os arquivos de forma ordenada, por exemplo:
   - `001-create-tables.sql`
   - `002-insert-data.sql`
3. Faça commit e push das alterações no branch `main`.

## Observações

- Certifique-se de que o banco de dados esteja acessível via rede pública ou configurado corretamente no **Security Group**.
- Os arquivos SQL são executados em ordem alfabética, garantindo a sequência correta.
