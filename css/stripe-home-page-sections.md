# Stripe Homepage Sections

## HTML Estructura Base

Esta es una estructura base de una seccion de la pagina de Stripe, esta estructura es usada en varias secciones de la pagina.

```html
<section class="Section">
  <div class="Section__masked">
    <div class="Section__backgroundMask">
      <div class="Section__background">
        <!-- Background Material -->
      </div>
    </div>
    <div class="Section__container">
      <div class="Section__layoutContainer">
        <div class="Section__layout">
          <!-- Content -->
        </div>
      </div>
    </div>
  </div>
</section>
```

`.Section` puede tener otras clases complementarias como

- `.Section--hasGuides`
- `.Section--angleTop`: Agrega CSS properties para agregar un angulo en la parte superior de la seccion
- `.Section--angleBottom`: Agrega CSS properties para agregar un angulo en la parte inferior de la seccion
- `.Section--paddingNormal`: Agrega padding normal a la seccion (este padding viene)
- etc.

> [!Info]
> Luego agregare mas info sobre estas clases

## CSS

Antes de empezar a desglosar el CSS de la seccion, hay que tomar en cuenta que se usaran variables CSS que vienen del html, estas variables son:

```css
html {
  --gutterWidth: 16px;

  --angleNormal: -6deg;
  --angleNormalSin: 0.106;
  --columnPaddingNormal: 16px;
  --windowWidth: calc(100vw - var(--scrollbarWidth));
}
```

Ese `--angleNormalSin` es la tangente del angulo `6deg`

---

Primero revisemos las declaraciones de la clase `.Section`

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

Aqui se crean todas la variables que se usaran en la seccion, estas variables son usadas para calcular el padding, margin, angulos (para los angulos de arriba y de abajo de las secciones), etc. Estas variables afectaran la parte de `.Section__layout` y `.Section__background`.

Aparte de esto, se establecen las reglas de CSS para la seccion, como el color del texto, el z-index, el margin-top y margin-bottom, etc.

Adicional a estas declaraciones, existe otra:

```css
.Section {
  --sectionPaddingNormalMax: 128;
}
```

Esta solo agrega esta variable CSS. Agrega un maximo para el padding, variable es usada tanto para el padding de arriba como para el de abajo.

Ahora vamos con variables calculadas para el padding de la seccion, estas variables son calculadas en base a las variables que se crearon anteriormente. Su uso es para calcular el padding de la seccion sin angulo y con angulo.

```css
.Section {
  --sectionAnglePaddingTopBase: calc(
    var(--sectionAnglePaddingBaseMin) * 1px +
      (
        var(--sectionAnglePaddingTopBaseMax) - var(--sectionAnglePaddingBaseMin)
      ) *
      (var(--windowWidth) / 737 - 0.50882px)
  );
  --sectionAnglePaddingBottomBase: calc(
    var(--sectionAnglePaddingBaseMin) * 1px +
      (
        var(--sectionAnglePaddingBottomBaseMax) -
          var(--sectionAnglePaddingBaseMin)
      ) *
      (var(--windowWidth) / 737 - 0.50882px)
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

- `--sectionAnglePaddingTopBase` calcula un valor medio entre el min y el max para el padding de arriba. (desde 375 hasta 1112) el valor tiene que estrar entre min y max.
- `--sectionAnglePaddingBottomBase` calcula un valor medio entre el min y el max para el padding de abajo. (desde 375 hasta 1112) el valor tiene que estrar entre min y max.
- `--sectionAnglePaddingTop` calcula el padding de arriba con el angulo. Para esto suma el alto del angulo, mas el padding base
- `--sectionAnglePaddingBottom` calcula el padding de abajo con el angulo. Para esto suma el alto del angulo, mas el padding base
- `--sectionPaddingTop` calcula el padding de arriba sin angulo
- `--sectionPaddingBottom` calcula el padding de abajo sin angulo

Algo a tomar en cuenta es que cuando la pantalla esta por debajo de 375px, estas son las variables CSS computadas:

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

y para mas de 1112px:

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

Cuando se usan clases como .Section--angleTop o .Section--angleBottom, estas clases agregan padding con angulo a la seccion.

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

Tomar en cuenta que cuando se agregar un angulo inferior, se debe restar la altura del angulo al margen inferior. Esto hace que el contenido siguiente, se desplace hacia arriba para compensar el espacio ocupado por el ángulo.
