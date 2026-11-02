---
description: Commit, merge a main y actualización de PLAN.md
argument-hint: [número de tarea]
---

Tarea: $ARGUMENTS (si está vacío, la que esté "en revisión").

1. Ejecuta una última vez la Verificación. Si falla, detente.
2. Marca la tarea como "hecha" en PLAN.md y añade una línea al Registro
   (fecha, tarea, notas relevantes o decisiones nuevas).
3. Commit con mensaje convencional (feat:/fix:/chore:… + "(tarea N)").
4. Merge a main y borra la rama local.
5. Cuenta las tareas cerradas desde la última replanificación: si son 3 o
   más, sugiere replanificar con el subagente `arquitecto`.
6. Indica cuál es la siguiente tarea disponible.
