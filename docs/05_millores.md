# 05 – Millores

## 1. Introducció

Aquest document recull les millores aplicades al projecte després de tenir una primera versió funcional i d'haver realitzat les proves descrites al document 04. Cada millora descriu el problema o limitació que existia, la solució aplicada i l'efecte que ha tingut en el joc.

---

## 2. Millores aplicades

### Millora 1: Correcció del HUD (de buit a funcional)

**Problema anterior**: El HUD no apareixia en iniciar la partida perquè el `LocalScript` s'executava abans que el personatge del jugador estigués completament carregat. La pantalla quedava completament buida.

**Millora aplicada**: S'ha afegit una espera explícita al LocalScript per assegurar que el personatge existeixi abans de crear i mostrar la interfície.

**Part del projecte afectada**: `StarterPlayerScripts > LocalScript` (costat client).

**Canvi respecte a la versió anterior**:

| Abans | Després |
|---|---|
| HUD creat immediatament en executar el script | HUD creat after `CharacterAdded:Wait()` |
| La pantalla quedava buida al inici | El HUD apareix des del primer moment |

**Verificació**: Proves de spawn repetides confirmen que el HUD és sempre visible.

---

### Millora 2: Reubicació de les HazmatBoots al StarterPack

**Problema anterior**: Les `Tool_HazmatBoots` estaven col·locades al Workspace. Quan el jugador moria i reapareixia, no les recuperava, quedant sense equipament.

**Millora aplicada**: L'eina s'ha mogut al `StarterPack`, que és el servei de Roblox que redistribueix automàticament les eines a cada jugador en cada spawn.

**Part del projecte afectada**: Estructura del Workspace i del StarterPack.

**Canvi respecte a la versió anterior**:

```
ABANS:
Workspace/
└── Tool_HazmatBoots   ← Es perdia al morir

DESPRÉS:
StarterPack/
└── Tool_HazmatBoots   ← Es recupera a cada respawn
```

**Efecte**: El jugador sempre comença amb l'equipament correcte independentment de quantes vegades hagi mort.

---

### Millora 3: Ajust del temps de respawn

**Problema anterior**: El temps de respawn per defecte de Roblox (5 segons) era massa llarg per al ritme del joc, i els jugadors percebien una espera excessiva.

**Millora aplicada**: S'ha reduït el `RespawnTime` des dels serveis de `Players` per reduir el temps d'espera i millorar el flux de joc.

**Part del projecte afectada**: Configuració del servei `Players`.

**Canvi respecte a la versió anterior**:

| Paràmetre | Valor anterior | Valor nou |
|---|---|---|
| `RespawnTime` | 5 segons (default) | 3 segons |

**Efecte**: El joc és més dinàmic i el jugador passa menys temps esperant.

---

### Millora 4: Afegir l'efecte d'atmosfera NuclearWinterSky

**Problema anterior**: El mapa inicialment tenia una il·luminació per defecte de Roblox que no transmetia l'ambient post-apocalíptic / nuclear que es volia aconseguir.

**Millora aplicada**: S'ha configurat el servei `Lighting` amb l'efecte `NuclearWinterSky` i s'han ajustat els paràmetres d'ambient (ColorShift, Brightness, Atmosphere) per crear un cel grisenc i una atmosfera brumosa adequada per a l'escenari.

**Part del projecte afectada**: Servei `Lighting` del Workspace.

**Canvi respecte a la versió anterior**:

| Aspecte | Abans | Després |
|---|---|---|
| Cel | Default (blau clar) | NuclearWinterSky (grisenc) |
| Ambient | Neutre | Fosc, post-apocalíptic |
| Atmosfera | Cap | Enabled amb boira lleugera |

**Efecte**: El mapa transmet l'ambient esperat i millora la coherència estètica del joc.

---

### Millora 5: Organització dels scripts per separació client/servidor

**Problema anterior**: En la primera versió, part de la lògica del joc estava barrejada sense una separació clara entre el que ha d'executar el servidor i el que ha d'executar el client. Això generava comportaments imprevisibles.

**Millora aplicada**: S'ha reorganitzat el codi seguint el model client-servidor de Roblox:
- Els **Scripts** (server-side) s'han mogut a `ServerScriptService`.
- Els **LocalScripts** (client-side) s'han col·locat a `StarterPlayerScripts` i `StarterCharacterScripts`.
- Els **ModuleScripts** de codi compartit s'han posat a `ReplicatedStorage`.

**Part del projecte afectada**: Estructura de scripts de tot el projecte.

**Efecte**: Codi més net, menys errors de seguretat i lògica del servidor no accessible des del client.

---

## 3. Millores pendents

Si hi hagués més temps disponible, s'aplicarien les millores següents:

| Millora pendent | Justificació |
|---|---|
| Lògica per a la zona d'aigua | La `BaseplatePartAgua` ara no té cap efecte sobre el jugador |
| Sistema de puntuació i leaderboard | No hi ha un rànquing visible de punts entre jugadors |
| Sons ambientals | Afegir so de sirena o música de tensió per reforçar l'ambient |
| Animació en usar les HazmatBoots | L'eina no té animació d'ús |
| Missatge de fi de partida | No hi ha cap pantalla de fi o victòria implementada |
| Sistema de zones tòxiques | Es podria penalitzar el jugador per entrar a certes zones sense protecció |

---

## 4. Evidències visuals

| A la carpeta evidències 05
