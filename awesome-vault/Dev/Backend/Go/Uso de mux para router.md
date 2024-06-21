En Go, puedes lograr esto dividiendo las responsabilidades en diferentes archivos y paquetes. Aquí te muestro cómo puedes organizar tu proyecto para tener las rutas en un archivo separado.

### Estructura del Proyecto

Aquí tienes una estructura de proyecto actualizada que separa las rutas del resto del código:

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

### Paso 1: Crear el Archivo de Rutas

Importa el paquete mux:

```bash
go get "github.com/gorilla/mux"
```

Crea un nuevo archivo para definir tus rutas, por ejemplo, `routes.go`.

**src/routes/routes.go**:
```go
package routes

import (
	"net/http"

	"github.com/gorilla/mux"
	"github.com/vcoromero/gymstration-backend/src/handlers"
)

// RegisterRoutes registra todas las rutas de la aplicación
func RegisterRoutes(r *mux.Router) {
	apiRouterV1 := r.PathPrefix("/api/v1").Subrouter()
	apiRouterV1.HandleFunc("/roles", handlers.GetRoles).Methods("GET")
	// Aquí puedes añadir más rutas
}
```

### Paso 2: Modificar el Archivo `main.go`

Actualiza tu archivo `main.go` para utilizar el enrutador definido en `routes.go`.

**main.go**:
```go
package main

import (
	"log"
	"net/http"

	"github.com/gorilla/mux"
	"github.com/vcoromero/gymstration-backend/config"
	"github.com/vcoromero/gymstration-backend/database"
	"github.com/vcoromero/gymstration-backend/src/routes"
)

func main() {
	config.Init()
	database.Connect()

	r := mux.NewRouter()
	routes.RegisterRoutes(r) // Registrar todas las rutas

	port := ":" + config.ServerPort
	log.Printf("Starting server on %s\n", port)
	log.Fatal(http.ListenAndServe(address, r))
}
```

### Paso 3: Verificar la Integración

Asegúrate de que todo esté bien conectado y prueba tu servidor para verificar que las rutas funcionan correctamente.

Con esta organización, tu código es más fácil de mantener y escalar, similar a cómo lo harías en proyectos con TypeScript y otros lenguajes. Si tienes más preguntas o necesitas más detalles, no dudes en preguntar.