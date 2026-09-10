# Página de bienvenida · Método F90

**En producción:** https://bienvenida.alvarocobos.com

El dominio se configura con el archivo `CNAME` de la raíz más un registro DNS
`CNAME` de `bienvenida` apuntando a `alvarocobos.github.io`. Si alguna vez
cambia el dominio, hay que actualizar también las etiquetas `og:url`,
`og:image` y `twitter:image` de `index.html`: son URL absolutas.

Portal de bienvenida para clientes que **acaban de entrar** en la asesoría.
No es una landing de venta: su único trabajo es que la persona sepa, desde el
primer segundo, qué tiene que hacer, en qué orden y qué puede esperar.

## Estructura

Cinco bloques. Todo lo accionable está en el segundo.

| Bloque | Para qué sirve |
|---|---|
| Hero | Logo, bienvenida y un único botón: empezar |
| Empieza aquí | Los 4 pasos, cada uno autosuficiente: se lee, se hace y se marca sin salir |
| Dudas y detalles | Acordeón. Aquí vive todo el contexto que no hace falta para actuar |
| Soporte | Contacto directo y tiempos de respuesta |
| Cierre | Recordatorios y firma |

Los pasos llevan etiqueta «PASO N» bien visible, un botón ancho con instrucción
literal, y —en los que te sacan de la página— un aviso de «vuelve aquí al
terminar», que es donde más gente se pierde.

## Cómo se opera la asesoría (lo que refleja la página)

- **Horario de atención:** de lunes a sábado, respuesta en menos de 24 h.
- **Revisión semanal:** cada viernes, desde la app.
- **Ajustes:** el fin de semana, para que el lunes esté todo listo.
- **Plan de nutrición, entrenamiento, revisiones y seguimiento:** todo en la app.
- **Credenciales de la app:** las envía Álvaro por WhatsApp; el cliente no se registra solo.

## Cómo personalizarla

Todo es un único archivo estático, `index.html`, sin dependencias ni compilación.

Los enlaces se configuran en el objeto `ENLACES`, al principio del `<script>`:

```js
var ENLACES = {
  whatsapp:     '',   // ← PENDIENTE: 'https://wa.me/34600000000'
  cuestionario: 'https://forms.gle/TtWAcpyBurS5vMw39',
  video:        '',   // ← PENDIENTE: vídeo de bienvenida
  videoApp:     '',   // ← PENDIENTE: vídeo de cómo funciona la app
  ios:          'https://apps.apple.com/es/app/fuelier/id6766125388',
  android:      'https://play.google.com/store/apps/details?id=com.fuelier.app',
  comunidad:    'https://www.skool.com/metodo-f90-4470/about',
  instagram:    'https://www.instagram.com/_alvarotrainer/'
};
```

Los enlaces ya conocidos están además escritos directamente en el HTML, así que
funcionan aunque el JavaScript falle.

**La página se adapta a lo que esté configurado.** Mientras un enlace siga vacío,
en vez de dejar un botón muerto se anuncia el estado:

- **Sin `video` o sin `videoApp`:** ese reproductor muestra «Disponible muy
  pronto» y deja de ser pulsable. Cada uno va por su cuenta: se puede publicar
  uno y dejar el otro pendiente.
- **Sin `video`** además: el paso 1 se marca como pendiente, pierde su casilla
  y sale del recuento, de forma que el progreso puede llegar igualmente al
  100 % con los otros tres pasos.
- **Sin `whatsapp`:** el bloque de soporte pasa a ofrecer el email como canal
  principal, en lugar de un botón que promete WhatsApp y abre el correo.

En cuanto se pega la URL, todo vuelve solo a su estado normal. No hay que tocar
nada más.

Para incrustar el vídeo dentro de la página en vez de abrirlo fuera, sustituye
el bloque `<a class="video-frame">` por el `<iframe>` que indica el comentario
que hay justo encima.

## El logo

Está en `assets/`, en dos versiones y dos formatos:

- `logo-f90.webp` / `.png` — lockup completo (hero).
- `logo-f90-mark.webp` / `.png` — sólo «F90», recortado para que se lea en la
  cabecera y en el pie, donde el lockup entero quedaría ilegible.

Se generaron a partir de `LOGO F90.png` recortando el fondo de estudio y
reconstruyendo la transparencia, para que el resplandor cálido se integre con
el fondo oscuro en lugar de dejar un recuadro gris.

## Detalles técnicos

- HTML + CSS + JS sin dependencias. Se despliega en GitHub Pages tal cual.
- Tipografías: Inter e Instrument Serif (Google Fonts).
- Iconografía propia en un sprite SVG (`<symbol>`), sin librerías.
- El progreso de los 4 pasos se guarda en `localStorage` del dispositivo del
  cliente. Si el almacenamiento está bloqueado, la página funciona igual.
- Accesibilidad: contraste AA en todo el texto, foco visible, navegación por
  teclado, nombres accesibles en todos los controles y soporte de
  `prefers-reduced-motion` (todas las animaciones se desactivan).
- La página abre siempre por arriba. El script de la cabecera desactiva la
  restauración de scroll del navegador y limpia el ancla heredada de la visita
  anterior; tiene que seguir en `<head>`, porque al final del documento el
  navegador ya ha restaurado la posición y llega tarde.
