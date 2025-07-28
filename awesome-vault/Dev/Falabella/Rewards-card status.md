Curps utilizadas con el nombre christmasvip
- [x] ropv950219htcmrc59
- [x] ropv950219htcmrc62
- [x] ropv950219htcmrc63
- [x] ropv950219htcmrc64
- [x] ropv950219htcmrc65
- [x] ropv950219htcmrc66
- [x] ropv950219htcmrc68
- [x] ropv950219htcmrc69

Curps utilizadas con el nombre christmasL
- [x] ropv950219htcmrc67
- [ ] 

## Pruebas realizadas

**QA:**
APK
- ropv950219htcmrc64
	- trajo logs de negocio (100% portainer)
	- hay registro en datadog
- ropv950219htcmrc65
	- trajo logs de negocio (100% portainer)
	- hay logs en kibana
	- hay registro en datadog
- ropv950219htcmrc66
	- no trajo logs de negocio (100% nullplatform)
	- hay logs en kibana
	- hay registro en datadog
- ropv950219htcmrc67
	- trajo logs de negocios (100% nullplatform)
	- hay registro en datadog
	- hay registro en kibana
Web QA
- ropv950219htcmrc62
	- trajo logs de negocios (X-NP-Upstream false)
	- hay registro en datadog
	-  NO ESTABA FUNCIONANDO KIBANA
- ropv950219htcmrc63
	- no trajo logs de negocios (X-NP-Upstream true)
	- hay registro en datadog
	- NO ESTABA FUNCIONANDO KIBANA
- ropv950219htcmrc67
	- trajo logs de negocios (X-NP-Upstream true)
	- hay registro en datadog
	- hay registro en kibana

---

## Logs
Kibana
- [x] Portainer
- [x] Nullplatform
Datadog
- [x] Portainer
- [x] Nullplatform
Logs de negocios
- [x] Portainer
- [x] Nullplatform


---

### Test cases QA
- [x] Probar 100% portainer
	- [x] Web
	- [x] App
- [x] Probar 100% nullplatform
	- [x] Web
	- [x] App
- [ ] Probar 50% nullplatform/portainer

---

#### Pendientes
- [x] Resuelvan ticket de no logs en kibana https://jira.falabella.tech/browse/SHDBP-435
- [x] Resolver no logs de negocios cuando las peticiones vienen de nullplatform
- [ ] Crear scope y asignar variables de entorno en ambiente prod
- [ ] Modificar el kong de PROD
- [ ] Modificar el stack file de prod
