---
description: Crea la rama de la siguiente tarea y la delega a Codex
argument-hint: [número de tarea]
---

Tarea solicitada: $ARGUMENTS (si está vacío, la primera "pendiente" de PLAN.md
cuyas dependencias estén hechas).

1. Lee la tarea en PLAN.md. Si le falta información para ser autocontenida,
   complétala primero en PLAN.md y dímelo.
2. Si es trivial (una línea, texto, config) o es maquetado visual fino, no la
   delegues: hazla tú y pasa a revisión.
3. Asegúrate de estar en main actualizado y sin cambios pendientes; crea la
   rama `tarea-N-slug`.
4. Marca la tarea como "en curso" en PLAN.md.
5. Delega con /codex:rescue (añade --background si la tarea dice
   "Modo: background"):
   "Implementa la tarea N de PLAN.md. Sigue AGENTS.md. Respeta 'No hacer' y
   las decisiones referenciadas. Termina ejecutando la Verificación y reporta
   el resultado."
6. Si es background, avísame y propón en qué avanzar mientras tanto. Recuerda
   que el seguimiento (`/codex:status`) y la recogida del resultado
   (`/codex:result`) los tengo que escribir yo: pídemelos, no los intentes.
