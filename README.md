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
| Empieza aquí | Los 7 pasos, cada uno autosuficiente: se lee, se hace y se marca sin salir |
| Dudas y detalles | Acordeón. Aquí vive todo el contexto que no hace falta para actuar |
| Soporte | Contacto directo y tiempos de respuesta |
| Cierre | Recordatorios y firma |

Los siete pasos alternan vídeo y acción:

1. Vídeo de bienvenida
2. Rellenar el cuestionario
3. Vídeo de cómo funciona la app
4. Descargar la app y registrarse — con el aviso ⚠️ de volver
5. Vídeo de cómo funciona la comunidad
6. Entrar en la comunidad
7. Vídeo de cómo será el seguimiento

Llevan etiqueta «PASO N» bien visible, un botón ancho con instrucción literal
y —en los que te sacan de la página— un aviso de «vuelve aquí al terminar»,
que es donde más gente se pierde.

Los pasos de vídeo declaran `data-needs="<clave>"`. Mientras esa clave de
`ENLACES` esté vacía, el paso se anuncia y sale del recuento, de modo que el
progreso puede llegar al 100 % con los pasos que sí se pueden hacer.

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
  video:            '',   // ← PENDIENTE: vídeo de bienvenida
  videoApp:         'https://youtu.be/7YInicFZphg',
  videoComunidad:   '',   // ← PENDIENTE: vídeo de cómo funciona la comunidad
  videoSeguimiento: '',   // ← PENDIENTE: vídeo de cómo será el seguimiento
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

- **Sin la URL de un vídeo:** ese reproductor muestra «Disponible muy pronto»
  y deja de ser pulsable, y su paso sale del recuento. Cada uno va por su
  cuenta: se pueden publicar unos y dejar otros pendientes.
- **Sin `whatsapp`:** el bloque de soporte pasa a ofrecer el email como canal
  principal, en lugar de un botón que promete WhatsApp y abre el correo.

En cuanto se pega la URL, todo vuelve solo a su estado normal. No hay que tocar
nada más.

## Los vídeos se ven dentro de la página

Basta con pegar la URL en `ENLACES`. Si es de YouTube —en cualquiera de sus
formas: `youtu.be/ID`, `watch?v=ID`, `embed/ID`, `shorts/ID`— la página lo
detecta sola y monta el reproductor ella misma:

- Pinta la **portada real** del vídeo (`maxresdefault`, y si ese vídeo no la
  tiene, `hqdefault`). La imagen es diferida: no se descarga hasta que el paso
  entra en pantalla, así los cuatro vídeos no pesan al abrir.
- Al pulsar, **el vídeo se reproduce ahí mismo**, sin salir de la guía. Esto es
  deliberado: mandar al cliente a YouTube a mitad del proceso es perderlo entre
  vídeos sugeridos. Se usa `youtube-nocookie.com` y el reproductor sólo se carga
  en ese momento, no antes.
- Con ctrl/cmd o rueda sigue abriéndose en otra pestaña, como cualquier enlace,
  y si el JavaScript falla el `href` original sigue llevando al vídeo.

Sobre la portada va un velo y el botón de play lleva halo propio, porque la
miniatura la elige el vídeo y puede venir clarísima: así el botón se recorta
siempre (medido: 3,4:1 en el peor caso, por encima del 3:1 que pide la norma).

Si algún vídeo se aloja fuera de YouTube, ese reproductor se queda como enlace
normal y se abre fuera; no hay que tocar nada.

## El retrato del hero

`assets/alvaro.webp` / `.jpg` — 400 × 400, recortado del original de Drive
(`alvaro.jpg`, 1024 × 1536) a un encuadre de retrato: cara centrada y algo de
hombro. Se muestra en círculo dentro del hero, entre el logotipo y el cintillo,
justo encima de un texto que habla en primera persona.

Al meterlo, el hero creció unos 120 px y el botón de empezar se salía de
pantalla en móviles pequeños y en portátil. En vez de encoger la foto se
recompactó el hero —el logotipo iba muy grande y la marca ya está en la
cabecera fija— y se añadió un `@media (max-height:740px)` para pantallas bajas.
Resultado: el botón se ve igual o mejor que antes de añadir la foto, en los
cinco tamaños medidos.

## El logo

En `assets/` hay también el wordmark de Skool en dos versiones:
`skool.*` con sus colores originales, y `skool-ink.*` teñido del color del
texto del botón. La que se usa es la segunda, dentro del botón del paso 6:
así se integra como un icono más en vez de parecer un logo pegado encima.

Titulares y botones van en versales por `text-transform`, no en el HTML: el
texto se mantiene legible en el código y el cambio es reversible desde el CSS.
Las preguntas del acordeón se quedan en caja baja a propósito: diez preguntas
en versales serían un muro.

El logotipo del Método F90 está en `assets/`, en dos versiones y dos formatos:

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
