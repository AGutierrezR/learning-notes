# Mutation Observer API

Los Mutation Observers son una API de JavaScript que permite observar cambios en el DOM, como modificaciones en nodos (agregar a remover), atributos o contenido. Son útiles para detectar y responder automáticamente a alteraciones en el DOM, sin necesidad de usar bucles de comparación o eventos ineficientes.

## Funcionamiento básico

Un MutationObserver observa un elemento del DOM y ejecuta un callback cuando detecta cambios. Los pasos básicos son:

1. Crear una instancia de MutationObserver y pasarle un callback.

```javascript
const observer = new MutationObserver(callback);
```

2. Llamar a observe sobre un nodo objetivo, especificando los tipos de mutaciones a observar.

```javascript
observer.observe(targetNode, config);
```

3. Detener la observación cuando ya no sea necesaria con disconnect.

```javascript
observer.disconnect();
```

## Argumentos y opciones

### Callback

El `callback` recibe **dos argumentos**:

1. Una lista de `MutationRecords`
2. El propio `MutationObserver`.

> [!Info]
> Los `MutationRecords` contienen información sobre los cambios detectados, como el tipo de mutación, el nodo afectado y los valores antiguos y nuevos.

### Opciones de observe

El método `observe` recibe **dos argumentos**:

1. El nodo a observar, este debe ser un elemento del DOM.
2. Un objeto de configuración con las opciones de observación.

> [!Info]
> Las opciones de observación son un objeto con las siguientes propiedades:
>
> - `childList`: Observa cambios en los hijos del nodo.
> - `attributes`: Observa cambios en los atributos del nodo.
> - `characterData`: Observa cambios en el contenido de texto del nodo.

## Referencias

- [MDN Web Docs: Mutation Observer API](https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver)
