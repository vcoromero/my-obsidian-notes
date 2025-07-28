# Cursor AI - Instalación en ~/Apps y menú de apps

- [ ] Descargar Cursor AI AppImage desde https://www.cursor.sh/
- [ ] Crear carpeta para la app: `mkdir -p ~/Apps/cursor`
- [ ] Mover AppImage: `mv ~/Descargas/Cursor-*.AppImage ~/Apps/cursor/cursor`
- [ ] Darle permisos de ejecución: `chmod +x ~/Apps/cursor/cursor`
- [ ] Crear symlink para usarlo en terminal: `sudo ln -sf ~/Apps/cursor/cursor /usr/local/bin/cursor`
- [ ] Crear `.desktop` file con: `nano ~/.local/share/applications/cursor.desktop`
- [ ] Agregar contenido:
  ```ini
  [Desktop Entry]
  Version=1.0
  Name=Cursor AI
  Comment=AI Pair Programming IDE
  Exec=/home/vromero/Apps/cursor/cursor
  Icon=/home/vromero/.local/share/icons/cursor.png
  Terminal=false
  Type=Application
  Categories=Development;IDE;
