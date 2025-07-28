Para renombrar el último commit es súper simple. No necesitas rebase, solo este comando:

```bash
git commit --amend -m "Nuevo mensaje del commit"
```

---

### 🔍 ¿Qué hace eso?

- Reescribe **solo el último commit** (mensaje y contenido si agregaste cambios).
    
- No cambia el snapshot si no agregaste nada, solo el mensaje.
    

---

### ⚠️ Importante:

Si **ya hiciste push**, y quieres cambiar el mensaje **en el repo remoto**, tienes que hacer un push forzado:

```bash
git push --force-with-lease
```
