# PLAN.md

## Resumen
Asistente virtual por WhatsApp para Centro Nenúfar (centro de estética,
https://centronenufar.com/). Funciones previstas:

1. **Citas:** pedir, consultar, cambiar y cancelar citas sobre Google Calendar,
   según disponibilidad real.
2. **Administradores (2):** desde WhatsApp pueden ver la agenda, bloquear huecos,
   confirmar o mover citas y lanzar campañas.
3. **Clientes existentes:** se reconocen por su número; se importan los actuales.
4. **Clientes nuevos:** flujo de alta y bienvenida (datos mínimos, consentimiento,
   información de servicios).
5. **Promociones:** listas de difusión segmentadas, solo a clientes con
   consentimiento y con baja fácil.

Estado: **brief inicial**. Falta cerrar las preguntas abiertas con `/nuevo-proyecto`
antes de fijar stack, decisiones y tareas.

## Preguntas abiertas
- Canal: ¿WhatsApp Business Cloud API (Meta) directa o un proveedor (Twilio, 360dialog)?
  ¿Número nuevo o el actual del centro?
- Calendario: ¿un calendario único o uno por profesional/cabina? ¿Duración y
  precio por servicio? ¿Horario y festivos?
- Clientes existentes: ¿de dónde salen (Excel, software de gestión, Google Contacts)?
  ¿Qué datos hay y hay consentimiento para promociones?
- Conversación: ¿IA (LLM) con herramientas o flujo guiado con menús? ¿Cuándo se
  deriva a una persona?
- Recordatorios automáticos de cita (24 h antes) y gestión de no-shows: ¿entran?
- Promociones: WhatsApp exige plantillas aprobadas por Meta y opt-in; ¿frecuencia
  y volumen previsto?
- Despliegue y presupuesto mensual (hosting, coste por conversación de Meta).
- Fecha de entrega y si habrá panel web además de WhatsApp.

## Fuera de alcance
<!-- se rellena al cerrar el plan -->

## Decisiones
<!-- Cada decisión con ID. Las tareas las referencian. Codex no las cambia. -->

## Tareas
<!-- Se generan con /nuevo-proyecto. Plantilla en ~/kit-claude-codex/plantilla-proyecto/PLAN.md -->

## Registro
- 2026-11-02 — Repo creado con el kit Claude + Codex y brief inicial.
