# 03 – Entorn i Prototip

## 1. Entorn de desenvolupament

### IDE utilitzat: Roblox Studio

Per a aquest projecte s'ha utilitzat **Roblox Studio** com a entorn de desenvolupament principal. Es tracta de l'IDE oficial de Roblox, dissenyat específicament per crear jocs dins de la plataforma Roblox.

**Per què Roblox Studio?**
- És l'única eina oficial per desenvolupar jocs de Roblox.
- Integra editor visual 3D, editor de scripts Lua i simulador de joc en un sol programa.
- Permet provar el joc directament dins l'editor sense necessitat de publicar-lo.
- Disposa d'un sistema de serveis integrats (ServerScriptService, StarterPlayerScripts, etc.) que faciliten l'organització del codi.
- La comunitat i la documentació (DevHub) són molt àmplies.

### Llenguatge de programació: Lua (LuaU)

El llenguatge de programació utilitzat és **LuaU** (Luau), la variant de Lua adaptada per Roblox. És un llenguatge lleuger, de tipat opcional i molt integrat amb l'API de Roblox.

### Eines i extensions

| Eina / Servei | Funció |
|---|---|
| Roblox Studio | Editor i simulador principal |
| ServerScriptService | Conté els scripts del servidor (lògica del joc) |
| StarterPlayerScripts | Scripts que s'executen al client de cada jugador |
| StarterCharacterScripts | Scripts associats al personatge del jugador |
| Script (Server) | Scripts executats al costat del servidor |
| LocalScript (Client) | Scripts executats al costat del client |
| ModuleScript | Mòduls reutilitzables de codi |
| ContextActionService | Gestió d'accions i controls del jugador |

---

## 2. Com s'executa el projecte

### Per obrir i executar el joc en local:
1. Descarregar i instal·lar **Roblox Studio** des de [roblox.com/create](https://www.roblox.com/create).
2. Obrir el fitxer `copia_juego_rblx.rbxl` amb Roblox Studio.
3. Prémer el botó **Play** (▶) a la barra superior per simular el joc en local.
4. Per simular múltiples jugadors, utilitzar **Test > Start Server** i afegir clients.
5. També podem probarlo una vegada publicat.

### Estructura inicial del projecte dins Roblox Studio:

```
Workspace/
├── Baseplate              ← Terra principal del mapa
├── BaseplatePartAgua      ← Zona d'aigua / material específic
├── nuclear plant+         ← Model principal de la planta nuclear
├── SpawnLocation          ← Punt d'aparició del jugador
└── Atmosphere             ← Efecte d'atmosfera visual

ServerScriptService/
├── Script                 ← Script principal del servidor
└── HUDManager             ← Gestió de la interfície (HUD)

StarterPlayerScripts/
└── LocalScript            ← Lògica del costat del client

StarterCharacterScripts/
└── Script                 ← Scripts del personatge

ReplicatedStorage/
└── ModuleScript           ← Mòduls compartits servidor/client

StarterPack/
└── Tool_HazmatBoots       ← Eina/equipament del jugador
```

---

## 3. Primer prototip funcional

### Descripció del prototip

El primer prototip funcional va consistir en un mapa jugable bàsic amb:

- **Mapa de la planta nuclear**: L'escenari principal ja estava col·locat al Workspace, incloent el model de la planta i el terra amb zona d'aigua (`BaseplatePartAgua`).
- **Punt d'aparició**: El jugador apareix en una posició fixa (`SpawnLocation`) amb temps de respawn configurat.
- **Equipament inicial**: El jugador rep les `Tool_HazmatBoots` en iniciar la partida, que és l'únic equipament disponible en aquesta fase.
- **HUD bàsic**: El `HUDManager` ja estava connectat i mostrava informació bàsica a la pantalla del jugador.
- **Atmosfera**: L'efecte `NuclearWinterSky` estava configurat per donar ambient al joc.

### Què funcionava en el prototip

| Element | Estat |
|---|---|
| Mapa carregat i navegable |  Funcional |
| Spawn del jugador |  Funcional |
| Respawn en morir |  Funcional |
| Equipament inicial (Hazmat Boots) |  Funcional |
| HUD visible |  Funcional |
| Atmosfera visual |  Funcional |
| Barreres / zones restringides |  Col·locades al mapa |
| Laser Pointer (eina secundària) |  Parcialment implementat |

### Què faltava en el prototip

- Lògica de guanyar/perdre completament implementada.
- Sistema de puntuació connectat al HUD.
- Esdeveniments entre servidor i client completament testejats.
- Animacions personalitzades.
- So i música ambiental completa.

---

## 4. Evidències visuals

| A la carpeta evidències 03

---

## 5. Resum

| Pregunta | Resposta |
|---|---|
| IDE utilitzat | Roblox Studio |
| Perquè aquest entorn | És l'eina oficial i única per a Roblox, integra tot en un |
| Llenguatge | LuaU (Lua per a Roblox) |
| Com s'executa | Obrir el .rbxl i prémer Play a Roblox Studio |
| Estructura inicial | Workspace + ServerScriptService + StarterPack + Scripts |
| Primer prototip | Mapa jugable amb spawn, HUD i equipament bàsic |
| Parts funcionals | Mapa, spawn, respawn, HUD, equipament |
| Parts pendents | Sistema de punts complet, lògica de victòria/derrota |
