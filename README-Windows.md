Cocorico-Docker For Windows
===========================

Cocorico-Docker is a docker composition providing a complete stack (Linux, Nginx, MySQL, PHP, MongoDB) for running 
[Cocorico](https://github.com/Cocolabs-SAS/cocorico) out of the box.

Note that Docker for Windows with shared volumes are very slow and impact Cocorico installation 
and usage performance. Use it for discovery or test purposes.

Requirements
------------

Install [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)

Setup
-----

1. Click on the "Docker Quickstart Terminal" desktop icon

    You are now in a pre-configured Docker Toolbox terminal with `/c/Users/[username]` as working directory.
    
    All the bash commands below should be executed inside this terminal if there is no other indication.

2. Clone this repository
  
    ```bash
    $ mkdir cocorico-project
    $ cd cocorico-project
    $ git clone https://github.com/Cocolabs-SAS/cocorico-docker.git cocorico-docker
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

    Open a new Docker terminal by clicking on desktop icon.
    
    ```bash
    $ cd cocorico-project/cocorico-docker
    $ ./cocorico-docker bash dev@php-cli
    $ composer install
    ```
    
    Once installed composer will ask you to set some parameters. 
    See the next section to know their values.
    
5. Set parameters:

    In cocorico/app/config/parameters.yml:
    
    ```yaml
    parameters:
        database_host: mysql
        database_port: null
        database_name: cocorico_dev
        database_user: cocorico_dev
        database_password: cocorico_dev
        mongodb_server: 'mongodb://192.168.99.100:27017'
        mongodb_database_name: cocorico_dev
        cocorico.assets_base_urls: 'http://cocorico.dev'
        router.request_context.host: cocorico.dev
        router.request_context.scheme: http
    ```

6. Initialize the SQL and NoSQL database

    ```bash
    chmod 744 bin/init-db
    ./bin/init-db php --env=dev
 
    chmod 744 bin/init-mongodb
    ./bin/init-mongodb php --env=dev
    ```
    
7. Dump assets
    
    ```bash
    php app/console assetic:dump --env=dev
    ```
    
8. Configure your host in **Windows terminal** as administrator user
    
    ```bash
    $ ECHO 192.168.99.100 cocorico.dev >> "C:\Windows\System32\drivers\etc\hosts"
    ```
    
9. [Visit your local Cocorico](http://cocorico.dev/)

    Note that on Docker for Windows shared volumes access are very slow.

10. [Visit your local phpmyadmin](http://cocorico.dev:8080/) (root / root)

Enjoy!

Note for Windows / Docker Toolbox / VirtualBox
----------------------------------------------------

* Shared volumes are very slow on Windows (and Mac)

* By default Docker Toolbox expects data volumes are within C:\Users. 

* VirtualBox shared folders are not supported by default by mongodb. 


License
-------

Cocorico-Docker is released under the [MIT license](LICENSE).

