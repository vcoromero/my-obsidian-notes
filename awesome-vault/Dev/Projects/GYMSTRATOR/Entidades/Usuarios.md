Existirán 4 tipos de usuario:

- SuperUser
	- Creador del universo gymstrator.
	- Existirá desde el inicio de la app.
	- Sus datos pueden modificarse.
	- Tiene un costo en especifico de su membresía (incluso podría no tenerla).
- Administrador
	- Se registra al ingresar al gimnasio.
	- Se da de alta una única vez.
	- Sólo SuperUser puede realizar esta acción.
	- Sus datos pueden modificarse.
	- Tiene un costo en especifico de su membresía.
- Empleado
	- Se registra al ingresar al gimnasio.
	- Se da de alta una única vez.
	- SuperUser, Administrador y Empleado pueden realizar esta acción.
	- Sus datos pueden modificarse.
	- Tiene un costo en especifico de su membresía.
- Entrenador
	- Se registra al ingresar al gimnasio.
	- Se da de alta una única vez.
	- SuperUser, Administrador y Empleado pueden realizar esta acción.
	- Sus datos pueden modificarse.
	- Tiene un costo en especifico de su membresía.
- Socio
	- Usuario quien dispone de los equipos para entrenar. 
	- Se registra al ingresar al gimnasio.
	- Se da de alta una única vez.
	- SuperUser, Administrador y Empleado pueden realizar esta acción.
	- Sus datos pueden modificarse.
	- Tiene un costo en especifico de su membresía.
- Visitante

Los datos base de cada usuario será los siguientes:
- Nombre*
- Segundo nombre
- Primer apellido*
- Segundo apellido*
- Fecha de nacimiento*
- Rol
- Created_at
- Updated_at
- Deleted_at

Además para tener un control de la selfies se creará una tabla que tendrá los siguientes campos:
- id
- user_id
- image_path
- created_at
- updated_at
- deleted_at
