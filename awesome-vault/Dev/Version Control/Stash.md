Guardar cambios con un nombre descriptivo:
```bash
git stash push -m "work-in-progress-fix-bug"
```

Ver listado de stashes
```bash
git stash list
```

Aplicar un stash en específico:
```bash
git stash apply stash@{0}
```

Eliminar un stash en específico después de aplicarlo:
```bash
git stash pop stash@{0}
```

Eliminar todos los stashes:
```bash
git stash clear
```