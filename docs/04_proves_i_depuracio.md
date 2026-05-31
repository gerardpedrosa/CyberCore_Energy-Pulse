# 04 – Proves i Depuració

## 1. Introducció

Aquest document recull les proves realitzades durant el desenvolupament del joc, els errors detectats i les solucions aplicades. L'objectiu de les proves era verificar que totes les funcionalitats principals del joc funcionaven correctament i detectar comportaments inesperats.

Les proves es van fer principalment amb el mode **Play** de Roblox Studio, i en alguns casos amb el mode **Test > Start Server** per simular múltiples jugadors.

---

## 2. Casos de prova

### Cas de prova 1: Aparició del jugador al mapa

| Camp | Detall |
|---|---|
| **Objectiu** | Verificar que el jugador apareix correctament al punt d'inici |
| **Condicions inicials** | Joc iniciat des de Roblox Studio amb Play |
| **Entrada** | Prémer Play (sense cap acció addicional) |
| **Resultat esperat** | El jugador apareix a l'SpawnLocation, dret i sense errors |
| **Resultat obtingut** |  El jugador apareix correctament a la posició definida |
| **Conclusió** | El spawn funciona correctament |

---

### Cas de prova 2: Funcionament de les HazmatBoots

| Camp | Detall |
|---|---|
| **Objectiu** | Verificar que l'eina Tool_HazmatBoots s'assigna al jugador en iniciar |
| **Condicions inicials** | Tool_HazmatBoots col·locada a StarterPack |
| **Entrada** | Iniciar partida i obrir l'inventari |
| **Resultat esperat** | El jugador té les HazmatBoots a l'inventari des del principi |
| **Resultat obtingut** |  L'eina apareix a l'inventari correctament |
| **Conclusió** | El sistema d'equipament inicial funciona |

---

### Cas de prova 3: Respawn del jugador

| Camp | Detall |
|---|---|
| **Objectiu** | Verificar que el jugador reapareix correctament després de morir |
| **Condicions inicials** | Jugador actiu al mapa |
| **Entrada** | Eliminar la vida del jugador (saltar fora del mapa o usar comanda /kill) |
| **Resultat esperat** | El jugador reapareix al SpawnLocation després del temps de respawn configurat |
| **Resultat obtingut** |  El jugador reapareix correctament |
| **Conclusió** | El sistema de respawn funciona |

---

### Cas de prova 4: Col·lisió amb les barreres del mapa

| Camp | Detall |
|---|---|
| **Objectiu** | Verificar que les barreres invisibles impedeixen sortir de les zones jugables |
| **Condicions inicials** | Jugador aparegut al mapa |
| **Entrada** | Intentar caminar cap a la zona restringida marcada amb "Delete If You Dont Need A Barrier" |
| **Resultat esperat** | El jugador xoca amb la barrera i no pot passar |
| **Resultat obtingut** |  La barrera funciona correctament com a límit físic |
| **Conclusió** | Les barreres limiten correctament les zones jugables |

---

### Cas de prova 5: Visualització del HUD

| Camp | Detall |
|---|---|
| **Objectiu** | Verificar que el HUDManager mostra correctament la informació a pantalla |
| **Condicions inicials** | LocalScript connectat amb el HUDManager actiu |
| **Entrada** | Iniciar la partida |
| **Resultat esperat** | El HUD és visible a pantalla amb la informació correcta |
| **Resultat obtingut** |  El HUD es carrega i és visible. En un cas inicial no es mostrava (veure incidència 1) |
| **Conclusió** | Après correcció, el HUD funciona correctament |

---

### Cas de prova 6: Comportament a la zona d'aigua

| Camp | Detall |
|---|---|
| **Objectiu** | Verificar el comportament del jugador en entrar a la zona BaseplatePartAgua |
| **Condicions inicials** | Jugador actiu, zona d'aigua present al mapa |
| **Entrada** | Caminar fins a la zona d'aigua |
| **Resultat esperat** | El jugador entra a l'aigua i neda o perd vida (segons la lògica implementada) |
| **Resultat obtingut** |  El jugador entra a l'aigua però no hi ha cap efecte específic programat |
| **Conclusió** | Cal implementar lògica per a la zona d'aigua (pendent de millora) |

---

## 3. Incidències detectades

### Incidència 1: El HUD no es mostrava en iniciar la partida

**Descripció**: En les primeres proves, el HUD gestionat per `HUDManager` no apareixia a pantalla quan el jugador s'unia.

**Com es va detectar**: En fer la prova 5, la pantalla quedava sense cap informació visible.

**Causa probable**: El `LocalScript` encarregat de crear la interfície s'executava abans que el jugador carregués completament al joc. Hi havia una condició de cursa (*race condition*) entre la càrrega del personatge i l'execució del script.

**Solució aplicada**: S'hi va afegir una espera amb `game.Players.LocalPlayer.CharacterAdded:Wait()` per assegurar que el personatge existís abans d'intentar modificar el HUD.

```lua
-- Fragment de codi corregit (LocalScript)
local player = game.Players.LocalPlayer
player.CharacterAdded:Wait() -- Esperar que el personatge estigui carregat
-- A partir d'aquí, crear i mostrar el HUD
```

**Verificació**: Després de la correcció, el HUD apareixia correctament des del primer moment.

---

### Incidència 2: Les HazmatBoots desapareixien al fer respawn

**Descripció**: Quan el jugador moria i reapareixia, les `Tool_HazmatBoots` no tornaven a l'inventari.

**Com es va detectar**: En la prova 3, es va comprovar que l'inventari quedava buit després del respawn.

**Causa probable**: L'eina estava col·locada directament al Workspace en comptes de a `StarterPack`. Les eines del Workspace s'eliminen en morir; les de `StarterPack` es tornen a donar automàticament.

**Solució aplicada**: Es va moure la `Tool_HazmatBoots` de la seva ubicació al `StarterPack`, assegurant que Roblox la redistribueixi automàticament en cada spawn.

```
Estructura correcta:
StarterPack/
└── Tool_HazmatBoots   ← S'assigna automàticament en cada spawn
```

**Verificació**: Després de moure l'eina, el jugador la rebia cada vegada que reapareixia.

---

## 4. Taula resum de proves

| # | Funcionalitat provada | Resultat | Incidència |
|---|---|---|---|
| 1 | Spawn del jugador |  Correcte | Cap |
| 2 | HazmatBoots assignades |  Correcte | Incidència 2 (resolta) |
| 3 | Respawn en morir |  Correcte | Cap |
| 4 | Col·lisió amb barreres |  Correcte | Cap |
| 5 | Visualització del HUD |  Correcte | Incidència 1 (resolta) |
| 6 | Zona d'aigua |  Parcial | Pendent de millora |

---

## 5. Evidències visuals

| A la carpeta evidències 04
