---
icon: plug
---

# Usage API

### 🔌 Obtaining the API Instance

The API is accessed through the static `DBansProvider` class. Your plugin should depend on DBans (specify in `plugin.yml`).

{% tabs %}
{% tab title="Main.java" %}
{% code lineNumbers="true" %}
```java
import me.demro.dlibs.api.DBansAPI;
import me.demro.dlibs.api.DBansProvider;
import org.bukkit.Bukkit;
import org.bukkit.plugin.java.JavaPlugin;

public class MyPlugin extends JavaPlugin {
    private DBansAPI dbansAPI;

    @Override
    public void onEnable() {
        // DBans may take a few ticks to initialise its API
        Bukkit.getScheduler().runTaskLater(this, () -> {
            dbansAPI = DBansProvider.get();
            if (dbansAPI == null || !dbansAPI.isEnabled()) {
                getLogger().severe("DBans API is not available! Plugin disabled.");
                getServer().getPluginManager().disablePlugin(this);
                return;
            }
            // API is ready
        }, 2L);
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

Always check that `dbansAPI` is not null before using it.

### 🧩 API Interfaces

| Method                 | Return Type       | Text                           |
| ---------------------- | ----------------- | ------------------------------ |
| getPunishmentManager() | PunishmentManager | Manager for punishments        |
| getPlayerManager()     | PlayerManager     | Manager for player data        |
| getEventManager()      | EventManager      | Manager for event registration |
| isEnabled()            | boolean           | Whether DBans is enabled       |
| getVersion()           | String            | Version of DBans               |
| getPlugin()            | Plugin            | The DBans plugin instance      |

***

### 📋 PunishmentManager

Core management of punishments.

#### **1. Create a Punishment (Synchronous)**

{% code lineNumbers="true" %}
```java
String punish(UUID targetUuid, PunishmentType type, String reason, Long duration,
              UUID issuerUuid, String issuerName, String serverName)
        throws PlayerNotFoundException;
```
{% endcode %}

**Parameters:**

* `targetUuid` – UUID of the punished player.
* `type`  – `PunishmentType` (see below).
* `reason` – reason (non‑null).
* `duration` – duration in milliseconds, or `null` for permanent.
* `issuerUuid` – UUID of the issuer (use `UUID.nameUUIDFromBytes("CONSOLE".getBytes())` for console).
* `issuerName` – name of the issuer.
* `serverName` – server name (required, used for sync).

**Returns:** The ID of the created punishment (String).\
**Throws:** `PlayerNotFoundException` if the target player is not known to DBans.

**Example – permanent ban:**

{% code lineNumbers="true" %}
```java
try {
    String id = punishmentManager.punish(
        targetUUID,
        PunishmentType.BAN,
        "Spamming",
        null,
        consoleUUID,
        "Console",
        "lobby"
    );
    Bukkit.getLogger().info("Ban created with ID: " + id);
} catch (PlayerNotFoundException e) {
    // handle missing player
}
```
{% endcode %}

**Example – temporary mute (1 hour):**

{% code lineNumbers="true" %}
```java
long duration = TimeUnit.HOURS.toMillis(1);
String id = punishmentManager.punish(
    targetUUID,
    PunishmentType.MUTE,
    "Excessive caps",
    duration,
    issuerUUID,
    "Admin",
    "survival"
);
```
{% endcode %}

***

#### **2. Revoke a Punishment**

{% code lineNumbers="true" %}
```java
void revoke(String punishmentId, String issuerName, String reason)
        throws PunishmentNotFoundException;
```
{% endcode %}

**Parameters:**

* `punishmentId` – ID of the punishment to revoke.
* `issuerName` – name of who revokes it.
* `reason` – reason for revocation.

**Throws:** `PunishmentNotFoundException` if the ID does not exist.

**Example:**

{% code lineNumbers="true" %}
```java
try {
    punishmentManager.revoke("aBcDe", "Admin", "False positive");
} catch (PunishmentNotFoundException e) {
    // ID not found
}
```
{% endcode %}

***

#### **3. Get Punishment by ID**

{% code lineNumbers="true" %}
```java
Punishment getPunishment(String id);
```
{% endcode %}

Returns a `Punishment` object or `null` if not found. Searches across all tables (punishments, warnings, jail).

***

#### **4. Get Active Punishments of a Player**

{% code lineNumbers="true" %}
```java
List<Punishment> getActivePunishments(UUID targetUuid);
```
{% endcode %}

Returns a list of all currently active punishments for the player (including warnings and jail).

***

#### **5. Get Punishment History**

{% code lineNumbers="true" %}
```java
List<Punishment> getHistory(UUID targetUuid);
```
{% endcode %}

Returns a list of all punishments (active and inactive) for the player.

***

#### **6. Check if Player is Banned**

{% code lineNumbers="true" %}
```java
boolean isBanned(UUID targetUuid);
```
{% endcode %}

Returns `true` if the player has an active, non‑expired ban.

***

**7. Check if Player is Muted**

{% code lineNumbers="true" %}
```java
boolean isMuted(UUID targetUuid);
```
{% endcode %}

Returns `true` if the player has an active, non‑expired mute.

***

**8. Create Punishment Asynchronously**

{% code lineNumbers="true" %}
```java
CompletableFuture<String> punishAsync(UUID targetUuid, PunishmentType type, String reason,
                                      Long duration, UUID issuerUuid, String issuerName,
                                      String serverName);
