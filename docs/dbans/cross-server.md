---
description: Description of cross-server operation and configuration settings
icon: shuffle
---

# Cross-server

## Modes

|     Mode     | Storage type |                                                              Description                                                             | The penalty applies to other netwo servers |
| :----------: | :----------: | :----------------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------: |
|    single    |  H2 or MySQL |                                        Suitable for single servers that do not form a network                                        |                     No                     |
|     sync     |     MySQL    |                     Allows punishing a player on all servers of the network, the player gets punished everywhere                     |                     Yes                    |
| sync\_static |     MySQL    | Allows you to punish a player on a specific server from the network, the punishment will only work on the server where it was issued |                     No                     |

## Server naming ([config.yml](configuration-files/config.yml.md))

{% hint style="warning" %}
If you are using sync or sync\_static, you must specify different names of the network servers in the configuration.
{% endhint %}

{% code title="config.yml" lineNumbers="true" %}
```yml
server_name: "survival"
```
{% endcode %}

## Configure cross-server ([config.yml](configuration-files/config.yml.md))

{% code title="config.yml" lineNumbers="true" %}
```yml
# Synchronization mode: single, sync, sync_static
#single - for standalone server usage
#sync - for multi-ple server usage with sync punishments between servers (all network)
#sync_static - for using multi-ple server, but the punishment only applies to the server where the tickets were issued
#IMPORTANT! for SYNC and SYNC_STATIC needs MySQL
mode: "single"
```
{% endcode %}

## Storage settings ([config.yml](configuration-files/config.yml.md))

{% code title="config.yml" lineNumbers="true" %}
```yml
# Database settings
database:
  type: "h2" #h2 or mysql
  h2:
    file: "data"
  mysql:
    host: "localhost"
    port: 3306
    database: "punishments"
    user: "root"
    password: "password"
    poolSize: 10
```
{% endcode %}

## Ban sync ([config.yml](configuration-files/config.yml.md))

{% hint style="warning" %}
Since the database is used as a link, not a plugin for the proxy server, other servers need to check whether there is an active ban or tempban type of punishment in the database. Therefore, it is possible to change the interval for checking these punishments.
{% endhint %}

{% code title="config.yml" lineNumbers="true" %}
```yml
#how often do we check a player's ban (in seconds, for SYNC mode)
sync:
  ban_check_interval_seconds: 10
```
{% endcode %}

## Flag server:lobby in commands

The flag only works when you have set sync or sync\_static mode in the configuration, this allows you to issue a penalty even if you or the player are on another server.
