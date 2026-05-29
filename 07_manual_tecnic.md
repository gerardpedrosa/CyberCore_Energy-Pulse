# 07 – Manual Tècnic

## 1. Visió general del projecte

**Nuclear Plant Survival** és un joc de Roblox desenvolupat amb **Roblox Studio** i **LuaU**. El projecte segueix l'arquitectura client-servidor pròpia de Roblox, on existeix una separació clara entre la lògica que s'executa al servidor i la lògica que s'executa al client de cada jugador.

---

## 2. Estructura del projecte

L'estructura interna del joc dins Roblox Studio és la següent:

```
Game (DataModel)
│
├── Workspace/
│   ├── Baseplate                  ← Terra principal (Part)
│   ├── BaseplatePartAgua          ← Zona d'aigua (Part amb material Water)
│   ├── nuclear plant+             ← Model principal de l'escenari (Model)
│   ├── SpawnLocation              ← Punt d'aparició del jugador
│   ├── Camera                     ← Càmera principal del joc
│   └── Atmosphere                 ← Efecte d'atmosfera (bruma, ambient)
│
├── ServerScriptService/
│   ├── Script                     ← Script principal del servidor
│   └── HUDManager                 ← Gestió del HUD (crida al client via RemoteEvent)
│
├── StarterPack/
│   └── Tool_HazmatBoots           ← Eina assignada automàticament a cada spawn
│
├── StarterPlayerScripts/
│   └── LocalScript                ← Script del client (HUD, controls, càmera)
│
├── StarterCharacterScripts/
│   └── Script                     ← Scripts associats al personatge del jugador
│
├── ReplicatedStorage/
│   └── ModuleScript               ← Mòduls compartits entre servidor i client
│
├── Players/
│   └── (gestió automàtica de Roblox)
│
├── Lighting/
│   ├── BloomEffect                ← Efecte de llum bloom
│   ├── DepthOfFieldEffect         ← Efecte de profunditat de camp
│   └── NuclearWinterSky (config) ← Configuració del cel i l'ambient
│
└── Teams/ (si s'utilitzen equips)
```

---

## 3. Fitxers i components principals

| Fitxer / Component | Tipus | Responsabilitat |
|---|---|---|
| `Script` (ServerScriptService) | Server Script | Lògica principal del joc al servidor: gestió d'events, control del joc |
| `HUDManager` (ServerScriptService) | Server Script | Comunicació amb el client per actualitzar el HUD |
| `LocalScript` (StarterPlayerScripts) | Local Script | Mostra el HUD, gestiona la càmera i la interfície del client |
| `Script` (StarterCharacterScripts) | Script | Lògica associada directament al personatge (moviment, estats) |
| `ModuleScript` (ReplicatedStorage) | Module | Funcions i dades compartides accessibles tant des del servidor com del client |
| `Tool_HazmatBoots` (StarterPack) | Tool | Eina equipable del jugador, es dóna automàticament en cada spawn |
| `SpawnLocation` (Workspace) | Instance | Defineix on apareix el jugador. Configura el `RespawnTime` |
| `Lighting` | Service | Gestiona la il·luminació global, el cel i els efectes visuals |
| `Atmosphere` | Instance | Efecte de boira i ambient del mapa |

---

## 4. Arquitectura client-servidor

Roblox utilitza un model de xarxa on existeixen dos contextos d'execució:

```
┌─────────────────────────────┐      ┌──────────────────────────────┐
│         SERVIDOR            │      │          CLIENT               │
│  (ServerScriptService)      │◄────►│  (StarterPlayerScripts)       │
│                             │      │                               │
│  - Lògica del joc           │      │  - HUD i interfície           │
│  - Gestió de jugadors       │      │  - Controls del jugador       │
│  - Validació d'accions      │      │  - Càmera                     │
│  - HUDManager (emissor)     │      │  - LocalScript (receptor)     │
└─────────────────────────────┘      └──────────────────────────────┘
           ▲                                        ▲
           │         ReplicatedStorage              │
           └────────────────────────────────────────┘
                  (ModuleScripts compartits)
```

