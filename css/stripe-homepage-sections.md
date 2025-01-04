# Stripe Homepage Sections

## Estructura Base en HTML

Esta es una estructura base utilizada en varias secciones de la página de Stripe.

```html
<section class="Section">
  <div class="Section__masked">
    <div class="Section__backgroundMask">
      <div class="Section__background">
        <!-- Material de fondo -->
      </div>
    </div>
    <div class="Section__container">
      <div class="Section__layoutContainer">
        <div class="Section__layout">
          <!-- Contenido -->
        </div>
      </div>
    </div>
  </div>
</section>
```

La clase `.Section` puede incluir otras clases complementarias como:

- `.Section--hasGuides`
- `.Section--angleTop`: Aplica propiedades CSS para agregar un ángulo en la parte superior de la sección.
- `.Section--angleBottom`: Aplica propiedades CSS para agregar un ángulo en la parte inferior de la sección.
- `.Section--paddingNormal`: Establece un padding estándar para la sección.

> **Nota:** Más detalles sobre estas clases serán añadidos más adelante.

### Background

Stripe siempre utiliza un elemento separado con la clase `.Section__background` para el fondo y los adornos. Este elemento se encuentra dentro de `.Section__backgroundMask`.

`.Section__backgroundMask` usa para posicionar el fondo y los adornos de la sección.

## CSS

### Section namespace

Antes de desglosar el CSS de la sección, es importante tener en cuenta el uso de variables CSS definidas en el HTML. Estas variables son:

```css
html {
  --gutterWidth: 16px;
  --angleNormal: -6deg;
  --angleNormalSin: 0.106;
  --columnPaddingNormal: 16px;
  --windowWidth: calc(100vw - var(--scrollbarWidth));
  --layoutWidth: calc(var(--windowWidth) - var(--gutterWidth) * 2);
  --layoutWidthMax: 1080px;
}
```

La variable `--angleNormalSin` representa la tangente del ángulo `6deg`.

---

Ahora veamos la declaración CSS para la clase `.Section`:

```css
.Section {
  --sectionAngleSin: var(--angleNormalSin);
  --sectionAngle: 0;
  --sectionPaddingSmallMax: 110;
  --sectionPaddingXSmallMax: 72;
  --sectionPaddingMin: 72;
  --sectionPaddingMax: var(--sectionPaddingNormalMax);
  --sectionPaddingTopMax: var(--sectionPaddingMax);
  --sectionPaddingBottomMax: var(--sectionPaddingMax);
  --sectionMarginTop: 0;
  --sectionMarginBottom: 0;
  --sectionAngleHeight: calc(var(--windowWidth) * var(--sectionAngleSin));
  --sectionAnglePaddingBaseMin: 100;
  --sectionAnglePaddingBaseMax: var(--sectionPaddingMax);
  --sectionAnglePaddingTopBaseMax: var(--sectionAnglePaddingBaseMax);
  --sectionAnglePaddingBottomBaseMax: var(--sectionAnglePaddingBaseMax);
  --sectionAngleMaxHeight: none;
  --sectionOverflow: hidden;
  --sectionTransformOrigin: 100% 0;
  --sectionBackgroundOverflow: visible;
  position: relative;
  z-index: 1;
  margin-top: var(--sectionMarginTop);
  margin-bottom: var(--sectionMarginBottom);
  color: var(--textColor);
  scroll-margin-top: calc(
    var(--fixedNavHeight) + var(--fixedNavSpacing) - var(--sectionPaddingTop)
  );
}
```

Puntos clave:

- En esta parte, se definen las variables CSS que se usarán en la sección. Estas variables son clave para calcular el padding, el margen, los ángulos (superiores e inferiores), entre otras cosas. Las propiedades CSS aplicadas a `.Section` afectan tanto a `.Section__layout` como a `.Section__background`.
- El `z-index: 1` hace que la siguiente sección este por encima de la anterior, lo que oculta el skew del background en la caso de tener ángulo.

Además, se declara lo siguiente:

```css
.Section {
  --sectionPaddingNormalMax: 128;
}
```

Esto agrega una variable CSS para definir el valor máximo del padding, utilizado tanto para el padding superior como inferior.

A continuación, se presentan las variables CSS calculadas para el padding de la sección, tanto con como sin ángulos.

