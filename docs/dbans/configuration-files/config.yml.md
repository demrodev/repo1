---
icon: wrench-simple
---

# Config.yml

{% tabs %}
{% tab title="config.yml" %}
{% code lineNumbers="true" %}
```yml
# Plugin prefix (use {prefix} in messages)
prefix: "&b&lНаказания &7| &r"

# Word for permanent punishment
permanent_word: "навсегда"

# Server name (used in sync modes)
server_name: "survival"

# Synchronization mode: single, sync, sync_static
#single - for standalone server usage
#sync - for multi-ple server usage with sync punishments between servers (all network)
#sync_static - for using multi-ple server, but the punishment only applies to the server where the tickets were issued
#IMPORTANT! for SYNC and SYNC_STATIC needs MySQL
mode: "single"

sync:
  ban_check_interval_seconds: 10  #how often do we check a player's ban (in seconds, for SYNC mode)

# Time units localization
time_units:
  second:
    one: "секунду"
    few: "секунды"
    many: "секунд"
  minute:
    one: "минуту"
    few: "минуты"
    many: "минут"
  hour:
    one: "час"
    few: "часа"
    many: "часов"
  day:
    one: "день"
    few: "дня"
    many: "дней"

# Groups that cannot be punished
immune_groups:
  - "admin"
  - "owner"

# Muted command blacklist
muted_command_blacklist:
  - "me"
  - "msg"
  - "tell"
  - "w"
  - "reply"

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

# Punishment limits
punishment_limits:
  default: "1h"
  mvp: "2h"
  helper: "100h"

#Cooldowns between commands using (in sec)
command_cooldowns:
  ban:
    default: 0
    vip: 600
    creative: 600
    helper: 300
    admin: 0
    owner: 0
  tempban:
    default: 0
    vip: 600
    creative: 600
  mute:
    default: 0
    vip: 300
  tempmute:
    default: 0
    creative: 300
  kick:
    default: 0
    moderator: 60
  banip:
    default: 0
    admin: 0

# date format
history:
  date_format: "dd.MM.yyyy HH:mm:ss"
punlist:
  entries_per_page: 10
  date_format: "dd.MM.yyyy HH:mm:ss"

#fallback keys if plugin can't find it in messages.yml
messages:
  target_higher_rank: "{prefix}&cИгрок {target} имеет более высокий ранг, чем вы, и не может быть наказан."
```
{% endcode %}
{% endtab %}
{% endtabs %}
