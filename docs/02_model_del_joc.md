## Explicació del diagrama de classes

El diagrama de classes representa l’estructura del sistema del joc i les relacions entre les entitats principals.

Les classes definides són:

- **DadesJugador**: és l’element central del sistema i emmagatzema tota la informació del progrés del jugador, com l’energia, els renaixements i els multiplicadors.
- **NucliEnergia**: s’encarrega de la generació d’energia manual mitjançant la interacció del jugador.
- **Servidor**: representa els elements d’automatització que generen energia passiva amb el temps.
- **SistemaRebirth**: gestiona el sistema de reinici (rebirth) i aplica els multiplicadors permanents.

### Relacions entre classes

- DadesJugador es relaciona amb totes les altres classes, ja que és qui gestiona l’energia.
- NucliEnergia interactua amb el jugador per generar energia manual.
- Servidor genera energia de forma automàtica.
- SistemaRebirth modifica les dades del jugador quan es fa un reinici.

### Justificació del disseny

Aquest disseny separa les responsabilitats en diferents mòduls, cosa que facilita:
- L’organització del codi
- La reutilització de components
- El manteniment i l’escalabilitat del sistema

---

## Explicació del diagrama de comportament

El diagrama de comportament és un diagrama d’activitat que representa el bucle principal del joc (core loop).

### Flux del joc

1. El jugador prem la tecla E per interactuar amb el nucli.
2. Es genera energia manualment.
3. L’energia s’acumula en les dades del jugador.
4. El jugador pot comprar servidors.
5. Els servidors generen energia passiva de forma contínua.
6. El sistema comprova si s’ha arribat al llindar de Rebirth.
7. Si es compleix la condició:
   - S’activa el Rebirth
   - Es reinicia l’energia
   - S’aplica un multiplicador permanent
8. El cicle torna a començar amb més eficiència.

### Justificació

Aquest diagrama reflecteix el funcionament típic d’un joc incremental:
- Repetició d’accions
- Acumulació de recursos
- Progressió contínua
- Reinici amb millores

---

## Correspondència entre diagrames i codi futur

Els elements del diagrama es traduiran al codi en Roblox (Luau) de la següent manera:

- DadesJugador → sistema de leaderstats i mòduls de dades
- NucliEnergia → script amb ProximityPrompt per detectar la tecla E
- Servidor → scripts que generen energia passiva en intervals de temps
- SistemaRebirth → sistema que comprova el llindar i reinicia el progrés

### Exemples de correspondència

- afegirEnergia() → modificar leaderstats.Energy.Value  
- generarEnergiaPassiva() → bucle amb temps (wait o equivalent)  
- executarRebirth() → reinici de valors + aplicació de multiplicador