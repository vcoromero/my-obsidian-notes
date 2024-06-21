Sí, hay herramientas disponibles para Go que permiten recargar automáticamente tu aplicación cuando guardas cambios en tu código. Una de las más populares es `air`.

### Instalación de `air`

Primero, necesitas instalar `air`. Puedes hacerlo utilizando `go install`:

```bash
go install github.com/cosmtrek/air@v1.28.0
```

Asegúrate de que `$GOPATH/bin` esté en tu variable de entorno `PATH` para que puedas ejecutar `air` desde la línea de comandos.

### Configuración de `air`

Después de instalar `air`, puedes configurarlo para tu proyecto Go. Sigue estos pasos:

1. **Crear un archivo de configuración `.air.toml` en la raíz de tu proyecto**:

```toml
# Config file for Air
[build]
  bin = "./tmp/main" # Path to binary file built by `go build`
  cmd = "go build -o ./tmp/main" # Command to build your project
  include_ext = ["go", "tmpl", "html"] # Extensions to trigger rebuild
  exclude_dir = ["assets", "tmp", "vendor"] # Directories to exclude from watching
  exclude_file = [] # Files to exclude from watching
  exclude_regex = ["_test\\.go"] # Regex for files to exclude from watching
  follow_symlink = true # Follow symlink
  dir = "." # Root directory to watch

[run]
  cmd = "./tmp/main" # Command to run the binary file
  restart_on_error = true # Restart if the process exits with an error

[log]
  color = "auto" # Colorize log output ("auto", "always", "never")
  level = "info" # Log level ("debug", "info", "warn", "error")
  time = false # Print timestamp in log output
```

2. **Ejecutar `air`**:

En la raíz de tu proyecto, simplemente ejecuta:

```bash
air
```

`air` empezará a monitorear los cambios en los archivos especificados (por defecto archivos `.go`) y recargará automáticamente tu aplicación cada vez que guardes un cambio.

### Ejemplo de Estructura de Proyecto

Aquí tienes un ejemplo de cómo se vería tu estructura de proyecto con `air`:

```
gymstration-backend/
├── config/
│   └── config.go
├── database/
│   ├── db.go
│   └── init.sql
├── src/
│   ├── handlers/
│   │   └── roles.go
│   ├── models/
│   │   └── role.go
│   ├── repositories/
│   │   └── role_repository.go
│   ├── routes/
│   │   └── routes.go
│   └── services/
│       └── role_service.go
├── .air.toml
├── .env
├── .gitignore
├── docker-compose.yml
├── go.mod
├── go.sum
├── main.go
└── README.md
```

### Uso de `air`

Cada vez que hagas cambios en tu código y guardes los archivos, `air` automáticamente reconstruirá y reiniciará tu aplicación Go, permitiéndote ver los cambios de inmediato sin necesidad de reiniciar manualmente.

Esto debería facilitar mucho tu flujo de trabajo durante el desarrollo.