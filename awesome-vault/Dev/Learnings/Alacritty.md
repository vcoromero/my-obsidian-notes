Me cambié a esta terminal porque me permitía instalar un plugin para poder dividir paneles dentro de la misma terminal, para esto también integré tmux.

### Usando tmux para dividir la pantalla

- **Dividir la pantalla horizontalmente**: Presiona `Ctrl + b`, suelta y luego presiona `%`.
    
- **Dividir la pantalla verticalmente**: Presiona `Ctrl + b`, suelta y luego presiona `"` (comillas dobles).
    
- **Navegar entre paneles**:
    
    - Ir al siguiente panel: `Ctrl + b` seguido de la flecha derecha o izquierda.
    - Ir al panel anterior: `Ctrl + b` seguido de la flecha arriba o abajo.
- **Crear una nueva ventana (tab)**: Presiona `Ctrl + b`, suelta y luego presiona `c`.
    
- **Navegar entre ventanas**:
    
    - Ir a la siguiente ventana: `Ctrl + b` seguido de `n`.
    - Ir a la ventana anterior: `Ctrl + b` seguido de `p`.
- **Cerrar el panel actual**: Presiona `Ctrl + b`, suelta y luego presiona `x`. Confirma el cierre del panel.
    
- **Cerrar la ventana actual (tab)**: Cierra todas las sesiones activas en la ventana (puedes usar `exit` en cada una) o presiona `Ctrl + b`, suelta y luego presiona `&` para cerrar la ventana actual.
### Copiar y Pegar en tmux

Para copiar y pegar en `tmux`, puedes usar el modo de copia de `tmux`, que funciona de manera diferente. Aquí están los pasos:

1. **Entrar en modo de copia**: Presiona `Ctrl + b` seguido de `[` para entrar en modo de copia.
    
2. **Mover el cursor**: Usa las teclas de flecha para mover el cursor al inicio del texto que quieres copiar.
    
3. **Iniciar la selección**: Presiona `Ctrl + Space` para iniciar la selección del texto.
    
4. **Mover el cursor para seleccionar**: Usa las teclas de flecha para mover el cursor y seleccionar el texto deseado.
    
5. **Copiar el texto**: Presiona `Enter` para copiar el texto seleccionado al búfer de `tmux`.
    
6. **Pegar el texto**: Presiona `Ctrl + b` seguido de `]` para pegar el texto copiado.