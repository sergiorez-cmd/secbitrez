# Comandos essenciais

$docker -v (Verificar versão do Docker)

$docker --help (Visualizar lista de opções do Docker)

### Repositório oficial de images para Docker: https://hub.docker.com

Uma imagem (image) Docker é um modelo pré-configurado que especifica o que deve ser incluído em um container Docker, ou seja, representa estaticamente as configurações de um sistema operacional, serviço ou do aplicativo desenvolvido.

### Images populares do Docker: ubuntu, wordpress, apache2, nginx, postgres, mariadb, etc.

$sudo docker search [name-image] (Pesquisar images no hub oficial do Docker)

$sudo docker pull [name-image] (Download de image do hub oficial do Docker)

$sudo docker images (Listar imagens disponíveis no disco local)

$sudo docker container list -a (Listar containers criados)

$sudo docker run -it [ubuntu] (Criar um container em modo interativo)

$sudo docker run --name meu-wordpress -p 8080:80 -d wordpress (Criar um container nomeado em modo de escuta para receber conexões de rede)

$sudo docker run -d --name meu-apache2 -e TZ=UTC -p 8080:80 ubuntu/apache2:2.4-22.04_beta (Criar container servidor web Apache2)

$sudo docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d  postgres (Criar container com instância do banco de dados Postgres)

$sudo docker run --detach --name some-mariadb --env MARIADB_ROOT_PASSWORD=my-secret-password  mariadb:latest

$sudo docker ps (Visualizar containers em execução)

$sudo docker ps -a (Visualizar todos containers criados)

$sudo docker [stop,restart,start] [number_id] (Gerenciar estado de um container)

$sudo docker attach [number_id] (Acessar interace de um container)

$sudo docker rm [number_id] (Remover um container)

$sudo docker rmi [number_id] (Remover uma image)

$sudo docker info (Informações detalhadas do Docker)
