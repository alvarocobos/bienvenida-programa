# Página de bienvenida · Álvaro Cobos

Portal de bienvenida para clientes que **acaban de entrar** en la asesoría online.
No es una landing de venta: su único trabajo es que la persona sepa, desde el
primer segundo, qué tiene que hacer, en qué orden y qué puede esperar.

## Qué contiene

| Sección | Para qué sirve |
|---|---|
| Hero + panel de progreso | Da la bienvenida y muestra los 4 primeros pasos con su estado |
| Empieza aquí | Los 4 pasos en orden, con tiempo estimado, acción y casilla de «hecho» |
| Cómo funciona | Qué pasa hoy, en 48 h, la primera semana y cada domingo |
| Tus herramientas | WhatsApp, cuestionario, app de entrenamiento y guías |
| Vídeo de bienvenida | Mensaje personal + recordatorios clave |
| Cómo trabajamos juntos | Compromiso de ambas partes: qué pone cada uno |
| Dudas frecuentes | Acordeón con las 7 preguntas de la primera semana |
| Soporte | Contacto directo y tiempos de respuesta |

## Cómo personalizarla

Todo es un único archivo estático, `index.html`, sin dependencias ni compilación.

1. Abre `index.html`.
2. Busca `var ENLACES` (al principio del `<script>`, cerca del final).
3. Pega tus URLs entre las comillas:

```js
var ENLACES = {
  whatsapp:     'https://wa.me/34600000000',
  cuestionario: 'https://forms.gle/...',
  video:        'https://youtu.be/...',
  entrenamiento:'https://...',
  guias:        'https://...',
  instagram:    ''   // vacío = el icono se oculta
};
```

Los enlaces que dejes vacíos siguen llevando a la sección correspondiente de la
propia página, así que nunca queda un botón roto.

Otros datos editables directamente en el texto: el email (`alvarocobos1995@gmail.com`),
los tiempos de respuesta (`24 h`, `48 h`) y el día del check-in (`domingo`).

Para incrustar el vídeo en la página en lugar de abrirlo fuera, sustituye el
bloque `<a class="video-frame">` por el `<iframe>` que se indica en el comentario
que hay justo encima.

## Detalles técnicos

- HTML + CSS + JS sin dependencias. Se despliega en GitHub Pages tal cual.
- Tipografías: Inter e Instrument Serif (Google Fonts).
- Iconografía propia en un sprite SVG (`<symbol>`), sin librerías.
- El progreso de los 4 pasos se guarda en `localStorage` del dispositivo del
  cliente. Si el almacenamiento está bloqueado, la página funciona igual.
- Accesibilidad: contraste AA en todo el texto, foco visible, navegación por
  teclado, nombres accesibles en todos los controles y soporte de
  `prefers-reduced-motion`.
