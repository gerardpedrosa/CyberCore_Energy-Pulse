# Casos de Prova

Aquest fitxer recull de forma resumida tots els casos de prova realitzats durant el projecte. La versió detallada amb explicacions es troba a [`docs/04_proves_i_depuracio.md`](../docs/04_proves_i_depuracio.md).

---

## Taula de casos de prova

| ID | Funcionalitat | Condicions inicials | Entrada | Resultat esperat | Resultat obtingut | Estat |
|---|---|---|---|---|---|---|
| CP-01 | Spawn del jugador | Joc iniciat | Prémer Play | Jugador apareix a SpawnLocation | ✅ Apareix correctament | Passat |
| CP-02 | HazmatBoots assignades | StarterPack configurat | Iniciar partida | Eina a l'inventari des del principi | ✅ Eina present | Passat |
| CP-03 | Respawn en morir | Jugador actiu | Eliminar la vida | Jugador reapareix en 3 segons | ✅ Respawn correcte | Passat |
| CP-04 | Barreres del mapa | Mapa carregat | Caminar cap a barrera | El jugador xoca, no passa | ✅ Barrera funcional | Passat |
| CP-05 | HUD visible | LocalScript actiu | Iniciar partida | HUD visible a pantalla | ✅ (després de correcció) | Passat |
| CP-06 | Zona d'aigua | Mapa carregat | Entrar a BaseplatePartAgua | Efecte específic (nedar/dany) | ⚠️ Sense efecte implementat | Pendent |

---

## Incidències

| ID | Descripció | Causa | Solució | Estat |
|---|---|---|---|---|
| INC-01 | HUD no apareixia en iniciar | Race condition: script s'executava abans del personatge | Afegir `CharacterAdded:Wait()` | ✅ Resolta |
| INC-02 | HazmatBoots desapareixien al fer respawn | Eina al Workspace en comptes de StarterPack | Moure eina a StarterPack | ✅ Resolta |
