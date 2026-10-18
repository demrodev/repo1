---
icon: layer-group
---

# Group\_priorities.yml

{% tabs %}
{% tab title="group_priorities.yml" %}
{% code lineNumbers="true" %}
```yml
# Group priorities, works with LuckPerms
# High number = high priority
# A player can only punish those whose priority is less than or equal to their own.
group_priorities:
  default: 1
  vip: 5
  creative: 5
  helper: 20
  moderator: 50
  admin: 99
  owner: 100
```
{% endcode %}
{% endtab %}
{% endtabs %}

