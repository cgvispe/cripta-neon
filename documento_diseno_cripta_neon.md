# Documento de diseño — Cripta Neon (nombre provisional)

## 1. Visión general
Plataformas 2D con scroll multi-pantalla y verticalidad, estilo cartoon vectorial.
Cada mundo tiene su propia ambientación visual acorde a su nombre (ver tabla en
la sección 4) — no hay un estilo visual único para todo el juego. Combate con
salto-pisotón + inventario de 3 armas (principal / secundaria / especial)
intercambiables en tiempo real. Progresión por mapa de mundos, con jefe final
(de varias fases) por mundo y llave de color al derrotarlo.

Objetivo final de plataforma: publicación en Steam (motor recomendado para esa fase: Godot).
Fase actual: prototipo jugable en navegador (Phaser) para validar diseño con el equipo
(product manager + tester = vosotros dos).

## 2. Estado actual del prototipo (v5)
- Movimiento, salto, agachado, animaciones de correr/saltar/agachar/disparar.
- Salto-pisotón elimina cualquier enemigo de un golpe; disparo requiere varios
  impactos según la vida del enemigo.
- Inventario de 3 armas (1/2/3), secundaria desbloqueable, especial con cargas limitadas.
- 3 tipos de enemigo con IA distinta (patrulla + embestida, vuelo persecutorio,
  artillero acorazado a distancia).
- Corazones de vida (3), invulnerabilidad temporal tras golpe.
- Monedas: caen al eliminar enemigos, se quedan en el sitio, parpadean a los 3s,
  desaparecen a los 5s si no se recogen.
- Tienda desacoplada del nivel, accesible con la tecla M (menú), compra de corazón
  extra y recarga de arma especial.
- Nivel con scroll horizontal + una zona vertical (torre), portal de fin de nivel
  con desvanecido del personaje al completarlo.

## 3. Backlog de mecánicas (para próximos niveles, no para el nivel actual)
- **Enemigos y jefes tematicos por mundo**: cada mundo debe tener sus propios tipos de
  enemigo (aspecto, movimiento y ataques acordes a su ambientacion — p. ej. criaturas de
  arena en el Desierto, criaturas acuaticas en el Lago, criaturas de hielo en la Montaña),
  en vez de reutilizar los 3 enemigos genericos del Mundo 1. Los jefes de cada mundo
  deben seguir la misma logica tematica.
- **Coleccionables**
  - Ocultos en objetos rompibles (cofres, jarrones, muros agrietados).
  - Soltados por ciertos enemigos al morir (además de las monedas).
- **Elementos de nivel según mundo**
  - Plataformas móviles (raíles fijos, horizontales/verticales, algunas que caen al pisarlas).
  - Trampas mortales (pinchos, sierras, lava, hielo resbaladizo, según el mundo).
  - Lianas / cuerdas para trepar o balancearse (mundos de vegetación).
- **Puzzles y exploración**
  - Acertijos con mecánicas de "empujar objeto hasta una posición".
  - Objetos recogidos en un punto del nivel que activan algo en otro punto
    (palancas, llaves de puzzle, interruptores de presión).
  - Posible variante de laberinto en algún mundo (p. ej. Pantano Mágico o Mundo Sombrío).

## 4. Progresión: mapa de mundos
Cada mundo tiene 5 niveles. Al completar los 5, se accede al jefe final del mundo
(varias fases). Los niveles deben ser notablemente más largos que el nivel inicial
de referencia (Mundo 1 - Nivel 1), que se queda corto para el ritmo deseado.

**Niveles del Mundo 1 (Pradera Serena):**
| # | Nombre | Estado |
|---|--------|--------|
| 1 | Amanecer en la Pradera | Terminado |
| 2 | El Sendero de los Cofres | Terminado (plataformas moviles, cofres, pinchos) |
| 3 | La Colina del Viento | Terminado (subida vertical, laberinto con callejon sin salida, plataforma movida por el viento) |
| 4 | El Claro Encantado | Terminado (tramo largo de 6 plataformas magicas que aparecen y desaparecen, con aviso antes de desvanecerse) |
| 5 | Las Puertas del Castillo | Terminado (plataforma movil, plataformas magicas, palanca que abre la puerta final del castillo) |
| Jefe | El Guardian de la Pradera | Terminado (dos fases: garras cuerpo a cuerpo, y baculo magico a distancia al bajar de la mitad de vida) |

