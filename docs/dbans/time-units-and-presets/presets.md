---
icon: presentation-screen
---

# Presets

These are the rules of the server rules built into the plugin, in fact, it saves the server moderation from remembering the limits on certain punishments and as an example of remembering a rule clause.

{% code title="presets.yml" lineNumbers="true" %}
```yml
presets:
  hacking:
    reason: "Using illegal software/cheats"
    duration: "12h"
    type: "tempban"
    permission: "dbans.preset.hacking"
  spam:
    reason: "Spamming in chat"
    duration: "1h"
    type: "tempmute"
    permission: "dbans.preset.spam"
  toxic:
    reason: "Toxic wibes"
    duration: "30m"
    type: "tempmute"
    permission: "dbans.preset.toxic"
  advertising:
    reason: "Advertising"
    duration: "7d"
    type: "tempban"
    permission: "dbans.preset.advertising"
  caps:
    reason: "CapsLock"
    duration: "15m"
    type: "tempmute"
    permission: "dbans.preset.caps"
  jail_1h:
    reason: "Violation of the rules"
    duration: "1h"
    type: "jail"
    permission: "dbans.preset.jail_1h"
  warn_spam:
    reason: "Spamming in chat"
    duration: "30m"
    type: "warn"
    permission: "dbans.preset.warn_spam"
```
{% endcode %}

## Usage in basic commands

{% tabs %}
{% tab title="/ban" %}
```
/ban playerName +projectHarm
```

{% hint style="warning" %}
Also keep in mind that presets with duration can only apply to /temp, and without duration to permanent punishments /ban & /mute.
{% endhint %}
{% endtab %}

{% tab title="/tempban" %}
```
/tempban playerName +hacking
```

{% hint style="warning" %}
Also keep in mind that presets with duration can only apply to /temp, and without duration to permanent punishments /ban & /mute.
{% endhint %}
{% endtab %}

{% tab title="/mute" %}
```
/mute playerName +swear
```

{% hint style="warning" %}
Also keep in mind that presets with duration can only apply to /temp, and without duration to permanent punishments /ban & /mute.
{% endhint %}
{% endtab %}

{% tab title="/tempmute" %}
<pre><code><strong>/tempmute playerName +caps
</strong></code></pre>

{% hint style="warning" %}
Also keep in mind that presets with duration can only apply to /temp, and without duration to permanent punishments /ban & /mute.
{% endhint %}
{% endtab %}

{% tab title="/warn" %}
/warn playerName +warn\_spam

{% hint style="warning" %}
Also keep in mind that presets with duration can only apply to /temp, and without duration to permanent punishments /ban & /mute.
{% endhint %}
{% endtab %}

{% tab title="/jail" %}
/jail playerName +jail\_1h

{% hint style="warning" %}
Also keep in mind that presets with duration can only apply to /temp, and without duration to permanent punishments /ban & /mute.
{% endhint %}
{% endtab %}
{% endtabs %}

