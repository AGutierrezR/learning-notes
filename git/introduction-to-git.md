# Introduccion a Git

## Que es Git?

Git es un sistema de control de versiones distribuido (VCS, por sus siglas en inglés). A diferencia del sistema tradicional centralizado, Git permite que todo el trabajo se realice localmente y puede divergir tanto como desees.

## Git

Git tiene dos tipos de comandos:

- Comandos de alto nivel ("porcelain"): son los que usas normalmente y hacen que Git sea fácil de manejar, como guardar cambios o revisar el historial.
- Comandos de bajo nivel ("plumbing"): son más técnicos y trabajan con las partes internas de Git, como mover datos en el sistema.

Por lo general, usaremos los comandos simples, pero de vez en cuando veremos los técnicos para entender mejor cómo funciona Git por dentro.

## Terminos clave

- **Repo**: un proyecto gestionado con Git.
- **Commit**: un punto en el tiempo que representa el estado completo del proyecto.
- **SHA de un commit**: una cadena de 40 caracteres (a-f, 0-9) generada a partir del contenido del cambio, autor, hora y más datos del commit.
- **Índice (index)**: También llamado "área de preparación" (staging area).

> [!NOTE]
> Según el blog de GitHub:
>
> El índice de Git es una estructura de datos clave. Funciona como una "zona intermedia" entre los archivos de tu sistema y el historial de commits. Cuando ejecutas git add, los archivos de tu directorio de trabajo se convierten en objetos y se almacenan en el índice, listos para ser confirmados como cambios "preparados".

- **Squash**: Unificar varios commits en un solo commit.
  - Técnicamente, un squash convierte N commits en N-1 o 1 commit, aunque generalmente significa reducirlos a uno solo.
- **Work tree, working tree, main working tree**: Es tu repositorio Git, es decir, el conjunto de archivos que representan tu proyecto. Tu "working tree" se configura con git init o git clone.

- Archivos no rastreados, preparados y rastreados:

  1. **No rastreados (untracked)**: Archivos que no están preparados (indexados) ni confirmados por primera vez. Son los más fáciles de perder, ya que Git no guarda información sobre ellos.
  2. **Preparados (staged/indexed)**: Cambios listos para ser confirmados. Se preparan con el comando git add. Consulta man git-add para más detalles.
  3. **Rastreados (tracked)**: Archivos que ya están gestionados por Git. Un archivo rastreado puede tener cambios preparados en el índice, listos para ser confirmados.

- **Remote**: Una copia del mismo repositorio Git en otra computadora o directorio. Puedes recibir cambios de este repositorio o enviarle tus cambios. Piensa en GitHub como un ejemplo de repositorio remoto.

## Hechos clave sobre Git

- Git es un grafo acíclico, lo que significa que **no puede haber ciclos** en su estructura.
- En Git, cada commit es un **nodo** en el grafo, y cada puntero representa una relación de **hijo a padre** entre los commits.
- Si eliminas archivos no rastreados, **se perderán para siempre**. Por eso se recomienda: **"confirma pronto y con frecuencia"**, ya que siempre puedes reorganizar el historial más adelante (por ejemplo, unificando commits con squash).
- Usa `man git-<op>` para acceder al manual detallado de cualquier comando (por ejemplo, `man git-add`).

## A tomar en cuenta

La experiencia de muchas personas con Git se resume en cinco comandos:

- `push`
- `pull`
- `add`
- `commit`
- `status`

Pero es bueno entender como funcionan los siguientes comandos:

- `log`
- `config`
- `reset`
- `rebase`
- `reflog`
- `rerere`
- `cat-file`
