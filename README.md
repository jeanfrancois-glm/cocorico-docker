Cocorico-Docker
===============

Cocorico-Docker is a docker composition providing a complete stack (Linux, Nginx, MySQL, PHP, MongoDB) for running 
[Cocorico](https://github.com/Cocolabs-SAS/cocorico) out of the box.

For Windows instructions see the [README for Windows](README-Windows.md)

Requirements
------------

Install [Docker Engine](https://docs.docker.com/engine/installation/)

Install [Docker Compose](https://docs.docker.com/compose/install/)


Setup
-----

Clone this repository

```bash
cd /path/to/cocorico-project
git clone https://github.com/Cocolabs-SAS/cocorico-docker.git cocorico-docker
```

Usage
-----

```bash
$ cd cocorico-docker
$ ./cocorico-docker --help
```


Getting started
---------------

1. Clone Cocorico repository 

    ```bash
    $ ./cocorico-docker install
    ```

2. [Create services accounts](https://github.com/Cocolabs-SAS/cocorico/blob/master/src/Cocorico/CoreBundle/Resources/doc/services-creation.rst)

3. Start docker composition

    The first build may take some time. The next ones are very fast.
    
    ```bash
    $ ./cocorico-docker start
    ```

4. Install Cocorico dependencies

    Once installed composer will ask you to set some parameters. 
    See the next section to know their values.
    
    ```bash
    $ ./cocorico-docker bash dev@php-cli
    $ composer install
    ```

5. Set parameters:

    ```yaml
    parameters:
        database_host: mysql
        database_port: null
        database_name: cocorico_dev
        database_user: cocorico_dev
        database_password: cocorico_dev
        mongodb_server: 'mongodb://mongo:27017'
        mongodb_database_name: cocorico_dev
        cocorico.assets_base_urls: 'http://cocorico.dev'
        router.request_context.host: cocorico.dev
        router.request_context.scheme: http
    ```

7. Initialize the SQL and NoSQL database

    ```bash
    chmod 744 bin/init-db
    ./bin/init-db php --env=dev
 
    chmod 744 bin/init-mongodb
    ./bin/init-mongodb php --env=dev
    ```
    
8. Dump assets

    ```bash
    php app/console assetic:dump --env=dev
    ```

9. Configure your host

   ```bash
    $ echo "127.0.0.1 localhost cocorico.dev >> /etc/hosts"
    ```
    
10. [Visit your local Cocorico](http://cocorico.dev/)

11. [Visit your local phpmyadmin](http://cocorico.dev:8080/) (root / root)

Enjoy!


License
-------

Cocorico-Docker is released under the [MIT license](LICENSE).