**Diseño del jefe (El Guardian de la Pradera):** un oso grande de color verde.
Combina dos tipos de ataque: zarpazos cuerpo a cuerpo con sus garras, y ataques a
distancia con un baculo de madera (posible ataque magico/proyectil). Encaja con el
combate de varias fases ya definido — por ejemplo, fase 1 solo garras, fase 2
añade ataques de baculo a distancia.

Acceso mediante tecla especial (a definir junto con el resto del menú). Cada mundo:
varios niveles + 1 jefe final con **varias fases** (cambia de ataque/patrón al
perder vida). Al derrotar al jefe se obtiene una llave de color única de ese mundo.

**Fase especial — laberinto de llaves**: al completar los 8 mundos principales
y reunir las 8 llaves, se accede a una fase de tipo laberinto en la que hay que
usar las llaves en una secuencia concreta para desbloquear, uno a uno, los 3
mundos extra (Mundo Sombrío, Mundo Castillo, Mundo Espacial).

**Pendiente de decidir** (para cuando podáis):
- Cómo se determina/comunica al jugador la secuencia correcta de llaves en el
  laberinto (¿pistas visuales en el propio laberinto?, ¿pistas repartidas por
  los 8 mundos principales?, ¿otra cosa?).

### Lista de mundos
| # | Mundo | Estilo visual | Notas de ambientación / mecánica especial (borrador) |
|---|-------|----------------|--------------------------------------------------------|
| 1 | Pradera Serena | Pradera: hierba, tierra, arbustos, cielo despejado | Mundo plantilla — en desarrollo |
| 2 | Tormenta en la Playa | Playa con cielo tormentoso, arena, palmeras | Rayos, viento, marea que sube y baja |
| 3 | Desierto Arenoso | Dunas, cactus, ruinas semienterradas | Arena movediza, tormentas de arena, poca visibilidad |
| 4 | Lago Siniestro | Aguas oscuras, juncos, niebla | Corrientes de agua, criaturas acuáticas |
| 5 | Bosque Frondoso | Vegetación densa, árboles altos, luz filtrada | Lianas, plataformas entre copas de árboles |
| 6 | Montaña Gélida | Nieve, roca, cuevas heladas | Hielo resbaladizo, ventiscas, caída de rocas |
| 7 | Pantano Mágico | Vegetación mágica, luces flotantes, barro | Veneno, laberintos, magia/hechizos ambientales |
| 8 | Volcán Candente | Roca volcánica, lava, cielo rojizo | Lava, plataformas que se derrumban, calor |
| E1 | Mundo Sombrío | Oscuridad, siluetas, tonos apagados | Visibilidad reducida, enemigos ocultos |
| E2 | Mundo Castillo | Piedra, vitrales, tapices | Trampas mecánicas, puzzles de palancas |
| E3 | Mundo Espacial | Estrellas, tecnología, ingravidez | Gravedad reducida, saltos más largos |

Nota: el estilo "gótico-medieval con toques futuristas" que usamos en el
prototipo actual queda libre para reasignarlo a uno de los mundos que mejor
encaje (por ejemplo, Mundo Castillo o Mundo Sombrío) en vez de a la Pradera Serena.

Cada mundo tendrá también su propia música y efectos de sonido (pendiente de
definir estilo/herramienta para audio).

## 5. Hoja de ruta sugerida
1. Cerrar el diseño del Mundo 1 (Pradera Serena) como plantilla: pulir mecánicas
   base, añadir 1-2 ejemplos de coleccionable oculto y una plataforma móvil,
   para probar el patrón antes de replicarlo.
2. Definir el sistema de mapa de mundos y menú (arte + navegación), y el
   propósito de las llaves.
3. Diseñar el primer jefe (Mundo 1) como plantilla de "combate de jefe".
4. Replicar la plantilla en los mundos 2-8 cambiando arte, enemigos y una
   mecánica especial por mundo.
5. Mundos extra (Sombrío, Castillo, Espacial) al final, como contenido avanzado.
6. Migración a Godot y preparación de la ficha de Steam cuando el diseño esté validado.
