# Stripe Color Management

## Themes

Stripe posee varias clases que declaran custom properties de CSS, entre estas estan:

- `.theme--White`
- `.theme--light`
- `.theme--Dark`
- `.theme--SemiDark`
- `.theme--Transparent`
- `.theme--HubDark`
- etc.

Estos solo declaran colores, como por ejemplo:

```css
.theme--White {
  --backgroundColor: #fff;
  --linkColor: var(--accentColor);
  --linkHoverColor: #0a2540;
  --buttonColor: var(--accentColor);
  --buttonHoverColor: #0a2540;
  --buttonDisabledColor: #cfd7df;
  --buttonDisabledOpacity: 0.7;
  --knockoutColor: #fff;
  --knockoutDisabledColor: #8898aa;
  --guideSolidColor: rgba(66, 71, 112, 0.06);
  --guideDashedColor: rgba(66, 71, 112, 0.09);
  --titleColor: #0a2540;
  --textColor: #425466;
  --formFieldDescriptionTextColor: #3f4b66;
  --inputBackground: #f6f9fc;
  --checkboxInputBackground: #e7ecf1;
  --inputPlaceholderColor: #727f96;
  --inputTextColor: #0a2540;
  --inputErrorAccentColor: #ff5996;
  --annotationColor: #8c9eb1;
  --maskFadeColor: rgba(0, 0, 0, 0.4);
  --navColor: #0a2540;
  --navHoverColor: #0a2540;
  --navHoverOpacity: 0.6;
  --footerColor: #0a2540;
  --cardBorderColor: #cbd6e0;
  --cardBackground: #fff;
  --subcardBackground: #f6f9fc;
  --gridSubcardBackground: #f6f9fc;
  --tableIconColor: #8c9eb1;
  --stripeAccentWhite: #fff;
  --stripeAccentLight: #e3e7ec;
  --stripeAccentDark: #0a2540;
  --bulletColor: #cfd7df;
  --footnoteTextColor: #4d5b78;
  --disclaimerTextColor: #707f98;
  --inlineCodeTextColor: #2c3a57;
  --inlineCodeBackground: #e6ecf2;
  --socialLogoColor: #c4ccd8;
  --socialLogoHoverColor: #0a2540;
}
```

Esta clase hace uso de la variable `--accentColor` para los links y los botones, por eso se debe unir con otra clase con el prefino `.accent--xxx`

Por ejemplo:

- `.accent--Slate`
- `.accent--Cyan`
- `.accent--Blurple`

En pocas palabras, se usa para agregar color los elementos de apoyo en el diseño (botones, links, etc.)

```css
.theme--White.accent--Slate {
  --accentColor: #0a2540;
  --linkHoverOpacity: 0.6;
  --buttonHoverOpacity: 0.6;
}
```

> [!INFO]
> En algunas ocaciones no se establecen `--linkHoverOpacity` o `--buttonHoverOpacity`
> Esta clase se debe establecer junto con la de `.theme--` para dar apoyo y consistencia

## Usage

Para la parte de del background, Stripe siempre usa un elemento aparte con la clase `.Section__background` para colocar el color de fondo y todos los adornos (esto esta dentro de `.Section__backgroundMask`)

Para la parte de un background con un top o bottom diagonal lo hace en este `.Section__background` usando `transform: skew()`


