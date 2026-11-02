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
- Calendario: ¿un calendario único o uno por profesional/cabina? (sin decidir; el
  diseño debe admitir ambos por configuración). ¿Duración y precio por servicio?
  ¿Horario y festivos?
- Excel de clientes: columnas exactas y quién tiene consentimiento documentado.
- Conversación: ¿IA (LLM) con herramientas o flujo guiado con menús? ¿Cuándo se
  deriva a una persona?
- Recordatorios automáticos de cita (24 h antes) y gestión de no-shows: ¿entran?
- Volumen real: citas/mes, clientes en el Excel, campañas/mes (para recalcular coste).
- Despliegue, fecha de entrega y si habrá panel web además de WhatsApp.

## Fuera de alcance
<!-- se rellena al cerrar el plan -->

## Decisiones
<!-- Cada decisión con ID. Las tareas las referencian. Codex no las cambia. -->
- **D1 — Proveedor WhatsApp (EN ESTUDIO, sin decidir):** dos candidatos, ambos con
  Coexistence sobre el número actual: (a) 360dialog Regular, 49 €/mes, arranque rápido;
  (b) Meta directa con Darío/Vertex como Tech Provider, 0 € de plataforma pero
  verificación + App Review + Embedded Signup propio. Descartadas las APIs no oficiales
  (riesgo de bloqueo del número). Ver `docs/estudio-proveedor-whatsapp.md`.
- **D2 — Adaptador de mensajería:** el bot habla con una interfaz propia
  (`MessagingProvider`); la implementación de 360dialog vive detrás. Motivo: poder
  migrar a Cloud API directa (Tech Provider) sin rehacer el bot.
- **D3 — Mensajes mínimos:** respuestas agrupadas y con botones/listas interactivas.
  Motivo: desde oct-2026 Meta cobra cada mensaje de servicio a partir del 1.001/mes.
- **D4 — Consentimiento:** solo reciben promociones los clientes con opt-in registrado
  (fecha, canal, texto). Opt-in desde conversación iniciada por el cliente, confirmación
  de cita o QR en el centro; baja inmediata con "BAJA". Nada de envío masivo inicial al
  Excel sin validación legal.

## Tareas
<!-- Se generan con /nuevo-proyecto. Plantilla en ~/kit-claude-codex/plantilla-proyecto/PLAN.md -->

## Registro
- 2026-11-02 — Estudio de proveedor WhatsApp (docs/estudio-proveedor-whatsapp.md); D1 en estudio, D2–D4 propuestas.
- 2026-11-02 — Repo creado con el kit Claude + Codex y brief inicial.
