# Codex Multi-Agent: configuración básica con Architect, Backend y Persistence

Referencia oficial:  
https://developers.openai.com/codex/multi-agent

## Objetivo

Configurar un proyecto con **multi-agent en Codex** para dividir responsabilidades entre:

- `architect`: arquitectura del proyecto
- `backend`: API con Node.js y Express
- `persistence`: persistencia con Prisma y SQLite

La idea es refactorizar una API simple de Express que hoy devuelve una lista en memoria, para mover esos datos a SQLite usando Prisma.

---

## 1. Estructura recomendada

```text
repo/
├─ .codex/
│  ├─ config.toml
│  └─ agents/
│     ├─ backend.toml
│     └─ persistence.toml
```

---

## 2. Crear la estructura desde terminal

```bash
mkdir -p .codex/agents
touch .codex/config.toml .codex/agents/backend.toml .codex/agents/persistence.toml
```

---

## 3. Configuración principal de agentes

Archivo: `repo/.codex/config.toml`

```toml
[agents.architect]
description = "Software architect"

[agents.backend]
description = "Backend engineer for Node.js and Express"
config_file = "agents/backend.toml"

[agents.persistence]
description = "Persistence and database engineer"
config_file = "agents/persistence.toml"
```

### Explicación breve

- `architect` define la estructura general y la organización del proyecto.
- `backend` se enfoca en Express, JavaScript moderno y capas de la API.
- `persistence` se enfoca en base de datos, Prisma, SQLite y acceso a datos.

---

## 4. Configuración del agente backend

Archivo: `repo/.codex/agents/backend.toml`

```toml
model = "gpt-5.4"
sandbox_mode = "danger-full-access"

developer_instructions = """
Utiliza Node.js con Express y JavaScript moderno.
Usa ES Modules (import/export) en lugar de CommonJS.
Prefiere async/await en lugar de cadenas de promesas.
Organiza el código con una estructura clara de controllers y services.
Mantén los controllers delgados y mueve la lógica de negocio a los services.
Sigue un estilo de código limpio y legible propio de Node.js/Express.
Usa nombres claros, funciones pequeñas y manejo de errores simple.
No mezcles lógica de persistencia directamente en los controllers.
"""
```

### Responsabilidad del agente backend

- modernizar el código
- usar ES Modules
- usar async/await
- separar `controller` y `service`
- mantener estilo limpio en Express

---

## 5. Configuración del agente persistence

Archivo: `repo/.codex/agents/persistence.toml`

```toml
model = "gpt-5.4"
sandbox_mode = "danger-full-access"

developer_instructions = """
Utilice Express con Prisma ORM y SQLite.
Archivo de base de datos: ./prisma/dev.db
Utilice las migraciones de Prisma.
Los controladores no deben acceder directamente a la base de datos.
Utilice el patrón de repositorio/servicio.
"""
```

### Responsabilidad del agente persistence

- definir Prisma
- configurar SQLite
- crear migraciones
- mover la persistencia a repository/service
- evitar acceso directo a base de datos desde controllers

---

## 6. Prompt de ejemplo

Usa este prompt para pedir el refactor del proyecto:

```text
Usa agentes architect, backend y persistence para que refactoricen esta API de Express para mover los features en memoria a SQLite usando Prisma.
Modernicen el código a JavaScript moderno (ES Modules, async/await) y separen controller, service y repository.
Mantengan el endpoint GET /features y creen el modelo, migración y seed inicial con los textos actuales.
```

---

## 7. Datos actuales en memoria

Ejemplo de datos que hoy están hardcodeados y que deben pasar a la base de datos:

```js
const multiAgentFeatures = Object.freeze([
  "Permite dividir trabajo en subtareas independientes.",
  "Ejecuta analisis y implementacion en paralelo para reducir tiempo.",
  "Asigna responsabilidades claras por archivo o modulo.",
  "Facilita validar cambios mientras otro agente sigue desarrollando.",
  "Mejora la escalabilidad en tareas grandes con coordinacion central."
]);
```

La meta es que estos textos se inserten inicialmente en SQLite mediante una migración o seed.

---

## 8. Confirmar los cambios con Git

Una vez revisados los cambios:

```bash
git add .
git commit -m "agregado mejoras de agentes architect, backend y persistence"
```

---

## 9. Recomendación práctica

Antes de pedir cambios grandes al agente, conviene guardar un checkpoint:

```bash
git add .
git commit -m "checkpoint antes de multi-agent refactor"
```

Así puedes volver atrás fácilmente si el resultado no te convence.

---

## 10. Resultado esperado

Después del refactor, el proyecto debería tener como mínimo:

- API Express modernizada
- ES Modules
- async/await
- separación por capas:
  - controller
  - service
  - repository
- Prisma configurado
- SQLite funcionando
- endpoint `GET /features`
- seed o migración inicial con los features actuales

---

## Resumen

Esta configuración permite usar **multi-agent en Codex** para dividir responsabilidades y hacer refactors más ordenados:

- `architect` piensa la estructura
- `backend` moderniza e implementa la API
- `persistence` mueve los datos a SQLite con Prisma

