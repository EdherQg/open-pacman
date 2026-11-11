# Instrucciones del repositorio

- Responde al usuario en español. Conserva sin traducir los comandos, las rutas y los identificadores técnicos.

## Ejecución y verificación

- Abre `src/index.html` directamente en un navegador; no hace falta instalar dependencias, compilar ni iniciar un servidor de desarrollo. No hay manifiesto de paquetes ni herramientas configuradas para pruebas, análisis estático, formateo o comprobación de tipos.
- Con Node instalado, usa `node --check src/js/game.js` para comprobar la sintaxis de un archivo (sustituye la ruta por la de cada script modificado). Esto no verifica el comportamiento en el navegador.
- Comprobaciones básicas en el navegador: botón Start, movimiento con las flechas, puntos que suman 10, paso entre extremos del túnel, pérdida de vidas y reinicio tras ganar o perder. Revisa si hay errores en la consola del navegador.

## Arquitectura y restricciones

- `src/index.html` carga scripts clásicos que comparten variables globales en este orden: `maze.js` → `game.js` → `render.js` → `main.js`. Conserva ese orden de dependencias; no son módulos ES.
- `main.js` gestiona el DOM y la entrada del usuario, y llama a `update(game)` una vez por fotograma de animación. Las velocidades se expresan en celdas por fotograma, no en píxeles ni en función del tiempo transcurrido. Los giros, el consumo de puntos y las decisiones ante muros dependen de posiciones enteras de la cuadrícula; los cambios de velocidad deben conservar esa alineación.
- `MAZE`, en `maze.js`, es la plantilla original que no se modifica. `createGame()` clona sus filas en la cuadrícula mutable `game.grid`; dibuja desde esa cuadrícula para que los puntos consumidos desaparezcan y se restauren al reiniciar.
- Las celdas usan `0` para espacio vacío, `1` para muro, `2` para punto y `3` para puerta del recinto de fantasmas. Pac-Man no puede atravesar las puertas; los fantasmas sí. La fila del túnel y las posiciones iniciales de los personajes también se definen en `maze.js`.
- La geometría está vinculada entre varios archivos: el laberinto tiene 28×31 celdas, `TILE` en `render.js` vale 20, y tanto los atributos del canvas en `src/index.html` como `#game-wrap` en `src/css/style.css` miden 560×620. Actualízalos conjuntamente al cambiar las dimensiones.

## Flujos de especificación

- Para solicitudes de `/spec` o `/spec-impl`, lee `.agents/skills/spec/SKILL.md` o `.agents/skills/spec-impl/SKILL.md`, respectivamente. Las reglas de aprobación, creación de ramas y revisión de cada paso están allí; no las sustituyas por un flujo improvisado.
