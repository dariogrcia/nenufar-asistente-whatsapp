# AGENTS.md — Fuente de verdad técnica
<!-- Codex lee este archivo automáticamente. CLAUDE.md lo importa.
     Todo lo técnico va aquí, una sola vez. -->

## Proyecto
- Nombre: nenufar-asistente-whatsapp
- Cliente: Centro Nenúfar, centro de estética (https://centronenufar.com/)
- Objetivo en una frase: asistente virtual por WhatsApp que gestiona citas en Google Calendar,
  atiende a clientes nuevos y existentes y envía promociones a listas de difusión.

## Stack
<!-- Pendiente: se decide en /nuevo-proyecto y se registra como decisión en PLAN.md -->
- Framework:
- Lenguaje:
- Estilos:
- Base de datos:
- Despliegue:

## Comandos
- Instalar: `npm install`
- Desarrollo: `npm run dev`
- Tests: `npm test`
- Lint: `npm run lint`
- Build: `npm run build`

## Estructura
<!-- carpetas principales y qué va en cada una -->

## Convenciones
- Nombres: camelCase para variables/funciones, PascalCase para componentes.
- Idioma del código y comentarios: inglés. Textos de interfaz: español.
- Validación de entradas en el servidor, siempre.
- Nunca secretos en el código: usar variables de entorno (.env, no versionado).
- Cada función nueva con lógica de negocio lleva test.

## Reglas para quien implementa
- Implementa SOLO la tarea indicada de PLAN.md. No refactorices fuera de alcance.
- Respeta las decisiones de la sección "Decisiones" de PLAN.md; no las cambies.
- Si algo del plan es imposible o contradictorio, detente y explícalo en vez
  de improvisar.
- Termina ejecutando el comando de "Verificación" de la tarea y reporta el
  resultado.
