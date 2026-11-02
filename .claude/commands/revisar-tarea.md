---
description: Revisa la tarea actual contra el plan y ejecuta la verificación
argument-hint: [número de tarea]
---

Tarea: $ARGUMENTS (si está vacío, la que esté "en curso" en PLAN.md).

IMPORTANTE — límite real de la herramienta: de los comandos del plugin, Claude
solo puede lanzar por su cuenta `/codex:rescue` y `/codex:setup`. `/codex:result`,
`/codex:status`, `/codex:review`, `/codex:adversarial-review`, `/codex:cancel` y
`/codex:transfer` llevan `disable-model-invocation: true`: los tiene que escribir
Darío. Cuando haga falta uno, PÁRATE y pídeselo con el comando exacto; no finjas
haberlo ejecutado ni inventes su resultado.

1. Si Codex trabajó en background y aún no tienes su salida, detente y pide:
   "Escribe `/codex:result` y pégame la salida". Continúa cuando la tengas.
2. Usa el subagente `revisor` sobre la tarea.
3. Si la tarea tiene "Crítica: sí", detente al terminar el paso 2 y pide:
   "Esta tarea es crítica: escribe `/codex:adversarial-review` centrado en
   <archivos de la tarea>". Integra su resultado en el veredicto.
4. Según el veredicto:
   - APROBADA → marca "en revisión" y dime que puedo lanzar /cerrar-tarea.
   - CAMBIOS MENORES → corrígelos tú y vuelve a ejecutar la verificación.
   - CAMBIOS DE FONDO → resume el feedback concreto y propón el
     /codex:rescue --resume correspondiente; espera mi confirmación.
