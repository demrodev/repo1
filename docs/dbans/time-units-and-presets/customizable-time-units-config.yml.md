---
icon: clock
---

# Customizable time units (config.yml)

You can change the localization of Time units depending on the case, number, etc.

Why do you need so many settings? This is due to the fact that the plugin may be used not only in English, but also in Russian, where the ending changes due to changes in cases and counts of units.

{% code title="config.yml" lineNumbers="true" %}
```yml
time_units:
  second:
    one: "second"
    few: "seconds"
    many: "seconds"
  minute:
    one: "minute"
    few: "minutes"
    many: "minutes"
  hour:
    one: "hour"
    few: "hours"
    many: "hours"
  day:
    one: "day"
    few: "days"
    many: "days"
```
{% endcode %}
