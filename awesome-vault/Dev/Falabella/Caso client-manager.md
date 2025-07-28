Bug reportado: https://jira.falabella.tech/browse/OME-2713
MR fix: https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-client-manager/-/merge_requests/40

Se certifico el 19/12/2025
***aparentemente nunca se paso a PROD

Revisando los release notes, no se encuentra la imagen generada de este MR(20241205-173423-BUILD)

Actualmente PROD tienes los cambios de la client-manager que se realizaron en este MR:
https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-client-manager/-/merge_requests/38
Que genero este tag: 20241121-193935-BUILD 

***este cambio fue un mes antes de bug OME-2713

El ultimo cambio que se realizo en la API fue este MR:
https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-client-manager/-/merge_requests/45 este genero el siguiente tag: 20250414-163541-BUILD

***dicho cambio se realizo en el PaP de 15/05/2025


El tag 20250414-163541-BUILD se paso a PROD en el release note https://confluence.falabella.tech/pages/viewpage.action?pageId=713629333 (15/05/2025) mientras que antes de eso, el ultimo cambio que habia pasado a PROD fue en este release note https://confluence.falabella.tech/pages/viewpage.action?pageId=637709747 (05/12/2024) y bueno, el fix del bug OME-2713 nunca se paso a PROD.