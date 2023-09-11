## WP-Docker
Running WordPress in an isolated environment using Docker.
Install Docker Compose

### Linux

- Run the following command to download:
  sudo curl -L "https://github.com/docker/compose/releases/download/1.28.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

- Run the following command for permissions:
  sudo chmod +x /usr/local/bin/docker-compose
  If it fails, please verify the path.

- Test the installation:
  $ docker-compose --version
  It should return:
  docker-compose version 1.28.4, build 1110ad01

### Windows

- Use the link below to download and install:
  Docker Desktop for Windows

Creating the Environment

- Create a new directory and navigate to it.
- Create a file named:
  docker-compose.yml
- Copy and paste the following content into the created file:

version: '3.3'

services:
   db:
     image: mysql:5.7
     volumes:
       - db_data:/var/lib/mysql
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

Inside the directory, run the following command:
docker-compose up -d

Now, access http://localhost:8000 in your browser and proceed with the WordPress installation.

Made with ❤ by Andressa Tancredi.
