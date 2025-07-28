HU https://jira.falabella.tech/browse/OME-3258

* Puede tener condicion economica 1 y 11
* El codigo de producto es 8
* La fecha de pago es el dia 1 de cada mes
* El monto con el que se otorga es $1
* Podriamos quitar la validacion de pagos fijos y cerrada en la evaluate-manager y tambien en el product

Proyectos que se involucran en este cambios:
- client-manager 
	- no hay stubs para fixed-payment y closed
	- agregar stubs en el store
- product-manager
	- modificar const configs en generic-utils-helper para agregar los atributos de la tarjeta garantizado (codigoProducto, paymentDay)
	- agregar funcion buildCardBody para garantizada en generic-body-builder-helper
	- modificar el const buildBody para evaluar el cardType de garantizada
	- agregar stubs para garantizado en:
		- store: action-trace-* , cat-* , credit-card-*
		- product-cat
- evaluate-manager
	- agregar producto garantizado en const getCardType de credit-evaluate-handler.js 
		- eliminar de esta funcion la evaluacion de fixed-payment y closed?? (seria otra subtask)
	- agregar stubs para garantizado en:
		- financial-risks/ assesment-approved-product-*
		- cae/response-cae2-aprobado-*
- document-manager
	- agregar en build-seventh-document.js el buildBodySeventh para producto garantizado
	- crear stub del store para producto garantizado
	- por que producto closed solo aparece en documento 2, se eliminara???
- api-stubs
	- agregar stubs para garantizado en:
	- financial-risks
	- cliente-admision-evaluar



Falta modificar:
- fraud-manager
- prevent-fraud-manager

MR de servicios modificados:
- https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-application-manager/-/merge_requests/239
- https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-client-manager/-/merge_requests/50
- https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-document-manager/-/merge_requests/106
- https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-fraud-manager/-/merge_requests/58
- https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-product-manager/-/merge_requests/69
- https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-prevent-fraud-manager/-/merge_requests/20