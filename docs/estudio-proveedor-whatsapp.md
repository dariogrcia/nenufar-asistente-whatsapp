# Estudio: proveedor de WhatsApp API para Centro Nenúfar

Fecha: 2026-11-02. Requisito: usar el **número actual** del centro.

## 1. Qué se paga siempre (lo cobra Meta, da igual el proveedor)
Tarifas de Meta para destinatarios en España (por mensaje entregado, + IVA):

| Categoría | Ejemplo en Nenúfar | Precio |
|---|---|---|
| Marketing (plantilla) | Promociones, difusiones | 0,0585 € |
| Utility (plantilla) | Recordatorio 24 h antes, confirmación | 0,0166 € |
| Service (texto libre en la ventana de 24 h) | Respuestas del bot cuando el cliente escribe | 0,0166 € a partir del mensaje 1.001 del mes |

- Desde el **1-oct-2026** Meta vuelve a cobrar los mensajes de servicio (1.000 gratis al
  mes por número) y las plantillas utility dentro de la ventana de 24 h dejan de ser gratis.
- Los mensajes que **envía el cliente** nunca se cobran.
- Consecuencia de diseño: el bot debe responder en **pocos mensajes** (botones y listas
  interactivas, nada de partir una respuesta en tres).

## 2. El número actual: "Coexistence"
Meta permite tener el mismo número en la app WhatsApp Business **y** en la Cloud API a
la vez: el personal sigue usando la app en el móvil y los mensajes se reflejan en ambos.
Se importa hasta 6 meses de historial.

Limitaciones que afectan:
- En la app se pierden las **listas de difusión**, los grupos, los mensajes temporales y
  las llamadas. Las difusiones pasarán a hacerse por la API (con plantillas), que es justo
  lo que queremos.
- Los dispositivos vinculados se desvinculan y hay que volver a vincular los compatibles
  (no sirven WhatsApp para Windows ni WearOS).
- No se puede tener la insignia azul (OBA); como alternativa está Meta Verified.
- Límite de 20 mensajes/segundo: de sobra para el centro.
- **Solo pueden activarlo un Solution Partner (BSP) o un Tech Provider**: no se puede
  hacer "a pelo" con la Cloud API sin uno de los dos.

## 3. Opciones

| Opción | Cuota fija | Recargo por mensaje | Coexistence | Esfuerzo de puesta en marcha |
|---|---|---|---|---|
| **A. 360dialog Regular** | 49 €/mes por número | 0 (Meta sin margen) | Sí, documentado | Bajo: alta guiada, soporte 24/7 (<4 h) |
| B. Meta Cloud API directa con Darío/Vertex como Tech Provider | 0 € | 0 | Sí | Alto: verificación de empresa, revisión de la app por Meta e implementar el alta guiada (Embedded Signup). Semanas |
| C. Twilio | 0 € | 0,005 $ por mensaje, de entrada y de salida | Sin confirmar en su documentación | Medio |
| D. SaaS con bandeja propia (WATI, Respond.io…) | 50–200 €/mes | Varía | Varía | No encaja: el bot lo hacemos nosotros |

**Calidad:** A, B y C usan por debajo la misma Cloud API de Meta, así que la entrega de
mensajes es idéntica. Lo que cambia es el soporte, el alta y si hay un intermediario más.

## 4. Coste mensual estimado (escenario medio, a validar con datos reales)
Supuestos: 400 citas/mes, 8 mensajes del bot por cita, 400 recordatorios y 1 campaña/mes
a 800 clientes con consentimiento.

| Concepto | Cálculo | € |
|---|---|---|
| Servicio | (3.200 − 1.000 gratis) × 0,0166 | 36,5 |
| Recordatorios | 400 × 0,0166 | 6,6 |
| Promoción | 800 × 0,0585 | 46,8 |
| **Meta (sin IVA)** | | **≈ 90** |
| Opción A, 360dialog | + 49 | **≈ 139** |
| Opción C, Twilio | + ~8.000 mensajes × 0,005 $ | **≈ 127** |
| Opción B, directa | + 0 | **≈ 90** |

