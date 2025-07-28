Ejemplo del archivo config.development.js
```js
module.exports = {

msConfig: {

timeOut: 40000

},

amqp: {

exchangeName: 'general-event',

paramsConnection: {

user: process.env.RABBIT_USER,

pass: process.env.RABBIT_PASS,

server: process.env.RABBIT_HOST,

vhost: process.env.RABBIT_VHOST,

protocol: process.env.RABBIT_PROTOCOL,

port: process.env.RABBIT_PORT,

},

},

services: {

apiPassthrough: process.env.API_PASSTHROUGH_URL, // ESTO

apiStoreManager: process.env.API_STOREMANAGER_URL // ESTO

},

businessTask: {

verifyRewardsCard: 'verificar_tarjeta_recompensas'

},

cipherConfig: {

cipherEnable: true

},

domainsWhitelist: [

'https://api-test.fif.tech',

'https://cmr-mx-onboarding-test.fif.tech',

'https://branch-solicitudes-test.falabella.com.mx',

'https://solicitudes-test.falabella.com.mx',

'http://localhost',

'http://localhost:8080',

'http://127.0.0.1:8080',

'http://127.0.0.1',

'file://'

]

};
```

#### MR de referencia
- Soporte para nullplatform: https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-rewards-card-manager/-/merge_requests/39#bde78f313e5e4d0170c8da4a22e81290f67a0dd7
