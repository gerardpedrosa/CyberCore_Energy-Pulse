# ⚡ Energy Pulse
 
> Joc clicker de Roblox ambientat en una planta nuclear. Fes clic, acumula energia i millora el teu reactor.
 
---
 
## 📸 Captura del joc
 
![alt text](<Captura de pantalla 2026-05-29 221214.png>)
 
---
 
## 📖 Descripció
 
**Energy Pulse** és un joc clicker desenvolupat a Roblox on el jugador genera energia fent clic sobre un reactor nuclear. Amb l'energia acumulada pots comprar millores que augmenten la quantitat d'energia obtinguda per clic o la generen automàticament, creant un bucle de progrés constant.
 
L'objectiu és optimitzar al màxim la teva producció d'energia i desbloquejar totes les millores disponibles. Com més eficient siguis, més ràpid progressaràs.
 
---
 
## 🎮 Com es juga
 
1. **Fes clic** sobre l'objecte principal (el reactor) per generar energia.
2. **Acumula** prou energia per comprar millores a la botiga.
3. **Compra millores** que augmenten l'energia per clic o la produeixen automàticament.
4. **Repeteix** el cicle per continuar progressant i desbloquejar millores més potents.
---
 
## 🕹️ Controls
 
| Acció | Control |
|---|---|
| Generar energia | Clic esquerre sobre el reactor |
| Comprar millora | Clic sobre la millora a la botiga |
| Moure's pel mapa | `W` `A` `S` `D` |
| Girar càmera | Ratolí |
 
---
 
## 🔄 Bucle principal del joc
 
```
Fer clic → Obtenir energia → Comprar millores → Generar més energia → ...
```
 
---
 
## ⚙️ Millores disponibles
 
Les millores es compren amb l'energia acumulada i poden ser de dos tipus:
 
- **Millores de clic**: Augmenten l'energia obtinguda per cada clic.
- **Millores automàtiques**: Generen energia de forma passiva sense necessitat de fer clic.
---
 
## 🛠️ Tecnologies utilitzades
 
| Tecnologia | Descripció |
|---|---|
| **Roblox Studio** | IDE oficial per a jocs de Roblox |
| **LuaU (Luau)** | Llenguatge de programació |
| **ServerScriptService** | Lògica del servidor |
| **StarterPlayerScripts** | Interfície i controls del client |
| **ReplicatedStorage** | Dades compartides client/servidor |
 
---
 
 
## 📁 Estructura del repositori
 
```
energy-pulse/
│
├── README.md
├── src/
│   └── energy_pulse.rbxl
├── docs/
│   ├── 01_idea_i_abast.md
│   ├── 02_model_del_joc.md
│   ├── 03_entorn_i_prototip.md
│   ├── 04_proves_i_depuracio.md
│   ├── 05_millores.md
│   ├── 06_manual_usuari.md
│   └── 07_manual_tecnic.md
├── diagrames/
├── evidencies/
│   ├── 03/
│   ├── 04/
│   └── 05/

```
 
---
 
## 🚦 Estat del projecte
 
| Funcionalitat | Estat |
|---|---|
| Sistema de clics | ✅ Completat |
| Acumulació d'energia | ✅ Completat |
| Botiga de millores | ✅ Completat |
| HUD amb comptador d'energia | ✅ Completat |
| Generació automàtica passiva | ✅ Completat |
| Equipament (HazmatBoots) | ✅ Completat |
 
---
 
## 👤 Autor
 
**[Gerard Pedrossa Toribio]**
Curs: [Curs / Assignatura]
Any: 2024–2025
 
---
 
## 💭 Reflexió
 
Desenvolupant Energy Pulse he après a gestionar l'estat del joc amb variables persistents entre servidor i client, a sincronitzar dades de puntuació en temps real i a dissenyar un bucle de joc motivador basat en progrés constant. El repte principal va ser mantenir la coherència de les dades d'energia entre el servidor i la interfície del client sense desfasaments.