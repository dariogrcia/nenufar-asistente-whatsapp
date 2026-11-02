# Asistente WhatsApp — Centro Nenúfar

Asistente virtual por WhatsApp para [Centro Nenúfar](https://centronenufar.com/):
gestión de citas en Google Calendar, atención a clientes nuevos y existentes,
dos administradores y listas de difusión de promociones.

En fase de planificación. El alcance y el estado están en [PLAN.md](PLAN.md);
las convenciones técnicas, en [AGENTS.md](AGENTS.md).

## Cómo se trabaja
Claude Code planifica y revisa; Codex (plugin `codex@openai-codex`) implementa.
Ciclo por tarea: `/siguiente-tarea` → `/revisar-tarea` → `/cerrar-tarea`.