```
{% endcode %}

Asynchronous version of `punish`. Recommended to avoid blocking the main server thread.

**Example:**

{% code lineNumbers="true" %}
```java
punishmentManager.punishAsync(targetUUID, PunishmentType.BAN, "Hacking", null,
                              consoleUUID, "Console", "lobby")
    .thenAccept(id -> Bukkit.getLogger().info("Async ban created: " + id))
    .exceptionally(e -> { /* handle error */ return null; });
```
{% endcode %}

***

### 🙋🏻‍♂️ PlayerManager

Provides player-related information.

**Methods**

{% code lineNumbers="true" %}
```java
String getPlayerIp(UUID playerUuid);
boolean hasImmunity(UUID playerUuid, PunishmentType type);
int getPriority(UUID playerUuid);
boolean canPunish(UUID issuerUuid, UUID targetUuid);
```
{% endcode %}

* `getPlayerIp` – returns the IP address stored for the player (may be null).
* `hasImmunity` – checks if the player has immunity against a specific punishment type.
* `getPriority` – returns the player's priority (higher values mean "more immune").
* `canPunish` – checks whether `issuerUuid` can punish `targetUuid` based on priority.

**Example:**

{% code lineNumbers="true" %}
```java
PlayerManager pm = api.getPlayerManager();
UUID target = player.getUniqueId();
if (pm.hasImmunity(target, PunishmentType.BAN)) {
    player.sendMessage("This player has ban immunity!");
}
if (!pm.canPunish(issuerUUID, target)) {
    issuer.sendMessage("You cannot punish this player (priority too high).");
}
```
{% endcode %}

***

### 📰 EventManager&#xD;

Allows you to register/unregister event listeners for punishment events.

{% code lineNumbers="true" %}
```java
void registerListener(Listener listener);
void unregisterListener(Listener listener);
void callEvent(PunishmentEvent event); // rarely used directly
```
{% endcode %}

**Example:**

{% code lineNumbers="true" %}
```java
api.getEventManager().registerListener(new MyListener());

// Later
api.getEventManager().unregisterListener(myListener);
```
{% endcode %}

***

### 📦 Data Types

#### `PunishmentType` (Enum)

| Value   | Description                   |
| ------- | ----------------------------- |
| BAN     | Permanent or temporary ban    |
| KICK    | Permanent or temporary mute   |
| MUTE    | Kick (always instant)         |
| IPBAN   | IP ban                        |
| JAIL    | Jail (temporary or permanent) |
| WARNING | Warning                       |

***

#### `Punishment` (Interface)

Represents a punishment and provides read‑only access to its fields.

| Method          | Return Type    | Description                                      |
| --------------- | -------------- | ------------------------------------------------ |
| getId()         | String         | Unique ID (5 characters)                         |
| getPlayerUuid() | UUID           | UUID of the punished player                      |
| getPlayerName() | String         | Name of the punished player                      |
| getIssuerUuid() | UUID           | UUID of the issuer                               |
| getIssuerName() | String         | Name of the issuer                               |
| getType()       | PunishmentType | Type of punishment                               |
| getReason()     | String         | Reason                                           |
| getStartTime()  | long           | Creation timestamp (ms)                          |
| getEndTime()    | Long           | Expiration timestamp (ms) or `null` if permanent |
| isActive()      | boolean        | Whether the punishment is still active           |
| isExpired()     | loolean        | Whether it has expired (if temporary)            |
| getServerName() | String         | Server name where it was issued                  |

***

### 🚨 Exceptions

All exceptions extend `APIException` (runtime).

* `PlayerNotFoundException` – thrown when a target player is not found in DBans.
* `PunishmentNotFoundException` – thrown when a punishment ID does not exist.

Always handle these exceptions in your code.

***

### 📡 Events (Listeners)

Events are fired when punishments are created, revoked, expire, or modified. All events extend `PunishmentEvent` and provide `getPunishment()`.

| Event Class           | When triggered                                                |
| --------------------- | ------------------------------------------------------------- |
| PunishmentCreateEvent | A new punishment is created (via command, API, or automation) |
| PunishmentRevokeEvent | A punishment is revoked (via command or API)                  |
| PunishmentExpireEvent | A temporary punishment expires naturally                      |
| PunishmentModifyEvent | The reason or duration of a punishment is changed             |

**Example listener**

{% code lineNumbers="true" %}
```java
import me.demro.dlibs.api.events.PunishmentCreateEvent;
import org.bukkit.event.EventHandler;
import org.bukkit.event.Listener;

