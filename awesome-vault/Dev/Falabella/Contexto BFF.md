# 🧠 Contexto para Cursor AI — Proyecto Backend con ExpressJS

Este documento sirve como guía para establecer el **contexto del proyecto** cuando se trabaje con Cursor AI u otra IA que apoye en desarrollo. Copia y pega este contenido al iniciar una conversación con la IA para que entienda las reglas del entorno.

---

## ⚙️ Stack general

- Lenguaje: **JavaScript**
- Framework: **ExpressJS**
- No se debe modificar el archivo `app.js`.

---

## ✅ Convenciones del proyecto

- Todos los `res.send()` deben reemplazarse por `sendResponse()` importado desde `common-lib`.
- El import debe hacerse así:
  ```js
 const { sendResponse } = require('onboarding-common-lib').expressJSCipherUtils;
  ```

---

## 🧪 Migración de pruebas unitarias

Estamos migrando todos los tests a **Jest**. Las siguientes reglas aplican:

- ❌ **No usar**: `mockery`, `sinon`, `chai`.
- ✅ Usar **solo Jest**, incluyendo sus utilidades de mocks y asserts.
- ❌ No se debe crear `config.test.js` dentro de app/configs.
- ✅ Crear solo un `jest.config.js` centralizado.
- Todos los tests nuevos o migrados deben seguir la estructura y convenciones nativas de Jest.
``` json
module.exports = {

collectCoverage: true,

coverageReporters: ['json-summary', 'text', 'html', 'lcov'],

coverageDirectory: './coverage',

testTimeout: 10000,

testMatch: ['**/*.spec.js'],

coverageThreshold: {

global: {

branches: 80,

functions: 80,

lines: 80,

statements: 80,

},

}

};
```
- Modificar los scritps de test/coverage de esta manera:
``` json
"unit-test": "jest",

"unit-test-w": "jest --watch",

"unit-test-n-w": "jest --watch --verbose",

"coverage": "jest --coverage",
```
---

## 🧹 Linter

- Usamos **ESLint actualizado** (última versión disponible).
- Configurado para trabajar con **ECMAScript 2020**:
  ```json
{

"root": true,

"env": {

"es6": true,

"node": true,

"browser": true

},

"plugins": [

"security-node"

],

"extends": [

"airbnb",

"plugin:import/warnings",

"plugin:security-node/recommended"

],

"parserOptions": {

"ecmaVersion": 2020,

"sourceType": "module",

"ecmaFeatures": {

"jsx": true

}

},

"rules": {

"class-methods-use-this": "off",

"arrow-body-style":"off",

"comma-dangle": "off",

"indent": [2, 2],

"max-len": [2, 200],

"complexity": [2, 10],

"max-lines":[2, 180]

  

}

  

}}
  ```
- Seguir reglas definidas en el archivo `.eslintrc`.

---

## 🧠 Instrucciones para uso de IA

Al utilizar Cursor AI o herramientas similares:

- Asegúrate de que las sugerencias respeten las siguientes condiciones:
  - Usar `sendResponse()` y no `res.send()`.
  - Las pruebas deben generarse con Jest puro, sin otras libs.
  - No modificar ni tocar `app.js`.
  - Seguir el estilo definido por ESLint.
- Puedes pegar este contexto al iniciar una sesión con IA para mejores resultados.

---

**Última revisión:** {{poner fecha aquí}}
