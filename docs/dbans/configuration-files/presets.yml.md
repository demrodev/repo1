---
icon: presentation-screen
---

# Presets.yml

{% tabs %}
{% tab title="presets.yml" %}
{% code lineNumbers="true" %}
```yml
#Presets are helpers for your moderators, so that you don't have to enter the time completely, you can specify the reason for the punishment as +preset_name.
#duration - sets the duration of the punishment, if duration is not specified, it means that the punishment is permanent.
#reason - sets the reason for the punishment. type - sets the type of punishment, either mute or ban.
#IMPORTANT! If the punishment does not have a duration set, you can only use the preset with the permanent punishment command /ban & /mute.
#If the duration is set, you can use it with temporary punishments such as /tempban & /tempmute
#You may add more!
presets:
  hacking:
    reason: "3.11 Using cheats"
    duration: "12h"
    type: "ban"
  projectHarm:
    reason: "3.10 Harm to the project"
    type: "ban"
  spam:
    reason: "2.2 Spam in chat"
    duration: "1h"
    type: "mute"
  toxic:
    reason: "2.5 Toxic behavour"
    duration: "30m"
    type: "mute"
  swear:
    reason: "2.6 Swear in chat"
    type: "mute"
  advertising:
    reason: "2.10 ADs"
    duration: "7d"
    type: "ban"
  caps:
    reason: "2.1 Too CapsLock"
    duration: "15m"
    type: "mute"
```
{% endcode %}
{% endtab %}
{% endtabs %}
