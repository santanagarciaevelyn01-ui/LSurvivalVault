# 📦 LSurvival Vault (RocketMod 4)

![LSurvival Vault Icon](https://i.imgur.com/tGFsdnA.png)

# 📦 LSurvival Vault (RocketMod 4)

**Persistent Virtual Storage System for Unturned Servers.**

LSurvival Vault is an infrastructure plugin designed to manage additional virtual inventories for players. It uses a memory injection architecture and NoSQL databases to provide secure, scalable, and high-performance storage.

---

## 📋 Technical Specifications and Features

### 🛠️ Storage Architecture (Mock Storage)
The system generates virtual storage containers directly in the server's RAM using dependency injection.

* **In-Memory Operation:** It does not instantiate physical objects (barricades) in the game world, eliminating collisions and unnecessary rendering.

* **Synchronization:** The virtual container dynamically positions itself over the player to comply with the server's distance validations.

### 💾 Data Persistence (LiteDB)
The plugin replaces flat file storage with **LiteDB v5**, a transactional embedded database.

* **Data Integrity:** Uses atomic transactions for read/write operations.

* **Auto-Save:** Executes an automatic save cycle every 60 seconds (configurable) to dump data from RAM to disk, minimizing data loss in the event of server interruptions.

* **Unified Structure:** All data is centralized in a single database file (`LSurvivalVault.db`) located in the plugin's `Data` folder.

### ⚔️ Combat Management (PvP Manager)
Integrates a damage event monitor to regulate storage access during combat situations.

* **Source Detection:** Specifically identifies damage from other players (PvP), ignoring environmental or zombie damage.

* **Temporary Lock:** Prevents the opening command from being executed for a configurable period of time after taking damage.

### 👮 Real-Time Administration
Tools for inventory management and auditing by administrative staff.

* **Remote Inspection:** Allows opening any player's inventory, regardless of whether they are online or offline.

* **Shared Memory:** If an administrator opens the vault of a player who is actively using it, both clients share the same memory instance, allowing real-time modifications to be viewed.

### 📈 Scalability (Multi-Vault System)
The system supports configuring multiple storage instances per player.

* **Dynamic Capacity:** Allows defining up to **18 independent vaults**.

* **Customizable Dimensions:** Each vault ID can have a unique grid size (Width x Height), configured from the XML file.

---

## 📜 Commands and Permissions

### User

| Command | Syntax | Description | Required Permission |

| :--- | :--- | :--- | :--- |

**/vault** | `/vault` | Accesses the default vault (ID 1). | `lsurvival.vault.1` |

**/vault** | `/vault [id]` | Accesses a specific vault by its number. | `lsurvival.vault.[id]` |

> **Note:** Permissions follow the format `lsurvival.vault.<number>`. Example: `lsurvival.vault.5`.

### Administration

| Command | Syntax | Description | Required Permission |

| :--- | :--- | :--- | :--- |

**/adminvault** | `/adminvault [player] [id]` | Opens the specified vault of the target player for management. | `lsurvival.admin` |

---

## ⚙️ Configuration (XML)

The `LSurvivalVault.configuration.xml` file controls the plugin's operational parameters.

### Vault Definitions
List that defines the physical properties of each available vault.

```xml
<Vaults> 
<VaultDefinition> 
<Id>1</Id> 
<Width>5</Width> <Height>5</Height> </VaultDefinition> 

<VaultDefinition> 
<Id>2</Id> 
<Width>8</Width> 
<Height>8</Height> 
</VaultDefinition> 

</Vaults>
````

### System Parameters

````xml
<BlockInCombat>true</BlockInCombat> <CombatCooldownSeconds>30</CombatCooldownSeconds> <AutoSaveIntervalSeconds>60</AutoSaveIntervalSeconds> <StorageAssetId>1283</StorageAssetId> ```

---

## 📥 Guide Deployment

For proper installation in a RocketMod 4 production environment:

1. **Dependencies:**

* The plugin requires the **`LiteDB.dll`** library (Version 5.0.x for .NET 4.6.1).

* Required location: `/Libraries` folder of the Rocket instance.

2. **Plugin Installation:**

* The `LSurvivalVault.dll` file in the `/Plugins` folder.

3. **Initialization:**

* Upon startup, the plugin will automatically generate the following folder structure:

* Configuration: `/Plugins/LSurvivalVault/`

* Database: `/Plugins/LSurvivalVault/Data/LSurvivalVault.db`
````
````
