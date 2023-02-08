# apm-terminals
Dashboard for APM Terminals

## Installation

1. Clone/Download repository.

2. Make a EOL conversion of the scripts.

   ```sed -i.bak 's/\r$//' scripts/mongo-rs-no-auth-setup.sh```

3. Up the Docker containers.

   ```run_up.sh```

4. Update new dependencies.

   ###### From container:

    ```docker compose run --rm composer update```

    ```docker compose run --rm composer install```

   ##### From host machine:

   ```cd src/```

   ```composer update```

   ```composer install```

5. Install node modules.

   ```docker compose run --rm npm install```

6. Execute this command line to UP all docker containers:

    ```docker compose -f docker-compose.yml up --build --force-recreate -d```

    or run the file ```run_up.sh```.

    > NOTE: Older versions of Docker may use 'docker-compose' instead of 'docker compose'.

## Installation of a new fresh Laravel

1. Remove ```src``` directory if exists.

   ```rm -R src```

2. Up the Docker containers.

   ```run_up.sh```

3. Create a new Laravel poject. This will also download all dependencies.

    ####### From container:

   ```docker compose run --rm composer create-project laravel/laravel . 8.5.9 --prefer-dist```

    Then [check and change PHP version](#change-composer-platform-php-version) if necessary.

    >sudo chmod -R 777 storage && sudo chmod -R 777 bootstrap/cache
    >
    >docker compose run --rm artisan key:generate

    ####### From host machine:

    ```composer create-project laravel/laravel src 8.5.9 --prefer-dist```

## Troubleshoots

### mongodb-setup container continually restarting and mongodb container isn't the PRIMARY replica set.

1. Check if the shell scripts have the correct "end-of-line":

    1. Confirm that shell file is not found by looking ```mongodb-setup``` container logs.
    
        ```docker logs mongodb-setup | grep "exec /scripts/mongo-rs-no-auth-setup.sh: no such file or directory"```

        The response must be ```exec /scripts/mongo-rs-no-auth-setup.sh: no such file or directory``` string repeated  several times.

    2. Confirm that mongodb is not the PRIMARY replica set.

        ```docker exec -it mongodb mongo```

        The terminal must looks like this:

        ![No Replica Set terminal](./images/troubleshoot_01---no-ReplicaSet.png)

    3. With Notepad++, open the shell file and go to ```View > Show Symbol > Show End of Line```. It must looks like one of both of these:

        ![No Replica Set terminal](./images/troubleshoot_01---CR.png)

        ![No Replica Set terminal](./images/troubleshoot_01---CR_LF.png)

    4. Still in Notepad++, go to ```Edit > EOL Conversion > Unix (LF)```. It must looks like this:

        ![No Replica Set terminal](./images/troubleshoot_01---LF.png)

    5. Save the file and make a full restart of containers:

        ```run_full_down.sh```

        ```run_up.sh```

    6. Wait until ```mongodb-setup``` container stops restarting (```STATUS: Exited```).

        ```docker container ps -a```

    8. Confirm that mongodb is now the PRIMARY replica set.

        ```docker exec -it mongodb mongo```

        The terminal must looks like this:

        ![No Replica Set terminal](./images/troubleshoot_01---yes-ReplicaSet.png)

### From Windows, if we have ```docker endpoint for "default" not found``` when we execute UP command to docker containers.

1. Delete ```.docker``` directory. Which exists on PATH ```C:\Users\your-username\.docker```.

2. Restart Docker service.

### From Windows, if we have ```the input device is not a TTY.  If you are using mintty, try prefixing the command with 'winpty'```.

1. Put ```winpty``` before de command (ex. ```docker exec -it mongodb mongo```):

    ```winpty docker exec -it mongodb mongo```

### If we have something like ```PHP Parse error:  syntax error, unexpected '|', expecting variable (T_VARIABLE) in path/to/file.php on line 30```.

1. It is caused by running different PHP versions between host machine PHP and Docker container PHP inside a Docker volume. Try to reset containers changing PHP version on php.dockerfile. 

### If we have something like ```Fatal error: Composer detected issues in your platform: Your Composer dependencies require a PHP version ">= 8.1.0". You are running 7.4.22. in /var/www/html/vendor/composer/platform_check.php on line 24```.

#### * Change composer platform PHP version.

1. Remove ```src/vendor``` folder.

    ```rm -R src/vendor```

2. Look for php conteiner's PHP version.

    ```docker compose run --rm php -v```

3. Edit ```composer.json``` file adding platform PHP version (the same as used in php container) into config section.

    ```
    "config": {
        "platform": {
            "php": "7.4.22"
        }
    }
   ```

4. Update composer.

    ```docker compose run --rm composer update```

### Error 500

* Try to run composer and artisan commands from Host machine.

* Try to reset containers changing PHP version on php.dockerfile.

* Try to change composer PHP version.
