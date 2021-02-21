# WP-Docker
Como rodar Wordpress em um ambiente isolado usando Docker.


## Instalar Docker Compose

#### Linux

* Rodar o comando para fazer o download:

`sudo curl -L "https://github.com/docker/compose/releases/download/1.28.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose`

* Rodar o comando para permissões:

`sudo chmod +x /usr/local/bin/docker-compose`

Caso falhe, verifique o caminho.

* Teste a instalação:

`$ docker-compose --version`

Deve retornar:

`docker-compose version 1.28.4, build 1110ad01`

#### Windows
* Usar o link abaixo, fazer o download e instalar:

`https://hub.docker.com/editions/community/docker-ce-desktop-windows/`

## Criação do Ambiente

* Crie um diretório novo e entre no diretório.
* Crie um arquivo com o nome:

`docker-compose.yml`
* Copie e cole o conteúdo abaixo no arquivo criado:


```
version: '3.3'

services:
   db:
     image: mysql:5.7
     
     volumes:
     
       - db_data:/var/lib/mysql
       - 
     restart: always
     
     environment:
     
       MYSQL_ROOT_PASSWORD: somewordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "8000:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD: wordpress
       WORDPRESS_DB_NAME: wordpress
volumes:
    db_data: {}

* Dentro do diretório rode o comando:
`docker-compose up -d`

* Agora acesse http://localhost:8000 no seu browser, prossiga com a instalção do Wordpress.

Feito com s2 por Andressa Tancredi.