```css
.Section {
  --sectionAnglePaddingTopBase: calc(
    var(--sectionAnglePaddingBaseMin) * 1px +
      (var(--sectionAnglePaddingTopBaseMax) - var(--sectionAnglePaddingBaseMin)) *
      (var(--windowWidth) / 737 - 0.50882px)
  );
  --sectionAnglePaddingBottomBase: calc(
    var(--sectionAnglePaddingBaseMin) * 1px +
      (
        var(--sectionAnglePaddingBottomBaseMax) -
          var(--sectionAnglePaddingBaseMin)
      ) * (var(--windowWidth) / 737 - 0.50882px)
  );
  --sectionPaddingTopGutterWidth: var(--gutterWidth);
  --sectionAnglePaddingTop: calc(
    var(--sectionAngleHeight) - var(--sectionAngleSin) *
      var(--sectionPaddingTopGutterWidth) + var(--sectionAnglePaddingTopBase)
  );
  --sectionAnglePaddingBottom: calc(
    var(--sectionAngleHeight) - var(--sectionAngleSin) * var(--gutterWidth) +
      var(--sectionAnglePaddingBottomBase)
  );
  --sectionPaddingTop: calc(
    var(--sectionPaddingMin) * 1px +
      (var(--sectionPaddingTopMax) - var(--sectionPaddingMin)) *
      (var(--windowWidth) / 737 - 0.50882px)
  );
  --sectionPaddingBottom: calc(
    var(--sectionPaddingMin) * 1px +
      (var(--sectionPaddingBottomMax) - var(--sectionPaddingMin)) *
      (var(--windowWidth) / 737 - 0.50882px)
  );
}
```

#### Notas sobre los valores:

- `737px`: Representa la diferencia entre el breakpoint mínimo (`375px`) y el máximo (`1112px`).
- `0.50882px`: Ajuste para garantizar un cálculo preciso en el límite inferior (`375px`). Es lo que resulta de dividir `375px/737px`

### Descripción de las variables CSS:

- `--sectionAnglePaddingTopBase`: Calcula un valor intermedio entre el padding mínimo y máximo para el padding superior (de 375px a 1112px).
- `--sectionAnglePaddingBottomBase`: Calcula un valor intermedio entre el padding mínimo y máximo para el padding inferior.
- `--sectionAnglePaddingTop`: Calcula el padding superior considerando el ángulo.
- `--sectionAnglePaddingBottom`: Calcula el padding inferior considerando el ángulo.
- `--sectionPaddingTop` y `--sectionPaddingBottom`: Calculan el padding superior e inferior sin tener en cuenta el ángulo.

Cuando la pantalla es más pequeña que 375px, estas son las variables CSS computadas:

```css
@media (max-width: 375px) {
  .Section {
    --sectionAnglePaddingTopBase: calc(var(--sectionAnglePaddingBaseMin) * 1px);
    --sectionAnglePaddingBottomBase: calc(
      var(--sectionAnglePaddingBaseMin) * 1px
    );
    --sectionPaddingTop: calc(var(--sectionPaddingMin) * 1px);
    --sectionPaddingBottom: calc(var(--sectionPaddingMin) * 1px);
  }
}
```

Esto simplemente se encarga de que se mantenga le padding mínimo para cada una de las estructuras (con ángulo o sin ángulo).

Y cuando es mayor a 1112px:

```css
@media (min-width: 1112px) {
  .Section {
    --sectionAnglePaddingTopBase: calc(
      var(--sectionAnglePaddingTopBaseMax) * 1px
    );
    --sectionAnglePaddingBottomBase: calc(
      var(--sectionAnglePaddingBottomBaseMax) * 1px
    );
    --sectionPaddingTop: calc(var(--sectionPaddingTopMax) * 1px);
    --sectionPaddingBottom: calc(var(--sectionPaddingBottomMax) * 1px);
  }
}
```

Y luego de `1112px` se debe mantener el padding máximo (con ángulo o sin ángulo)

#### Nota

Se podria usar `clamp()` para evitar usar media queries

