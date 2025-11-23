<div align="center">

<img src="https://i.imgur.com/tGFsdnA.png" alt="LSurvival Vault Logo" width="150"/>

# 📦 LSurvival Vault
### Enterprise-Grade Virtual Storage for RocketMod 4

![RocketMod](https://img.shields.io/badge/RocketMod-4-blue?style=flat-square&logo=csharp)
![Unturned](https://img.shields.io/badge/Game-Unturned-green?style=flat-square&logo=steam)
![Database](https://img.shields.io/badge/Database-LiteDB_v5-orange?style=flat-square)
![Performance](https://img.shields.io/badge/Performance-Zero_Allocation-blueviolet?style=flat-square)

<p align="center">
  <b>LSurvival Vault</b> is a high-performance virtualization plugin that replaces physical storage with <b>memory-injected inventories</b>.
  <br>
  Designed for high-population servers, it features asynchronous persistence, multi-language support, and zero-physics overhead.
</p>

---

</div>

## 📑 Table of Contents
- [Overview](#-overview)
- [Technical Refactoring](#-technical-refactoring)
- [Key Features](#-key-features)
- [Localization](#-localization)
- [Commands & Permissions](#-commands--permissions)
- [Configuration](#-configuration)
- [Acknowledgments](#-acknowledgments)

---

## 🔭 Overview

Standard storage plugins often instantiate physical prefabs under the map to trick the game into opening an inventory. This causes unnecessary collision checks (`BoxCollider`) and rendering overhead.

**LSurvival Vault** uses a **Ghost Identity Architecture**:
It injects a virtual asset identity (Asset ID 1283) into the network stream to trigger the native UI, while the storage object itself remains a "naked" GameObject in RAM without physics or mesh renderers.

> **Result:** 100% Native UI experience with **0% Physics Impact**.


---

## ✨ Key Features

| Feature | Description |
| :--- | :--- |
| **👻 Ghost Architecture** | Virtual inventories with no physical footprint, no collision, and no lag. |
| **🌍 Multi-Language** | Built-in support for **English (EN)**, **Spanish (ES)**, and **Portuguese (PT)**. |
| **⚡ Async Persistence** | Auto-saves run on background threads. You can save every **60 seconds** without lag. |
| **🛡️ Combat Locking** | automatically blocks vault access if the player is in PvP combat. |
| **💾 Atomic Database** | Powered by **LiteDB (NoSQL)** with WAL (Write-Ahead Logging) for data integrity. |
| **👮 Admin Tools** | Admins can force-open any vault (offline or online) and trigger emergency saves. |

---

## 🌍 Localization

Change the language of the entire plugin with a single configuration setting. No manual translation files needed.

Supported modes in `LSurvivalVault.configuration.xml`:
* `<Language>ES</Language>` (Spanish - Default)
* `<Language>EN</Language>` (English)
* `<Language>PT</Language>` (Portuguese)

---

## ⌨️ Commands & Permissions

### 👤 User Commands

| Command | Syntax | Description | Permission Node |
| :--- | :--- | :--- | :--- |
| **Open Default** | `/vault` | Opens the default vault (ID 1). | `lsurvival.vault.1` |
| **Open Specific** | `/vault <id>` | Opens a specific vault number. | `lsurvival.vault.<id>` |

### 🛡️ Admin Commands

| Command | Syntax | Description | Permission Node |
| :--- | :--- | :--- | :--- |
| **Inspect** | `/adminvault <player> <id>` | Force open any player's vault. | `lsurvival.admin` |
| **Emergency Save** | `/vaultsave` | Forces an immediate asynchronous save of all active sessions. | `lsurvival.admin` |

---
💖 Acknowledgments
Thanks to Midnight for pointing out the performance issue regarding the FixedUpdate loop. That specific insight led me to re-evaluate the code and implement the correct event-driven solution included in this version.
## ⚙️ Configuration

Recommended settings for production environments:

```xml
<LSurvivalVaultConfiguration>
    <Language>ES</Language>
    <StorageAssetId>1283</StorageAssetId>
    <AutoSaveIntervalSeconds>60</AutoSaveIntervalSeconds>
    <BlockInCombat>true</BlockInCombat>
    ...
</LSurvivalVaultConfiguration>


