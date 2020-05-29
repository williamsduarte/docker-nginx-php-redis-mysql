# Laravel Nginx PHP Redis MySQL 

Adminstração de Laravel, Nginx, PHP-FPM, Redis e MySQL com Docker.

**ESTE AMBIENTE SÓ DEVE SER USADO PARA O DESENVOLVIMENTO!**

**ATENÇÃO**: Não use em produção.

## Images usadas

* [Nginx - PHP-FPM](https://hub.docker.com/r/wyveo/nginx-php-fpm/)
* [MySQL](https://hub.docker.com/_/mysql/)
* [phpMyAdmin](https://hub.docker.com/r/phpmyadmin/phpmyadmin/)
* [Gerar Certificado](https://hub.docker.com/r/jacoelho/generate-certificate/)
* [SMTP](https://hub.docker.com/r/bytemark/smtp/)

## Pacotes usados 

* [Predis](https://github.com/nrk/predis)

## Comece a usá-lo

1. Baixe :

    ```sh
    git clone https://github.com/williamsduarte/docker-nginx-php-redis-mysql.git
    ```
    
2. Entre na pasta do projeto :

    ```sh
    cd docker-nginx-php-redis-mysql
    ```

3. Faça do setup.sh um executável :

   ```sh
   sudo chmod +x setup.sh
   ``` 

4. **Importante!** Clone o repositório do Laravel :

    ```sh
    git clone https://github.com/laravel/laravel.git src && cp src/.env.example src/.env
    ```

5. No arquivo **.env** do Laravel, que encontra-se em `src/.env`, defina as seguintes variáveis de ambiente para :     

    ```env
    DB_CONNECTION=mysql
    DB_HOST=db
    DB_PORT=3306
    DB_DATABASE=app_development
    DB_USERNAME=root
    DB_PASSWORD=secret

    BROADCAST_DRIVER=redis
    CACHE_DRIVER=redis
    QUEUE_CONNECTION=redis
    SESSION_DRIVER=redis
    SESSION_LIFETIME=120

    REDIS_HOST=redis
    REDIS_PASSWORD=null
    REDIS_PORT=6379
    ```

6. Para instalar execute o comando abaixo :

    ```sh
    sudo docker-compose up -d && echo "Por favor, aguarde enquanto o serviço é ..." && sleep 5 && docker exec myapp-web /usr/local/bin/setup.sh
    ```

7. Para acessar o Laravel :

    * [http://localhost:8000](http://localhost:8000/)
    * [https://localhost:3000](https://localhost:3000/) ([HTTPS](https://github.com/nanoninja/docker-nginx-php-mongo#generating-ssl-certificates) não configurado por padrão)

8. Para acessar o phpMyAdmin :

    * [http://localhost:8080](http://localhost:8080/)    

## Diretório 


```sh
docker-nginx-php-redis-mysql
├── README.md
├── bin
│   └── linux
│       └── clean.sh
├── data
│   └── db
│       ├── dumps
│       └── mysql
├── docker-compose.yml
├── Dockerfile
├── etc
│   ├── nginx
│   │   └── default.conf
│   ├── php
│   │   └── php.ini
│   └── ssl
├── setup.sh
└── src (Laravel)
```

## Limpar Projeto

**Aviso**: Apaga todos os containers e volumes.

```sh
./bin/linux/clean.sh $(pwd)
```