public class MyListener implements Listener {
    @EventHandler
    public void onCreate(PunishmentCreateEvent event) {
        Punishment p = event.getPunishment();
        Bukkit.getLogger().info("New " + p.getType() + " for " + p.getPlayerName());
    }
}
```
{% endcode %}

Register it with `api.getEventManager().registerListener(new MyListener());`.

***

### 🧪 Complete Example Plugin

{% code lineNumbers="true" %}
```java
package com.example.integration;

import me.demro.dlibs.api.*;
import me.demro.dlibs.api.events.PunishmentCreateEvent;
import me.demro.dlibs.api.exceptions.PlayerNotFoundException;
import me.demro.dlibs.api.exceptions.PunishmentNotFoundException;
import org.bukkit.Bukkit;
import org.bukkit.entity.Player;
import org.bukkit.event.EventHandler;
import org.bukkit.event.Listener;
import org.bukkit.plugin.java.JavaPlugin;

import java.util.UUID;
import java.util.concurrent.TimeUnit;

public class IntegrationPlugin extends JavaPlugin implements Listener {
    private DBansAPI api;
    private PunishmentManager pm;
    private PlayerManager playerManager;

    @Override
    public void onEnable() {
        Bukkit.getScheduler().runTaskLater(this, () -> {
            api = DBansProvider.get();
            if (api == null || !api.isEnabled()) {
                getLogger().severe("DBans API not available. Disabling.");
                getServer().getPluginManager().disablePlugin(this);
                return;
            }
            pm = api.getPunishmentManager();
            playerManager = api.getPlayerManager();
            api.getEventManager().registerListener(this);
            getLogger().info("Integration with DBans established.");
        }, 2L);
    }

    @Override
    public void onDisable() {
        if (api != null) {
            api.getEventManager().unregisterListener(this);
        }
    }

    // Command to ban a player
    public void banPlayer(Player target, Player issuer, String reason) {
        UUID consoleUUID = UUID.nameUUIDFromBytes("CONSOLE".getBytes());
        try {
            String id = pm.punish(target.getUniqueId(), PunishmentType.BAN, reason, null,
                                  issuer.getUniqueId(), issuer.getName(), "lobby");
            issuer.sendMessage("Player banned. ID: " + id);
        } catch (PlayerNotFoundException e) {
            issuer.sendMessage("Player not found in DBans.");
        }
    }

    // Temporary mute for 1 hour
    public void tempMutePlayer(Player target, Player issuer, String reason) {
        try {
            long duration = TimeUnit.HOURS.toMillis(1);
            String id = pm.punish(target.getUniqueId(), PunishmentType.MUTE, reason, duration,
                                  issuer.getUniqueId(), issuer.getName(), "lobby");
            issuer.sendMessage("Muted for 1 hour. ID: " + id);
        } catch (PlayerNotFoundException e) {
            issuer.sendMessage("Player not found.");
        }
    }

    // Revoke by ID
    public void revokeById(String id, String revoker) {
        try {
            pm.revoke(id, revoker, "Revoked by admin");
            Bukkit.broadcastMessage("Punishment " + id + " revoked.");
        } catch (PunishmentNotFoundException e) {
            getLogger().warning("ID " + id + " not found.");
        }
    }

    // Event listener example
    @EventHandler
    public void onPunishmentCreate(PunishmentCreateEvent event) {
        Punishment p = event.getPunishment();
        getLogger().info("Punishment created: " + p.getId() + " for " + p.getPlayerName());
    }

    // Check ban status
    public boolean isBanned(UUID uuid) {
        return pm.isBanned(uuid);
    }

    // Print history
    public void printHistory(UUID uuid) {
        for (Punishment p : pm.getHistory(uuid)) {
            getLogger().info(p.getId() + " | " + p.getType() + " | " + p.getReason());
        }
    }
}
```
{% endcode %}

***

### ❓ Frequently Asked Questions

**Can I set my own `serverName`?**\
Yes, you pass it as a parameter in `punish`. It is mandatory and used for cross‑server synchronisation.

**What if I pass `duration = null`?**\
The punishment will be permanent (for types that support permanence: BAN, MUTE, IPBAN).

**Where do I get the punishment ID after creation?**\
The `punish` method returns the ID as a String. Save it for future operations.

**Does `revoke` work for WARNING and JAIL?**\
Yes, `revoke` works for all punishment types, including WARNING and JAIL. It will handle them correctly (remove from the appropriate table and broadcast messages).

**What about immunity and priority?**\
`PlayerManager` provides methods to check immunity and priority. You should check them before punishing a player to respect the permissions system.

**Is the API thread‑safe?**\
Most methods are synchronous and should be called on the main thread unless you use `punishAsync`. Use asynchronous calls for long‑running operations.

***

### 📬 Support

For issues, questions, or suggestions, please contact the DBans developer team or open an issue in the [dlibs repository](https://github.com/demrodev/dlibs).
