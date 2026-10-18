---
icon: message
---

# Messages.yml

{% tabs %}
{% tab title="Messages.yml (RU)" %}
{% code lineNumbers="true" %}
```yml
# Файл с локализуемыми сообщениями плагина
# Поддерживает HEX-цвета вида &#RRGGBB и стандартные &c, &a и т.д.
# Плейсхолдеры: {prefix}, {sender}, {target}, {reason}, {duration}, {server}, {id}, {date}, {type}, {issuer}, {page}, {total_pages}, {player}, {expires}, {command}, {max}, {group}, {status}, {preset}, {name}

# Status punishments for web-interface and /history & /punlist
status_active: "&aАктивно"
status_expired: "&eИстекло"
status_pardoned: "&cСнято"

# Errors and information messages
no_permission: "{prefix}&cУ вас нет прав на использование этой команды."
player_not_found: "{prefix}&cИгрок {target} не найден."
invalid_time: "{prefix}&cНеверный формат времени. Пример: 1h30m (1 час 30 минут), 2d (2 дня), 30m (30 минут)."
limit_exceed: "{prefix}&cВы не можете выдать наказание дольше {max} (ваша группа: {group})."
target_immune_group: "{prefix}&cИгрок {target} принадлежит группе {group}, которую нельзя наказывать."
target_immune_permission: "{prefix}&cИгрок {target} имеет иммунитет к этому типу наказаний."
punishment_not_found: "{prefix}&cНаказание с ID {id} не найдено."
punishment_deleted: "{prefix}&aНаказание #{id} успешно удалено из базы данных."
reason_updated: "{prefix}&aПричина наказания #{id} изменена на: {reason}"
no_history: "{prefix}&cУ игрока {target} нет истории наказаний."
reload_success: "{prefix}&aКонфигурация и пресеты успешно перезагружены."
cannot_punish_self: "{prefix}&cВы не можете наказать самого себя."
preset_not_found: "{prefix}&cПресет не найден: {name}"
preset_wrong_type: "{prefix}&cПресет {preset} нельзя использовать с /{command}"
preset_has_duration: "{prefix}&cПресет {preset} имеет длительность. Используйте /{command}"
preset_no_duration: "{prefix}&cПресет {preset} не имеет длительности. Используйте /{command}"
cannot_punish_higher_priority: "{prefix}&cВы не можете наказать игрока {target} с более высоким приоритетом (ваш: {issuer_priority}, его: {target_priority})."
command_on_cooldown: "{prefix}&cВы не можете использовать команду /{command} ещё {time} секунд."
ban_already: "{prefix}&cИгрок {target} уже забанен."
not_banned: "{prefix}&cИгрок {target} не забанен."
ip_not_found_for_player: "{prefix}&cНе найден IP-бан для игрока {target}."
ip_not_banned: "{prefix}&cIP-адрес {target} не забанен."
ip_banned_already: "{prefix}&cIP-адрес игрока {target} уже забанен."

#Mute
muted_command_blocked: "{prefix}&cВы замучены и не можете использовать команду /{command}."
cannot_chat: "&c✖ Вы замучены {sender} на {duration}. Причина: {reason}. \nСервер: {server}"
mute_broadcast: "{prefix}&e❱ {sender} замутил {target} навсегда. &6Причина: {reason}"
mute_player: "&c✖ Вы были замучены {sender} навсегда. Причина: {reason}\nСервер: {server}"
tempmute_broadcast: "{prefix}&e❱ {sender} замутил {target} на {duration}. &6Причина: {reason}"
tempmute_player: "&c✖ Вы были замучены {sender} на {duration}. Причина: {reason}\nСервер: {server}"
unmute_broadcast: "{prefix}&a❱ {sender} снял мут с игрока {target}."
mute_already: "{prefix}&cИгрок {target} уже замучен."
not_muted: "{prefix}&cИгрок {target} не замучен."
mute_expired: "&aВаш мут истёк. Теперь вы можете снова писать в чат."
tempmute_expired: "&aВаш временный мут истёк. Теперь вы можете снова писать в чат."

#Bans
ban_broadcast: "{prefix}&c❱ {sender} забанил {target} навсегда. &6Причина: {reason}"
ban_player: "&c✖ Вы были забанены навсегда.\nПричина: {reason}\nАдминистратор: {sender}\nСервер: {server}"
tempban_broadcast: "{prefix}&c❱ {sender} временно забанил {target} на {duration}. &6Причина: {reason}"
tempban_player: "&c✖ Вы были забанены на {duration}.\nПричина: {reason}\nАдминистратор: {sender}\nСервер: {server}"
unban_broadcast: "{prefix}&a❱ {sender} снял бан с игрока {target}."
ip_unbanned: "{prefix}&aIP-адрес {target} разбанен."
banip_broadcast: "{prefix}&c❱ {sender} забанил по IP игрока {target} навсегда. &6Причина: {reason}"
banip_player: "&c✖ Ваш IP-адрес заблокирован.\nПричина: {reason}\nАдминистратор: {sender}"

# Usage messages
history_usage: "{prefix}&cИспользование: /history <ник>"
inspect_usage: "{prefix}&cИспользование: /inspect <ник>"
altreason_usage: "{prefix}&cИспользование: /altreason <ID> <новая причина>"
droppunish_usage: "{prefix}&cИспользование: /droppunish <ID>"
usage_ban: "{prefix}&cИспользование: /ban <игрок> <причина> [-s]"
usage_tempban: "{prefix}&cИспользование: /tempban <игрок> <время> <причина> [-s]"
usage_unban: "{prefix}&cИспользование: /unban <игрок>"
usage_mute: "{prefix}&cИспользование: /mute <игрок> <причина> [-s]"
usage_tempmute: "{prefix}&cИспользование: /tempmute <игрок> <время> <причина> [-s]"
usage_unmute: "{prefix}&cИспользование: /unmute <игрок>"
usage_kick: "{prefix}&cИспользование: /kick <игрок> <причина> [-s]"
usage_banip: "{prefix}&cИспользование: /banip <игрок|ip> [причина] [-s]"
usage_dban: "{prefix}&cИспользование: /dban reload"
usage_unbanip: "{prefix}&cИспользование: /unbanip <игрок|ip>"

#Kick command
kick_broadcast: "{prefix}&6❱ {sender} кикнул {target}. &cПричина: {reason}"
kick_player: "&c✖ Вас кикнули.\nПричина: {reason}\nАдминистратор: {sender}"

# History command
history.header: "{prefix}&6=== История наказаний игрока {target} ==="
history.entry: " &7- &f#{id} &8| &f{date} &8| &c{type} &8| &7Статус: {status} &8| &7Сервер: {server} &8| &7Выдал: {issuer} &8| &7Причина: {reason}"
history.footer: "&7=== Всего записей: {total} ==="

# Check command
inspect.header: "{prefix}&6=== Активные наказания игрока {target} ==="
inspect.entry_ban: " &7- &cБан #{id} &8| &7Сервер: {server} &8| &7Причина: {reason} &8| &7До: {expires}"
inspect.entry_mute: " &7- &eМут #{id} &8| &7Сервер: {server} &8| &7Причина: {reason} &8| &7До: {expires}"
inspect.entry_permanent: " &7- &c{type} #{id} &8| &7Сервер: {server} &8| &7Причина: {reason} &8| &cНавсегда"
inspect.none: "&aУ игрока {target} нет активных наказаний."
inspect.footer: "&7=== Используйте /droppunish <ID> для удаления ==="

# Punlist command
punlist.header: "{prefix}&6=== Список всех наказаний (страница {page}/{total_pages}) ==="
punlist.entry: " &7- &f#{id} &8| &c{type} &8| &c{player} &8| &7Статус: {status} &8| &7Сервер: {server} &8| &7Выдал: {issuer} &8| &f{date} &8| &e{duration} &8| &7{reason}"
punlist.footer: "&7=== Используйте /punlist <страница> для навигации ==="
punlist.no_punishments: "{prefix}&cНаказаний не найдено."

# Presetlist command
presetlist.header: "{prefix}&6=== Доступные пресеты наказаний ==="
presetlist.entry: " &7- &f{name} &8| &c{type} &8| &7{reason} &8| &e{duration}"
presetlist.footer: "&7=== Используйте +название в команде ==="
presetlist.no_presets: "{prefix}&cПресеты не найдены."
```
{% endcode %}
{% endtab %}

{% tab title="Messages.yml (EN)" %}
Soon
{% endtab %}
{% endtabs %}

