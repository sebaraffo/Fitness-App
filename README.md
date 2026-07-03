# Space Fitness — App móvil (prototipo)

Prototipo navegable de la app del gimnasio **Space Fitness**: ejercicios por grupo muscular con sustitutivos (gimnasio / casa), rutinas por día, modo entrenamiento con temporizador y sonido, registro de pesos por fecha, membresía con bloqueo por cuota vencida, renovación por QR y panel de staff.

## Archivos

| Archivo | Qué es |
|---|---|
| `Space Fitness App.dc.html` | **Fuente principal** de la app (editá este) |
| `support.js` | Runtime que hace funcionar el `.dc.html` (no editar) |
| `sf-images.js` | Imágenes de grupos musculares embebidas como data-URIs |
| `assets/` | Logo, póster del login y imágenes generadas |
| `Space Fitness App (celular).html` | **Versión empaquetada en un solo archivo** — funciona sola, ideal para compartir o abrir en el celular |
| `Volt Gym App.dc.html` | Storyboard original (referencia de diseño) |

## Cómo correrlo local

Necesita servirse por HTTP (no abrir con doble click el `.dc.html`, porque el navegador bloquea los archivos locales). Con cualquiera de estas opciones desde la carpeta del proyecto:

```bash
# opción 1: Python (ya viene en Mac/Linux)
python3 -m http.server 8000

# opción 2: Node
npx serve .
```

Después abrí `http://localhost:8000/Space%20Fitness%20App.dc.html` en el navegador.

> La versión `Space Fitness App (celular).html` sí funciona con doble click — es un único archivo autocontenido.

## Datos útiles del demo

- **PIN del panel de staff:** `2468` (en Mi Cuenta → Panel de staff)
- El staff puede: marcar cuota pagada, simular cuota vencida y generar el QR de pago
- "Renovar cuota" abre el lector QR (pide permiso de cámara); el botón "Simular escaneo válido" completa el demo
- El estado (rutinas, registros, cuota) se guarda en `localStorage` del navegador

## Cómo editarlo

Todo el código de la app está en `Space Fitness App.dc.html`:
- El **HTML de las pantallas** está dentro de `<x-dc>…</x-dc>` (estilos inline)
- La **lógica** (navegación, estado, rutinas, timers, audio, QR) está en la clase `Component` dentro del `<script data-dc-script>`
- Los **datos de ejercicios** (grupos, sustitutivos, videos) están en `this.data` dentro de esa clase

Para desarrollo alcanza con servir la carpeta completa; no hace falta regenerar el bundle.

## Subirlo a GitHub

```bash
git init
git add .
git commit -m "Space Fitness app — prototipo inicial"
# creá el repo vacío en github.com y después:
git remote add origin https://github.com/TU_USUARIO/space-fitness-app.git
git branch -M main
git push -u origin main
```

Para publicarlo gratis con **GitHub Pages**: Settings → Pages → Deploy from branch → `main` / root. La app queda en `https://TU_USUARIO.github.io/space-fitness-app/Space%20Fitness%20App.dc.html`.

## Próximos pasos sugeridos (producción real)

- Backend (p. ej. Firebase/Supabase) para: socios, pagos, validación real del QR firmado, rutinas del profe
- Los videos de ejercicios son de muestra — reemplazar por los reales en `this.data` (campo `video`)
- Convertirla en PWA (manifest + service worker) para instalarla como app
