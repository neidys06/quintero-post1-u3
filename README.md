# Post-contenido — Unidad 3: CSS3 Básico

## Descripción

Repositorio del laboratorio de la Unidad 3 de Programación Web — Séptimo Semestre.
Contiene dos partes: página de perfil con selectores CSS avanzados, Box Model y
posicionamiento (`parte-1-perfil-css3/`) y dashboard responsivo con CSS Grid y
Flexbox (`parte-2-dashboard-grid/`).

**Estudiante:** Neidys Mariana Quintero Carrillo

## Cómo visualizar el proyecto

1. Clonar el repositorio: `git clone https://github.com/neidys06/quintero-post1-u3.git`
2. Abrir la carpeta en Visual Studio Code
3. Clic derecho en `index.html` (de cada parte) → "Open with Live Server"

---

## Parte 1 — Página de perfil

Página de perfil personal que implementa selectores CSS avanzados, `box-sizing:
border-box`, posicionamiento (`fixed`/`relative`/`absolute`), una escala de
espaciado con Custom Properties (`--space-3xs` a `--space-3xl`), tipografía
fluida con `clamp()` en el nombre de perfil y formulario de contacto accesible
con estados `:focus` y validación `:invalid`. Ver `parte-1-perfil-css3/`.

### Box Model con `box-sizing: border-box`

Se verificó en DevTools que el Box Model global respeta `border-box`, por lo
que padding y border no aumentan el ancho/alto declarado de los elementos.

![Box model border-box](parte-1-perfil-css3/captures/chk1.png)

### Tarjeta de perfil — posicionamiento y tipografía fluida

El badge "CSS3" se posiciona con `absolute` respecto a `.avatar-wrapper`, que
actúa como contexto con `position: relative`. Esto se confirmó inspeccionando
el elemento en DevTools:

![Avatar wrapper position relative](parte-1-perfil-css3/captures/chk2-1.png)

Además, el nombre de perfil usa `clamp()` para escalar de forma fluida entre
375px y 1440px sin saltos abruptos. Se probó reduciendo el viewport con
DevTools:

![Vista responsiva 375px](parte-1-perfil-css3/captures/chk2-2.png)

### Vista completa — perfil y habilidades

La página completa en escritorio, mostrando el header fijo, la tarjeta de
perfil, y las etiquetas de habilidades con la nomenclatura BEM (`.skill-item--html`,
`.skill-item--css`, etc.), cada una con su color propio:

![Perfil completo escritorio](parte-1-perfil-css3/captures/chk3.png)

### Formulario de contacto — estados de foco accesibles

Al hacer clic en cualquier campo, el borde cambia de color y aparece el ring
de foco translúcido, cumpliendo con el requisito de accesibilidad del Paso 7:

![Formulario focus](parte-1-perfil-css3/captures/chk4.png)

### Validación `:invalid` — decisión de especificidad

Se eligió la **Estrategia A**: `input:invalid:not(:placeholder-shown)`.

Se optó por esta estrategia en lugar de `.contact-form input:invalid` porque
aprovecha la validación HTML5 nativa de los atributos `required`/`type="email"`
y solo se activa después de que el usuario haya escrito algo en el campo y
luego lo deje inválido, gracias a `:not(:placeholder-shown)`. Esto evita que
los tres campos requeridos (nombre, email, mensaje) aparezcan en rojo apenas
carga la página, que es el problema que habría que resolver aparte con la
Estrategia B.

En cuanto a especificidad: la regla de error tiene especificidad `0,0,2,0`
(dos pseudo-clases), mientras que `input:focus` del Paso 7 tiene `0,0,1,0`
(una pseudo-clase). Al ser más específica, la regla de error gana sobre el
borde por defecto sin necesitar `!important` ni depender del orden de
declaración en el archivo. Cuando un campo está enfocado *y* es inválido al
mismo tiempo, ambas reglas conviven sin conflicto real porque controlan
propiedades distintas: `:focus` gobierna el `box-shadow` (el ring azul) y la
regla de error gobierna el `border-color` (rojo).

La siguiente captura muestra el campo de correo con valor inválido, el borde
en rojo (`--color-error: #C62828`), y en el panel Styles de DevTools se
confirma que ninguna declaración usa `!important`:

![Estado invalid con color de error](parte-1-perfil-css3/captures/chk5.png)

---


