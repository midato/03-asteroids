# AGENTS.md

Clon de Asteroids: juego de canvas HTML5 en un solo archivo. Sin dependencias, sin bundler, sin tooling de tests/build/lint.

## Regla obligatoria

- Cada cambio al proyecto debe reflejarse en `AGENTS.md` (contexto/arquitectura) y en `README.md` (uso/funcionalidades).

## Ejecutar / verificar
- Abre `index.html` directamente en el navegador, o usa `npx serve .` y visita `http://localhost:3000`.
- No hay verificación automatizada. La única comprobación es manual: cargar la página, revisar que no haya errores en la consola de JS, y jugar un poco (cualquier cambio de estado: disparar, completar nivel, morir, reiniciar).

## Estructura
- `game.js` — toda la lógica del juego y el renderizado, cargado vía `<script src="game.js">`. No separar en módulos; mantenerlo en un solo archivo.
- `index.html` — elemento canvas y CSS inline. Los atributos del canvas `width="800" height="600"` deben estar sincronizados con las constantes `W`/`H` fijas al inicio de `game.js`. Sin bundler.

## Convenciones
- El repo está en español: README, textos del HUD y comentarios del código están en español (p. ej. `NIVEL`, `PUNTAJE`, `llama del propulsor`). Mantén el mismo idioma en textos de UI y comentarios nuevos.
- Las clases de entidades (`Bullet`, `Asteroid`, `Ship`, `Particle`) son dueñas de su `update(dt)`, `draw()` y bandera `dead`; el ciclo global de `update`/`draw` filtra los objetos muertos cada frame.
- Timestep: el `dt` se limita a 0.05s en el bucle de `requestAnimationFrame`.
- Los pools de objetos son arreglos simples reasignados después de filtrar (p. ej. `asteroids = asteroids.filter(...)`); mantén ese estilo.