La comunicació entre servidor i client es fa a través de **RemoteEvents** i **RemoteFunctions** emmagatzemats a `ReplicatedStorage`.

---

## 5. Flux d'execució principal

```
1. El joc s'inicia → Roblox carrega el DataModel
2. El servidor executa els Scripts de ServerScriptService
3. Un jugador s'uneix → Players.PlayerAdded s'activa
4. El personatge es crea → CharacterAdded s'activa
5. Roblox assigna automàticament el contingut de StarterPack (Tool_HazmatBoots)
6. El client executa el LocalScript → crea el HUD
7. El jugador juga → el servidor valida accions
8. El jugador mor → respawn automàtic (3 segons) → torna al pas 4
```

---

## 6. Decisions tècniques rellevants

### 6.1 Separació client/servidor
S'ha optat per col·locar tota la lògica sensible (validació, gestió de vida, punts) al servidor per evitar que clients maliciosos puguin manipular l'estat del joc.

### 6.2 StarterPack per a les eines
L'eina `Tool_HazmatBoots` es col·loca a `StarterPack` i no al Workspace, perquè Roblox redistribueix automàticament el contingut del StarterPack a cada spawn, sense necessitat de codi addicional.

### 6.3 CharacterAdded per al HUD
El LocalScript espera l'event `CharacterAdded` abans de crear el HUD, evitant errors de *nil reference* quan el personatge no existeix encara.

### 6.4 RespawnTime
El temps de respawn s'ha configurat a **3 segons** a través del servei `Players.RespawnTime` per mantenir el joc dinàmic.

---

## 7. Com es podria ampliar el projecte

| Funcionalitat | Descripció tècnica |
|---|---|
| Sistema de puntuació | Afegir un `Leaderboard` amb `leaderstat` per mostrar punts per jugador |
| Zones tòxiques | Usar `BasePart.Touched` per detectar quan el jugador entra a zones perilloses i reduir-li la vida |
| Efectes de la zona d'aigua | Implementar lògica al `BaseplatePartAgua.Touched` per nedar o perdre vida |
| Sons ambientals | Afegir `Sound` instances al Workspace amb sons de sirena o ambient nuclear |
| Múltiples rondes | Implementar un sistema de rondes amb `TimerService` i gestió d'estats |
| Més eines | Afegir noves `Tool` al StarterPack amb efectes específics al mapa |
| Animacions personalitzades | Utilitzar `AnimationController` per a animacions específiques de les HazmatBoots |

---

## 8. Taula de relació fitxer–classe–responsabilitat

| Fitxer | Servei Roblox | Responsabilitat principal |
|---|---|---|
| Script principal | ServerScriptService | Lògica del servidor, events globals |
| HUDManager | ServerScriptService | Comunicació amb el HUD del client |
| LocalScript | StarterPlayerScripts | Interfície i controls del client |
| Script personatge | StarterCharacterScripts | Lògica del moviment i estat del personatge |
| ModuleScript | ReplicatedStorage | Funcions compartides |
| Tool_HazmatBoots | StarterPack | Eina equipable, assignada automàticament |

---

## 9. Evidències visuals

> 📸 **Captura 1**: Explorer de Roblox Studio mostrant l'estructura completa del DataModel.

> 📸 **Captura 2**: Codi del LocalScript amb la crida a `CharacterAdded:Wait()`.

> 📸 **Captura 3**: Configuració de `Players.RespawnTime` des del panel de propietats.

> 📸 **Captura 4**: Diagrama d'arquitectura client-servidor (pot ser el diagrama de la carpeta `/diagrames/`).

*Nota: Afegir les captures reals a `evidencies/captures/` i referenciar-les aquí.*
