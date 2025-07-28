HU:https://jira.falabella.tech/browse/OME-3292
HU referencia: https://jira.falabella.tech/browse/OME-3082

Subtasks:
[CHORE] Crear la aplicacion en nullplatform
	Es requerido crear la aplicación desde el portal de Nulltform teniendo en cuenta los siguientes puntos: 

- Respetar la nomenclatura para el nombre de la aplicación [https://confluence.falabella.tech/pages/viewpage.action?pageId=516338963](https://confluence.falabella.tech/pages/viewpage.action?pageId=516338963)

- Importar el repositorio vigente:  
    [https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-rewards-card-manager](https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-rewards-card-manager)

[CHORE] Crear el scope para el ambiente TEST QA PROD
- Registrar el ambiente(scope) en Null
- Asignar las variables de entorno en el apartado de parámetros acorde al ambiente

[BACK] Modificar el archivo gitlab-ci.yml para el soporte de nullplatform

[BACK] Migrar funciones de la client-manager-ingress a la client-manager-manager
- Migrar los middlewares del ingress.
- Agregar variables de entorno para las URLs de los servicios que se llaman internamente.
- Agregar variable de entorno para datadog.

[BACK] Actualizar las vulnerabilidades de dependencias

[CHORE] Modificar Kong TEST QA PROD para balanceo y soporte nullplatform en el servicio client-manager
- Eliminar la configuración del ingress
- Agregar el balanceo de trafico entre las dos aplicaciones
- Validar el correcto balanceo

Tomar como referencia la siguiente documentación:  
[https://confluence.falabella.tech/pages/viewpage.action?pageId=516808658](https://confluence.falabella.tech/pages/viewpage.action?pageId=516808658)

[BACK] Modificar stack TEST QA PROD para agregar soporte a nullplatform y cambios de la ingress
- eliminar configuraciones del ingress
- Crear el nuevo VAULT_FILE y modificar el stack-{enviroment}.env para agregarlo (si aplica).
- Modificar el docker-stack en la sección del servicio para usar el nuevo VAULT_FILE (si aplica).
- agregar variables de entorno faltantes
