[⬅ Volver al índice](../README.md)

## TICKET-012
**Categoría:** Hardware

**Título:** La computadora se reinicia sola o muestra pantalla azul

**Descripción del usuario:**
> Mi compu se ha estado reiniciando sola, a veces sale una pantalla azul con letras y números y se reinicia. Pasa como 2-3 veces al día, en cualquier momento.

**Diagnóstico paso a paso:**
1. Preguntar si el reinicio ocurre haciendo alguna tarea específica o es completamente aleatorio.
2. Pedir el código de error de la pantalla azul si lo alcanzó a ver o tomar foto (ej. "MEMORY_MANAGEMENT", "IRQL_NOT_LESS_OR_EQUAL") — orienta la causa.
3. Revisar el Visor de eventos de Windows (Registro del sistema) buscando eventos de BugCheck alrededor de la hora del reinicio.
4. Revisar temperatura del equipo — sobrecalentamiento es causa común, sobre todo en laptops con ventiladores sucios.
5. Verificar si hubo una actualización de drivers o de Windows reciente coincidiendo con el inicio del problema.
6. Ejecutar Windows Memory Diagnostic si se sospecha de un módulo de RAM defectuoso.

**Solución aplicada:**
- El Visor de eventos mostró errores de BugCheck consistentes con fallas de memoria (MEMORY_MANAGEMENT).
- Se ejecutó el diagnóstico de memoria de Windows y se confirmó un error en uno de los módulos RAM.
- Se reemplazó el módulo defectuoso.
- Se monitoreó el equipo por 2 días sin nuevos reinicios ni pantallas azules, confirmando la resolución.

---

[⬅ Volver al índice](../README.md)