La promoción es la partida que más pesa: cada campaña a 800 personas cuesta unos 47 €.

## 5. Recomendación inicial (D1 sigue en estudio)
**Opción A: 360dialog Regular con Coexistence.**
- Es la única que cumple a la vez: número actual, coexistence documentado, sin margen sobre
  Meta, soporte, y arranque en días en lugar de semanas.
- Twilio sale parecido en coste, pero el coexistence no está confirmado y su recargo crece
  con el volumen (también cobra los mensajes de entrada).
- **Revisar más adelante la opción B** si Vertex Studio va a vender más asistentes de
  WhatsApp: ser Tech Provider ahorra 49 €/mes por cliente y es un activo del estudio. El
  número se puede migrar después entre proveedores.
- El código se escribe contra la Cloud API de Meta (360dialog la expone casi tal cual)
  y detrás de un adaptador, para poder cambiar de proveedor sin rehacer el bot.

## 5 bis. Alternativas de bajo coste fijo (en estudio)
- **Tech Provider propio (opción B):** requiere verificar la empresa en Meta, una app de
  Meta con acceso avanzado a `whatsapp_business_messaging` y `whatsapp_business_management`
  (App Review con política de privacidad y dos vídeos de demostración), implementar
  Embedded Signup con Coexistence y los webhooks. El cliente paga a Meta con su propio
  método de pago. Meta no publica plazos. Reutilizable para otros clientes de Vertex.
  Fuente: https://developers.facebook.com/docs/whatsapp/solution-providers/get-started-for-tech-providers
- **APIs no oficiales (Baileys, whatsapp-web.js, Evolution API): descartadas.** Casi gratis,
  pero incumplen los términos de WhatsApp y suponen un riesgo real de bloqueo del número.
- **Ahorro con cualquier proveedor:** que el personal responda desde la app (con
  coexistence esos mensajes no los cobra Meta), mantener el bot por debajo de 1.000
  mensajes de servicio al mes, entradas desde anuncios Click-to-WhatsApp (72 h gratis) y
  promociones segmentadas.
- Camino posible: arrancar con 360dialog y migrar a Tech Provider propio cuando Meta lo
  apruebe (lo permite D2).

## 6. Consentimiento para promociones (pregunta 3)
La idea de "el primer mensaje les pide que acepten" tiene un riesgo: **la política de
Meta exige el opt-in antes de enviar mensajes iniciados por la empresa**. Un mensaje
masivo y no esperado a todo el Excel genera bloqueos y denuncias, que bajan la calificación
de calidad del número y pueden limitarlo. Y el número es el que usa el centro a diario.
Propuesta:
1. Los clientes del Excel **con** consentimiento documentado entran directamente en la lista.
2. Al resto se le pide el consentimiento **cuando escriba él** (ventana de 24 h, mensaje de
   servicio), al confirmar una cita o en el propio centro (QR o enlace wa.me).
3. Si aun así se quiere un aviso inicial al Excel: solo a clientes recientes, en lotes
   pequeños, con un texto claro y una opción de "BAJA" a un toque. Confirmarlo con la
   asesoría (RGPD y art. 21 LSSI) antes de lanzarlo.
4. Guardar fecha, canal y texto de cada consentimiento, y procesar las bajas al instante.

## Fuentes
- Meta, precios: https://developers.facebook.com/docs/whatsapp/pricing
- Meta, coexistence: https://developers.facebook.com/docs/whatsapp/embedded-signup/custom-flows/onboarding-business-app-users
- 360dialog, precios: https://360dialog.com/pricing
- 360dialog, coexistence: https://docs.360dialog.com/docs/resources/phone-numbers/coexistence
- Twilio, alta: https://www.twilio.com/docs/whatsapp/self-sign-up
- Cambios de oct-2026 y tarifas en España: https://www.agenciareinicia.com/en/blog/whatsapp-business-api-price-changes-in-october-2026-what-this-means-for-your-bill/
