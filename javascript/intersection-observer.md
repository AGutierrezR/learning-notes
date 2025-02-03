# Intersection Observer API

Los **Intersection Observers** son una API de JavaScript que permite observar y reaccionar cuando un elemento entra o sale del viewport (o de un contenedor específico). Son ideales para aplicaciones donde se necesita detectar la visibilidad de elementos, para iniciar animaciones, imágenes diferidas o carga infinita.

## Funcionamiento básico

Un `IntersectionObserver`:

1. Monitorea uno o más elementos objetivo (`target elements`).
2. Ejecuta un callback cuando las condiciones de intersección cambian (es decir, cuando un elemento entra o sale del viewport o del contenedor definido).
3. Se puede configurar para definir márgenes o porcentajes de visibilidad.

### Ejemplo básico

```javascript
const target = document.querySelector(".target");

// Crear el observer
const observer = new IntersectionObserver((entries) => {
  entries.forEach((entry) => {
    if (entry.isIntersecting) {
      console.log("El elemento es visible.");
    } else {
      console.log("El elemento no es visible.");
    }
  });
});

// Observar el elemento objetivo
observer.observe(target);
```

## Argumentos y opciones

### Callback

El `callback` recibe **una lista de `IntersectionObserverEntry`**. Cada entrada contiene información sobre la intersección de un elemento objetivo con el viewport o contenedor.

### Opciones de observe

El método `observe` recibe **dos argumentos**:

1. El nodo a observar, este debe ser un elemento del DOM.
2. Un objeto de configuración con las opciones de observación.

> [!Info]
> Las opciones de observación son un objeto con las siguientes propiedades:
>
> - `root`: Elemento que actúa como contenedor de referencia. Por defecto es el viewport.
> - `rootMargin`: Márgenes alrededor del contenedor de referencia. Puede ser un string o un array de strings. 
> - `threshold`: Umbral de visibilidad para disparar el callback. Puede ser un número o un array de números.

## Referencias

- [MDN Web Docs: Intersection Observer API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API)

