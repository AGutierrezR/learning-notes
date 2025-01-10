# Worktrees

- Crear un nuevo directorio con una rama ya existente:

```bash
git worktree add path/to/directory branch
```

- Crear un nuevo directorio con una nueva rama:

```bash
git worktree add path/to/directory -b new_branch
```

- Listar todos los directorios de trabajo adjuntos a este repositorio:

```bash
git worktree list
```

- Eliminar un directorio de trabajo (después de eliminar el directorio de trabajo):

```bash
git worktree prune
```