```css
.Section {
  --sectionAnglePaddingTopBase: clamp(
    var(--sectionAnglePaddingBaseMin) * 1px,
    5.3596rem + 3.7992vw,
    var(--sectionAnglePaddingTopBaseMax) * 1px
  );
  --sectionAnglePaddingTopBase: clamp(
    var(--sectionAnglePaddingBaseMin) * 1px,
    5.3596rem + 3.7992vw,
    var(--sectionAnglePaddingBottomBaseMax) * 1px
  );
  --sectionPaddingTopGutterWidth: var(--gutterWidth);
  --sectionAnglePaddingTop: calc(
    var(--sectionAngleHeight) - var(--sectionAngleSin) *
      var(--sectionPaddingTopGutterWidth) + var(--sectionAnglePaddingTopBase)
  );
  --sectionAnglePaddingBottom: calc(
    var(--sectionAngleHeight) - var(--sectionAngleSin) * var(--gutterWidth) +
      var(--sectionAnglePaddingBottomBase)
  );
  --sectionPaddingTop: clamp(
    var(--sectionPaddingMin) * 1px,
    5.3596rem + 3.7992vw,
    var(--sectionPaddingTopMax) * 1px
  );
  --sectionPaddingBottom: clamp(
    var(--sectionPaddingMin) * 1px,
    5.3596rem + 3.7992vw,
    var(--sectionPaddingBottomMax) * 1px
  );
}
```

### Angle Top/Bottom

Cuando se usan clases como `.Section--angleTop` o `.Section--angleBottom`, estas agregan padding con ángulo a la sección.

```css
.Section--angleTop {
  --sectionPaddingTop: var(--sectionAnglePaddingTop);
  --sectionAngle: var(--angleNormal);
}

.Section--angleBottom {
  --sectionPaddingBottom: var(--sectionAnglePaddingBottom);
  --sectionMarginBottom: calc(var(--sectionAngleHeight) * -1);
}
```

Es importante recordar que cuando se agrega un ángulo inferior, la altura del ángulo debe restarse del margen inferior. Esto asegura que el contenido siguiente se desplace hacia arriba para compensar el espacio ocupado por el ángulo.

### Section masked

Este elemento solo tiene estos estilos:

```css
.Section__masked {
  overflow: var(--sectionOverflow); /* hidden at first */
}
```

### Section Background Mask

Este elemento es el encargado de contener los elementos que se presentaran en el background de la sección, posee el CSS:

```css
.Section__backgroundMask {
  position: absolute;
  width: 100%;
  height: 100%;
  overflow: var(--sectionBackgroundOverflow); /* visible at first */
}
```

Se asegura de ocupar todo el ancho y alto del sección

### Section Background

Este elemento va a establecer el color de fondo de la section y posee los siguientes estilos:

```css
.Section__background {
  position: relative;
  height: 100%;
  max-height: var(--sectionAngleMaxHeight);
  width: 100%;
  top: 0;
  left: 0;
  transform-origin: var(--sectionTransformOrigin);
  transform: skewY(var(--sectionAngle));
  background: var(--backgroundColor);
  overflow: hidden;
}
```

Como se puede ver, si se tiene un angulo, este estara refleado en `transform: skew(var(--sectionAngle))`, ademas se establece el background desde `background: var(--backgroundColor)`

### Section Container

Este es el elemento que contiene el contenido (text e imagenes), este es del mismo tamaño de la sección:

```css
.Section__container {
  position: relative;
  z-index: 1;
  display: flex;
  justify-content: center;
  min-height: var(--sectionMinHeight);
}
```

Esto hara que todo contenido este centrado sin usar la tecnica de `margin: 0 auto`

### Section Layout Container

Este elemento se encarga de establecer el ancho y margenes del contenido:

```css
.Section__layoutContainer {
  width: 100%;
  max-width: var(--layoutWidth);
  margin: 0 var(--columnPaddingNormal);
}
```

El valor de `layoutWidth` cambia a `1112px`

```css
@media (min-width: 1112px) {
  html {
    --layoutWidth: var(--layoutWidthMax);
    --gutterWidth: calc(var(--windowWidth) / 2 - var(--layoutWidth) / 2);
  }
}
```

### Section Layout

Ultimo element de la seccion, este se encarga de establecer el padding top y padding bottom (si es angle o no):

```css
.Section__layout {
  padding: var(--sectionPaddingTop) 0 var(--sectionPaddingBottom);
}
```

Como se ve, se usa `--sectionPaddingTop` y `--sectionPaddingBottom` que son dos variables de las que se ha hablado anteriomente y cambian dependiendo del los media queries (`375px < x < 1112px`)
