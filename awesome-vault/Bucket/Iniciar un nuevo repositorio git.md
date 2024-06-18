Para iniciar un nuevo proyecto/repositorio de git, basta con realizar los siguientes pasos:

- Dirigirnos al proyecto
- Crear la rama main
- Agregar todos los archivos 
- Agregar un comentario a ese commit.
```bash
cd /path/to/my/project

git init 

git add .

git commit -m "Feat: initial commit"
```

- Enlazar el repositorio local con el repositorio remoto
```bash
git remote add origin <URL>
```
- Verificar que el remoto se añadió correctamente
```bash
git remote -v
```
- Subir los archivos al repositorio remoto:
```bash
git push -u origin main
```
