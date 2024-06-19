Definición de Roles y Permisos:

- **Root**: Permisos completos, incluyendo la gestión de roles y usuarios.
- **Administrador**: Puede realizar todas las acciones administrativas necesarias, pero con algunas restricciones en comparación con el root.
- **Empleado**: Permisos específicos para tareas asignadas a empleados.
- **Entrenador**: Solo puede su propia anotar asistencia.
- **Socio**: Solo puede anotar su propia asistencia.
- **Visitante**: Administradores y empleados solo pueden anotar su asistencia.

Los roles tendrán los siguientes datos:
- id
- nombre
- created_at
- updated_at
- deleted_at

La tabla de funciones tendrá los siguientes datos:
- Id
- name


Ambas se van a relacionar en una tabla de muchos a muchos.