---
description: List of commands and permissions for the plugin
icon: terminal
---

# Commands & Permissions

## Punishment commands

|                                      Command                                     |   Permission   |                          Description                          |
| :------------------------------------------------------------------------------: | :------------: | :-----------------------------------------------------------: |
|          /ban \<player> \<reason or +preset\_name> \[-s] \[server:lobby]         |    dbans.ban   |          Permanently blocks the player on the server          |
|  /tempban \<player> \<duration or +preset\_name> \<reason> \[-s] \[server:lobby] |  dbans.tempban |          Temporarily blocks the player on the server          |
|                              /unban \<player \| ID>                              |   dbans.unban  | Removes penalties in the form of temporary and permanent bans |
|                       /banip \<player or IP-address> \[-s]                       |   dbans.banip  |       Blocks all accounts associated with the IP address      |
|                          /unbanip \<player \| IP \| ID>                          |  dbans.unbanip |                   Removes the IP address ban                  |
|         /mute \<player> \<reason or +preset\_name> \[-s] \[server:lobby]         |   dbans.mute   |            Permanently restricts chat to the player           |
| /tempmute \<player> \<duration or +preset\_name> \<reason> \[-s] \[server:lobby] | dbans.tempmute |            Temporarily restricts chat to the player           |
|                             /unmute \<player \| ID>                              |  dbans.unmute  |           Removes the restriction on using the chat           |
|                         /kick \<player> \<reason> \[-s]                          |   dbans.kick   |      Throws the player off the server, works as a warning     |
|                    /warn \<player> \<duration> \<reason> \[-s]                   |   dbans.warn   |          Allows you to issue a warning to the player          |
|                              /unwarn \<player \| ID>                             |  dbans.unwarn  |                Allows you to remove the warning               |
|                    /jail \<player> \<duration> \<reason> \[-s]                   |   dbans.jail   |              Allows you to put the player in jail             |
|                             /unjail \<player \| ID>                              |  dbans.unjail  |            Allows you to get the player out of jail           |
|                                /warnlist \<player>                               | dbans.warnlist |        Allows you to see a list of all player warnings.       |

## Additional commands

|              Command              |     Permission    |                                                   Description                                                   |
| :-------------------------------: | :---------------: | :-------------------------------------------------------------------------------------------------------------: |
|   /altreason \<ID> \<newReason>   |  dbans.altreason  | Helps to correct the incorrectly stated reason for the punishment, without having to issue the punishment again |
|         /history \<player>        |   dbans.history   |                                     Displays the player's punishment history                                    |
|         /inspect \<player>        |   dbans.inspect   |                                  Displays the current punishments of the player                                 |
|              /punlist             |   dbans.punlist   |                                Displays a list of all punishments in the database                               |
|            /presetlist            |  dbans.presetlist |                                            Displays a list of presets                                           |
|      /droppunish \<ID \| all>     |  dbans.droppunish |     Deletes the line with the punishment and the ID from the database or drop all punishments from database     |
| /altduration \<ID> \<newDuration> | dbans.altduration |                                     Change duration for temporary punishment                                    |
|         /getuuid \<player>        |   dbans.getuuid   |                                        Get UUID of player (even offline)                                        |
|          /pstat \<player>         |    dbans.pstat    |                              Allows statistics on punishments, number and what kind                             |
|       /playerinfo \<player>       |  dbans.playerinfo |         Allows you to see the player's IP address, location by GeoIP, and a list of active punishments.         |

## GeoIP & Twin Accounts

<table><thead><tr><th align="center" valign="middle">Command</th><th align="center">Permission</th><th align="center">Description</th></tr></thead><tbody><tr><td align="center" valign="middle">/geoip &#x3C;player></td><td align="center">dbans.geoip</td><td align="center">Allows you to see the player's geolocation exactly to the city</td></tr><tr><td align="center" valign="middle">/twaccs</td><td align="center">dbans.twaccs</td><td align="center">Allows you to see the twin accounts associated with the account</td></tr><tr><td align="center" valign="middle">/bantwaccs</td><td align="center">dbans.bantwaccs</td><td align="center">Allows you to ban the player's twin accounts</td></tr></tbody></table>

## Admin commands

|    Command    |  Permission  |                  Description                 |
| :-----------: | :----------: | :------------------------------------------: |
| /dbans reload | dbans.reload | Reloads the settings and configuration files |
