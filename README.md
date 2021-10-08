## Cakefest 2021

## Unit and CakePHP4 Starterpack


#### Install Unit and PHP

*Install composer*

https://getcomposer.org/download/


The Unit language module for PHP comes with the most important requiret modules as a dependency.

```shell

apt install unit unit-php

```

```shell
apt install php7.4-mbstring php7.4-intl php7.4-dom php7.4-mysql php7.4-sqlite3
```

Adding a runtime User

```shell
useradd -G unit -s /usr/sbin/nologin -M my_appuser
```

## Create your cake-app
```
composer create-project --prefer-dist cakephp/app:~4.0 my_app_name
```

## Unit Configraiton

```
{
    "listeners": {
        "*:80": {
            "pass": "routes/cakephp"
        }
    },
    "routes": {
        "cakephp": [
            {
                "match": {
                    "uri": [
                        "*.php",
                        "*.php/*"
                    ]
                },
                "action": {
                    "pass": "applications/cakephp/direct"
                }
            },
            {
                "action": {
                    "share": "/path/cakefest21demo/webroot",
                    "fallback": {
                        "pass": "applications/cakephp/index"
                    }
                }
            }
        ]
    },
    "applications": {
        "cakephp": {
            "type": "php",
            "user": "my_appuser",
            "group": "my_appuser",
            "processes": {
                "max": 20,
                "spare": 5,
                "idle_timeout": 20
            },            
            "targets": {
                "direct": {
                    "root": "/path/cakefest21demo/webroot"
                },
                "index": {
                    "root": "/path/cakefest21demo/webroot",
                    "script": "index.php"
                }
            },
            "environment": {
                "VERSION": "0.0.1",
                "DEBUG": "false",
                "SECURITY_SALT": "CHANGME",
                "DATABASE_URL":"mysql://USER:PASS@DB_Host_IP/SCHEMA?encoding=utf8mb4&timezone=UTC&cacheMetadata=true&quoteIdentifiers=false&persistent=false"
            },
            "options": {
                "file": "/etc/php.ini",
                "admin": {
                    "memory_limit": "512M",
                    "variables_order": "EGPCS",
                    "expose_php": "0"
                },
        
                "user": {
                    "display_errors": "0"
                }
            }
        }
    } 
}

```
