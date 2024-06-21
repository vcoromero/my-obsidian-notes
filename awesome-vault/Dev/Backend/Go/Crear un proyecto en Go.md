Sigue estos pasos:

1. **Instalar Go:**
   - Asegúrate de tener Go instalado en tu sistema. Puedes descargarlo desde [la página oficial de Go](https://golang.org/dl/).

2. **Configurar el entorno:**
   - Define tu GOPATH. Este es el directorio donde se almacenarán tus proyectos y dependencias. Puedes hacerlo configurando la variable de entorno `GOPATH`. Por ejemplo, en Linux o macOS, puedes agregar esto a tu archivo `.bashrc` o `.zshrc`:
     ```sh
     export GOPATH=$HOME/go
     export PATH=$PATH:$GOPATH/bin
     ```

3. **Crear el directorio del proyecto:**
   - Crea un nuevo directorio para tu proyecto. Por ejemplo:
     ```sh
     mkdir -p $GOPATH/src/github.com/tuusuario/tu-proyecto
     cd $GOPATH/src/github.com/tuusuario/tu-proyecto
     ```

4. **Inicializar el módulo Go:**
   - Inicia un nuevo módulo Go. Esto creará un archivo `go.mod` que define tu proyecto y sus dependencias.
     ```sh
     go mod init github.com/tuusuario/tu-proyecto
     ```

5. **Escribir el código:**
   - Crea un archivo `main.go` y escribe un programa simple. Por ejemplo:
     ```go
     package main

     import "fmt"

     func main() {
         fmt.Println("Hola, mundo!")
     }
     ```

6. **Compilar y ejecutar:**
   - Compila y ejecuta tu programa usando los comandos `go build` y `go run`.
     ```sh
     go run main.go
     ```

7. **Gestionar dependencias:**
   - Usa `go get` para añadir nuevas dependencias a tu proyecto. Por ejemplo:
     ```sh
     go get github.com/gin-gonic/gin
     ```

### Estructura del Proyecto

Una estructura de proyecto común en Go puede verse así:

```
/tu-proyecto
  ├── go.mod
  ├── go.sum
  ├── main.go
  ├── /cmd
  │   └── tu-proyecto
  │       └── main.go
  ├── /internal
  │   └── package1
  │       └── package1.go
  ├── /pkg
  │   └── package2
  │       └── package2.go
  ├── /api
  │   ├── handler.go
  │   └── router.go
  ├── /config
  │   └── config.go
  ├── /docs
  │   └── README.md
  ├── /scripts
  │   └── script.sh
  ├── /build
  │   ├── docker
  │   └── ci
  └── /vendor
```

### Ejemplo de Proyecto

Para un proyecto más complejo, por ejemplo, usando Gin para crear una API web, podrías tener algo así en `main.go`:

```go
package main

import (
    "github.com/gin-gonic/gin"
)

func main() {
    r := gin.Default()
    r.GET("/ping", func(c *gin.Context) {
        c.JSON(200, gin.H{
            "message": "pong",
        })
    })
    r.Run() // por defecto, ejecuta en :8080
}
```
