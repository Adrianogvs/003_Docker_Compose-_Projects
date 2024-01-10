# Configuração Docker Compose para Apache Airflow e Bancos de Dados

Este repositório contém um conjunto de arquivos Docker Compose para configurar o Apache Airflow, uma plataforma de orquestração de fluxos de trabalho complexos, juntamente com serviços de suporte como PostgreSQL, SQL Server, Redis e outros. A orquestração de tarefas é gerenciada pelo CeleryExecutor.

## Pré-requisitos

- Docker instalado na sua máquina.
- Recursos do sistema suficientes (pelo menos 4GB de RAM, 2 CPUs e 10GB de espaço em disco).

## Serviços

### PostgreSQL

- Serviço de banco de dados para o Airflow.
- Imagem: postgres:13
- Credenciais:
  - Usuário: airflow
  - Senha: airflow
  - Banco de dados: airflow

### SQL Server

- Serviço de banco de dados SQL Server para o Airflow.
- Imagem: mcr.microsoft.com/mssql/server:2019-latest
- Credenciais:
  - SA Password: SuperPassuwordê23

### Redis

- Broker de mensagens usado pelo CeleryExecutor.
- Imagem: redis:latest

### Airflow Webserver

- Interface web do Airflow acessível em [http://localhost:8080](http://localhost:8080).
- Imagem: apache/airflow:2.5.1
- Dependências:
  - PostgreSQL (Condição: service_healthy)
  - SQL Server (Condição: service_healthy)
  - Redis (Condição: service_healthy)
- Volumes:
  - Dags: `/opt/airflow/dags`
  - Logs: `/opt/airflow/logs`
  - Plugins: `/opt/airflow/plugins`

### Airflow Scheduler

- Serviço de agendamento para lidar com a programação de tarefas no Airflow.
- Imagem: apache/airflow:2.5.1
- Dependências:
  - PostgreSQL (Condição: service_healthy)
  - SQL Server (Condição: service_healthy)
  - Redis (Condição: service_healthy)

### Airflow Worker

- Serviço de worker Celery para executar tarefas.
- Imagem: apache/airflow:2.5.1
- Dependências:
  - PostgreSQL (Condição: service_healthy)
  - SQL Server (Condição: service_healthy)
  - Redis (Condição: service_healthy)

### Airflow Triggerer

- Serviço Triggerer para gerenciar acionadores de DAG.
- Imagem: apache/airflow:2.5.1
- Dependências:
  - PostgreSQL (Condição: service_healthy)
  - SQL Server (Condição: service_healthy)
  - Redis (Condição: service_healthy)

### Inicialização do Airflow

- Serviço para inicializar o ambiente do Airflow.
- Imagem: apache/airflow:2.5.1
- Verificações:
  - Versão do Airflow (>= 2.2.0 requerido)
  - Recursos do sistema (memória, CPUs, espaço em disco)

### CLI do Airflow

- Serviço de interface de linha de comando para o Airflow.
- Imagem: apache/airflow:2.5.1

### Flower (Monitoramento do Celery)

- Serviço de monitoramento para o Celery, acessível em [http://localhost:5555](http://localhost:5555).
- Imagem: apache/airflow:2.5.1
- Dependências:
  - PostgreSQL (Condição: service_healthy)
  - SQL Server (Condição: service_healthy)
  - Redis (Condição: service_healthy)

## Começando

1. Clone este repositório.
2. Navegue até o diretório do repositório no seu terminal.
3. Execute `docker-compose up -d` para iniciar os serviços.
4. Acesse a interface web do Airflow em [http://localhost:8080](http://localhost:8080).

## Observações

- Certifique-se de ter os recursos do sistema necessários antes de iniciar os serviços.
- Personalize as variáveis de ambiente no arquivo Compose conforme necessário.
- Verifique a interface web do Airflow para DAGs, status das tarefas e logs.

![Interface Web do Airflow](path/to/airflow_web_interface_screenshot.png)
![Monitoramento do Flower](path/to/flower_monitoring_screenshot.png)
