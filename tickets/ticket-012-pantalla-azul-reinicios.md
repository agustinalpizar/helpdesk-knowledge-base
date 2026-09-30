[⬅ Volver al índice](../README.md)

## TICKET-012
**Categoría:** Hardware

**Título:** La computadora se reinicia sola o muestra pantalla azul

**Descripción del usuario:**
> Mi compu se ha estado reiniciando sola, a veces sale una pantalla azul con letras y números y se reinicia. Pasa como 2-3 veces al día, en cualquier momento.

**Diagnóstico paso a paso:**
1. Preguntar si el reinicio ocurre haciendo alguna tarea específica o es completamente aleatorio.
2. Pedir el código de error de la pantalla azul si lo alcanzó a ver o tomar foto (ej. "MEMORY_MANAGEMENT", "IRQL_NOT_LESS_OR_EQUAL") — orienta la causa.
3. Revisar el Visor de eventos buscando el evento de parada: `Get-WinEvent -FilterHashtable @{LogName='System'; ID=1001} -MaxEvents 5` devuelve los registros de BugCheck con el código y los parámetros de cada pantalla azul.
4. Confirmar que existan volcados de memoria en `C:\Windows\Minidump`: su presencia y fecha acotan cuándo empezó el problema.
5. Revisar temperatura del equipo — sobrecalentamiento es causa común, sobre todo en laptops con ventiladores sucios.
6. Verificar si hubo una actualización de drivers o de Windows reciente coincidiendo con el inicio del problema: `Get-HotFix | Sort-Object InstalledOn -Descending | Select -First 5`.
7. Ejecutar el diagnóstico de memoria de Windows (`mdsched.exe`) si el código de parada apunta a RAM.

**Solución aplicada:**
- Los eventos 1001 del registro del sistema mostraron BugCheck repetidos con código `MEMORY_MANAGEMENT` (0x0000001A), y había volcados correspondientes en `C:\Windows\Minidump`.
- `Get-HotFix` no mostró actualizaciones recientes que coincidieran con el inicio del problema, lo que descartó un driver nuevo como causa.
- Se ejecutó `mdsched.exe` y el diagnóstico reportó errores de hardware en la memoria.
- Se probó arrancando con un solo módulo a la vez para aislar cuál fallaba, y se reemplazó el defectuoso.
- Se monitoreó el equipo por 2 días sin nuevos reinicios ni pantallas azules, confirmando la resolución.

---

[⬅ Volver al índice](../README.md)
