Para conectarte a MySQL desde Go utilizando Docker, necesitas realizar varios pasos, incluyendo la configuración del contenedor de MySQL y la instalación del controlador MySQL para Go. A continuación, te proporciono una guía paso a paso:

### 1. Configura y ejecuta MySQL en Docker

1. Crear un archivo `.env` con los datos de conexión:
   
```env
DB_HOST=localhost
DB_PORT=3306
DB_USER=gymstrator
DB_PASSWORD=gymstrator_pswrd
DB_NAME=gymstration
MYSQL_ROOT_PASSWORD=root_pswrd
SERVER_PORT = 8080
```

2. Crear un archivo `config.go` para gestionar las variables de entorno:
   
```go
package config

import (
	"log"
	"os"
	
	"github.com/joho/godotenv"
)

var DbUser string
var DbPassword string
var DbHost string
var DbPort string
var DbName string

  

func Init() {
	err := godotenv.Load()
	if err != nil {
	log.Fatal("Error loading .env file")
	}

	DbUser = os.Getenv("DB_USER")
	DbPassword = os.Getenv("DB_PASSWORD")
	DbHost = os.Getenv("DB_HOST")
	DbPort = os.Getenv("DB_PORT")
	DbName = os.Getenv("DB_NAME")
  
	log.Println("Config initialized")
}
```

3. **Crear un contenedor MySQL**:
   
   Crea un archivo `docker-compose.yml` para configurar el contenedor de MySQL:

```yaml
version: "3.9"
services:
  db:
	image: mysql:8.0
	container_name: gymstration-db
	environment:
	  MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
	  MYSQL_DATABASE: ${DB_NAME}
	  MYSQL_USER: ${DB_USER}
	  MYSQL_PASSWORD: ${DB_PASSWORD}
	ports:
	  - "3306:3306"
	volumes:
	  - gymstration-data:/var/lib/mysql
	  - ./database/init.sql:/docker-entrypoint-initdb.d/init.sql
	networks:
	  - gymstration-db-network

volumes:
  gymstration-data:

networks:
  gymstration-db-network:
   ```

   Luego, ejecuta el contenedor:

   ```bash
   docker-compose up -d
   ```

2. **Verifica que MySQL esté corriendo**:

   Puedes verificar si el contenedor está corriendo usando:

   ```bash
   docker ps
   ```
   3. Accesar a la instancia de mysql:
   ```bash
   docker exec -it db mysql -ubasic_user -pbasic_password
```

### 2. Instala el controlador MySQL para Go

En tu proyecto Go, necesitas instalar el controlador MySQL. Utiliza `go get` para instalar el paquete:

```bash
go get -u github.com/go-sql-driver/mysql
```

### 3. Conéctate a MySQL desde Go

A continuación, un ejemplo de código para conectarse a MySQL desde Go:

 ```go
package database

import (
	"database/sql"
	"fmt"
	"log"
	_ "github.com/go-sql-driver/mysql"
	cfg "github.com/vcoromero/gymstration-backend/config"
)


var DB *sql.DB

func Connect() {
	databaseConnectionString := fmt.Sprintf("%s:%s@tcp(%s:%s)/%s", cfg.DbUser, cfg.DbPassword, cfg.DbHost, cfg.DbPort, cfg.DbName)
	
	databaseConnectionUri := databaseConnectionString
	
	db, err := sql.Open("mysql", databaseConnectionUri)

	if err != nil {
		log.Fatal(err)
	}

	err = db.Ping()
	if err != nil {
		log.Fatal(err)
	}

	DB = db
	log.Println("Connected to the database!")
}
```

```go
package main

import (
	"github.com/vcoromero/gymstration-backend/config"
	"github.com/vcoromero/gymstration-backend/database"
)

func main() {
	config.Init()
	database.Connect()
	}
}
```

