---
description: >-
  In the limits.yml file, you can set limits for each group, including
  cooldowns, immunities, and maximum duration of punishment.
icon: do-not-enter
---

# Immunities and restrictions

{% tabs %}
{% tab title="limits.yml" %}
{% code lineNumbers="true" %}
```yml
groups:
  default:
    max_durations:
      ban: "1h"
      tempban: "1h"
      mute: "1h"
      tempmute: "1h"
      kick: "0"
      banip: "0"
    cooldowns: #in second
      ban: 600
      tempban: 600
      mute: 300
      tempmute: 300
      kick: 60
      banip: 0
    priority: 1
    immunities: [] #for someone types of punishments or bypass for all punishment types
  vip:
    max_durations:
      ban: "2h"
      tempban: "2h"
      mute: "2h"
      tempmute: "2h"
    cooldowns:
      ban: 600
      tempban: 600
      mute: 300
      tempmute: 300
    priority: 5
    immunities: []
  helper:
    max_durations:
      ban: "12h"
      tempban: "12h"
      mute: "6h"
      tempmute: "6h"
    cooldowns:
      ban: 300
      tempban: 300
      mute: 120
      tempmute: 120
      kick: 30
    priority: 20
    immunities: []
  moderator:
    max_durations:
      ban: "7d"
      tempban: "7d"
      mute: "7d"
      tempmute: "7d"
    cooldowns:
      ban: 60
      tempban: 60
      mute: 30
      tempmute: 30
      kick: 15
    priority: 50
    immunities: []
  admin:
    max_durations:
      ban: "0"
      tempban: "0"
      mute: "0"
      tempmute: "0"
      kick: "0"
      banip: "0"
    cooldowns:
      ban: 0
      tempban: 0
      mute: 0
      tempmute: 0
      kick: 0
      banip: 0
    priority: 100
    immunities:
      - bypass
  owner:
    max_durations:
      ban: "0"
      tempban: "0"
      mute: "0"
      tempmute: "0"
      kick: "0"
      banip: "0"
    cooldowns:
      ban: 0
      tempban: 0
      mute: 0
      tempmute: 0
      kick: 0
      banip: 0
    priority: 1000
    immunities:
      - bypass
```
{% endcode %}
{% endtab %}
{% endtabs %}

In this file, you can set your limits for each group (works only with LuckPerms). It is possible to set the maximum time of punishment for a certain type of punishment, you can set cooldowns for using commands (in seconds, no need to download additional plugins), set priorities (from lowest to highest, higher priority = higher rank), and also grant immunity from using a certain type of punishment against a group (or bypass for immunity from all kinds of punishments).
