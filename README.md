# Projeto WordPress com Docker Compose

Este repositório contém uma configuração completa de um ambiente WordPress utilizando Docker Compose, incluindo serviços adicionais como MySQL, Redis e Prometheus.


## Pré-requisitos

Antes de começar, certifique-se de ter os seguintes itens instalados:

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Instalação
1. Configure o Docker para permitir a coleta de métricas. Edite o arquivo `daemon.json` do Docker:

    - No Linux: `/etc/docker/daemon.json`
    - No Windows: `%programdata%\docker\config\daemon.json`
    - No macOS: `~/.docker/daemon.json`

    Adicione a seguinte configuração:

    ```json
    {
      "experimental": false,
      "metrics-addr": "127.0.0.1:9323"
    }
    ```

    Reinicie o serviço do Docker para aplicar as alterações
  
2. Clone o repositório:

    ```bash
    git clone https://github.com/arthurritzel/dockerProject.git
    cd dockerProject
    ```

3. Inicialize os contêineres:

    ```bash
    docker-compose up
    ```
    Aguarde que todos os containers sejam iniciados corretamente

4. Inicialize o WordPress:

    - Abra seu navegador e vá para `http://localhost:8000`
    - Siga as instruções na tela para concluir a instalação do WordPress:
        - Escolha o idioma.
        - Preencha as informações do site, como título, nome de usuário, senha e email.
        - Clique em "Instalar WordPress"
     - Com a confirmação de instalação clique em acessar.
     - Logue com o usuario e senha escolhidos previamente.
     - Acesse a pagina de plugins do wordpress e clique em ativar no pluguin do *Redis Object Cache*
     - Confirme que o Redis está funcionando corretamente acessando a página de configurações do Redis no WordPress.

    
## Estrutura do Projeto

A estrutura do projeto é a seguinte:

├── wp

├── docker-compose.yml

└── prometheus.yaml

- `wp`: Diretório contendo arquivos relacionados ao WordPress.
- `docker-compose.yml`: Arquivo de configuração do Docker Compose.
- `prometheus.yaml`: Arquivo contendo as configurações necessarias para o prometheus

A configuração padrão expõe os seguintes serviços:

- WordPress: `localhost:8000`
- Redis: `localhost:6379`
- Prometheus: `localhost:9090`


## Serviços Adicionais

### Redis

Redis é utilizado como cache para melhorar a performance do WordPress. Para configurar o WordPress para usar o Redis, é necessario adicionar o seguinte ao seu `wp-config.php`:

```php
define('WP_REDIS_HOST', 'redis');
define('WP_REDIS_PORT', '6379');
```

No entando esse passo não é necessario para o uso completo desse repositorio, visto que essa configuração ja esta inserida na pasta wp do projeto, e a mesa esta mapeada no docker


### Prometheus

Prometheus é utilizado para monitorar a performance dos serviços. A configuração padrão do Prometheus pode ser encontrada em prometheus.yml.

Para acessar a interface do Prometheus, vá para:
- `localhost:9090`
