# 📦 LSurvival Vault (RocketMod 4)

![LSurvival Vault Icon](https://i.imgur.com/tGFsdnA.png)



## 📖 Introducción

**LSurvival Vault**  en la gestión de inventarios virtuales. Diseñado desde cero para servidores **Survival Hardcore, PvP y RPG**

A diferencia de mis ideas Anteriores que "esconden" barricadas físicas debajo del mapa (causando lag, desync y glitches de duplicación), **LSurvival Vault** utiliza tecnología de **Inyección de Memoria (Mock Storage)**.

### ¿Por qué elegir LSurvival Vault?

| Característica | Plugins Tradicionales (Legacy) | ⚡ LSurvival Vault (Next-Gen) |
| :--- | :--- | :--- |
| **Tecnología** |  | **Virtual Mock Storage (RAM Injection)** |
| **Impacto FPS** |  **Nulo (0.00ms)** |
| **Riesgo de Dupeo**  **Imposible (Transacciones Atómicas)** |
| **Persistencia** | **Base de Datos LiteDB (NoSQL)** |
| **Escalabilidad** |  **Infinita (1 a 18+ Baúles Config)** |

---

## 🛠️ Arquitectura Técnica

### 1. Motor de Persistencia LiteDB 💾
Olvídate de la corrupción de datos. **LSurvival Vault** integra **LiteDB v5**, una base de datos NoSQL embebida de alto rendimiento.
* **Transacciones ACID:** Tus datos están seguros incluso si se corta la luz del servidor.
* **Auto-Guardado Silencioso:** El sistema realiza un "commit" de todos los baúles abiertos cada 60 segundos sin spamear la consola.
* **Organización Limpia:** La base de datos se genera ordenadamente en `/Plugins/LSurvivalVault/Data/`.

### 2. Sistema Anti-Combat Logging (PvP Inteligente) ⚔️
Para mantener la integridad del juego, el plugin incluye un **Combat Manager** nativo.
* **Filtro Inteligente:** Detecta exclusivamente daño provocado por **otros jugadores**. Si te ataca un zombie, un animal o te caes, el baúl sigue accesible (salvando tu vida).
* **Bloqueo PvP:** Si recibes daño de un jugador, el comando `/vault` se bloquea temporalmente para evitar el "Stashing" (guardar armas antes de morir).

### 3. Herramientas de Admin con "Memoria Compartida" 🧠
El comando `/adminvault` utiliza una técnica de inyección de dependencia avanzada.
* Si abres el baúl de un jugador que está conectado y mirando su caja, **ambos verán lo mismo en tiempo real**.
* Si tú mueves un item, desaparece de su pantalla al instante. Sin desincronización, sin copias fantasmas.

---

## 🎮 Comandos y Permisos

El sistema de permisos es **granular y dinámico**. Puedes monetizar o premiar cada nivel de baúl por separado.

### Comandos de Usuario

| Comando | Sintaxis | Descripción | Permiso |
| :--- | :--- | :--- | :--- |
| **/vault** | `/vault` | Abre tu baúl principal (Nivel 1). | `lsurvival.vault.1` |
| **/vault** | `/vault <id>` | Abre un baúl específico (ej: `/vault 5`). | `lsurvival.vault.<id>` |

> **Ejemplo:** Para que un VIP pueda abrir hasta el baúl 3, dale los permisos:
> * `lsurvival.vault.1`
> * `lsurvival.vault.2`
> * `lsurvival.vault.3`

### Comandos de Administración

| Comando | Sintaxis | Descripción | Permiso |
| :--- | :--- | :--- | :--- |
| **/adminvault** | `/adminvault <jugador> <id>` | Abre el baúl de CUALQUIER jugador (Online/Offline) para inspección, auditoría o recuperación de items. Sincronizado en tiempo real. | `lsurvival.admin` |

---

## ⚙️ Configuración Completa

El archivo `LSurvivalVault.configuration.xml` permite un control total sobre la experiencia de juego.

### 📐 Definición de Baúles (Scalability)
Define cuántos baúles existen y qué tamaño tiene cada uno. El plugin genera 18 por defecto con progresión RPG.

```xml
<Vaults>
  <VaultDefinition>
    <Id>1</Id>
    <Width>5</Width>
    <Height>5</Height>
  </VaultDefinition>
  
  <VaultDefinition>
    <Id>2</Id>
    <Width>8</Width>
    <Height>8</Height>
  </VaultDefinition>

  <VaultDefinition>
    <Id>18</Id>
    <Width>12</Width>
    <Height>14</Height>
  </VaultDefinition>
</Vaults>
