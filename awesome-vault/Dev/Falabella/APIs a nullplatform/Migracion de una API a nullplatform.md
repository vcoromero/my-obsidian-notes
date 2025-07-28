Para realizar la migración de un servicio, se tiene que realizar las siguientes acciones:

### Servicio:
- [[Migrar la ingress a manager (si aplica).]]
- [[Modificar el gitlab-ci.yml en el servicio para dar soporte al onepipe de nullplatform]]
- [[Modificar las URLs de otros servicios a los que el servicio llama en sus configuraciones de ambiente (local, dev, qa, prod), esto mediante variables de entorno que se agregaran en el stack.]]

### Nullplatform:
- Crear aplicación.
- Crear el scope para test, qa y prod.
- Crear variables de entorno y asignarlas a los scopes.
- Crear un release y hacer deploy de la aplicación.

### Kong:
- Eliminar lo relacionado al ingress(si aplica) de los routes y services.
- Agregar los archivos targets y upstreams.
- Modificar los archivos routes y services.
- Modificar (o agregar) el archivo plugins para habilitar el balanceo.

### Stack
- Modificar el healtcheck del servicio (si aplica).
- Eliminar la ingress (si aplica).
- Modificar los middlewares del servicio.
- Agregar variables de entorno para las URLs de los servicios que se llaman internamente.
- Agregar variable de entorno para datadog.
- Crear el nuevo VAULT_FILE y modificar el stack-{enviroment}.env para agregarlo (si aplica).
- Modificar el docker-stack en la sección del servicio para usar el nuevo VAULT_FILE (si aplica).




Rewards-card-manager MRs:
- Migración de la ingress (incompleto, faltaban cosas que se hicieron en el MR de abajo): https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-rewards-card-manager/-/merge_requests/38/diffs#7030d0b2f71b999ff89a343de08c414af32fc93a
- Soporte para nullplatform: https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-rewards-card-manager/-/merge_requests/39#bde78f313e5e4d0170c8da4a22e81290f67a0dd7

Kong MRs:
- Test: https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/cmr-mx-onboarding-test-kong-config-terraform/-/merge_requests/77#587d266bb27a4dc3022bbed44dfa19849df3044c
- QA: https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/cmr-mx-onboarding-qa-kong-config-terraform/-/merge_requests/43

Stack deploy MRs:
- Modificar el healtcheck: https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-stack-deploy/-/merge_requests/330
- Cambios para Test (fueron varios porque se omitían cosas):
	- https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-stack-deploy/-/merge_requests/333
	- https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-stack-deploy/-/merge_requests/334
	- https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-stack-deploy/-/merge_requests/335
	- https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-stack-deploy/-/merge_requests/336
- Cambios para QA: https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-stack-deploy/-/merge_requests/337
- Eliminar rewards-card-ingress
	- Test: https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-stack-deploy/-/merge_requests/274
	- QA: https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-stack-deploy/-/merge_requests/277
	- Prod: https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-stack-deploy/-/merge_requests/278