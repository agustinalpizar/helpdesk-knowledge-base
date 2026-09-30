[⬅ Volver al índice](../README.md)

## TICKET-004
**Categoría:** Hardware / Software

**Título:** Computadora muy lenta para abrir programas

**Descripción del usuario:**
> Mi compu está bien lenta, se tarda un montón en abrir Excel o Chrome, a veces se queda pensando y no responde. Ya la reinicié pero sigue igual.

**Diagnóstico paso a paso:**
1. Preguntar desde cuándo empezó y si coincide con alguna instalación, actualización o falta de espacio en disco.
2. Revisar Administrador de Tareas (`taskmgr`): uso de CPU, RAM y disco en reposo. Un disco al 100% de actividad con CPU baja apunta a almacenamiento, no a falta de memoria.
3. Medir el espacio libre real: `Get-PSDrive C` muestra usado y disponible. Un disco casi lleno es causa muy común de lentitud, sobre todo en SSD, porque se queda sin espacio para operar.
4. Revisar los programas de inicio y su impacto medido: pestaña Inicio del Administrador de tareas, columna *Impacto de inicio*.
5. Verificar actualizaciones de Windows corriendo en segundo plano.
6. Revisar si hay un análisis de antivirus en curso.
7. Si la lentitud es severa y persistente, revisar la salud del disco: `Get-PhysicalDisk | Select FriendlyName,MediaType,HealthStatus` y, para el detalle SMART, `wmic diskdrive get model,status`. Un disco degradado se comporta como lentitud generalizada antes de fallar del todo.

**Solución aplicada:**
- `Get-PSDrive C` mostró el disco al 95% de capacidad, y el Administrador de tareas lo confirmó con actividad de disco al 100% en reposo.
- `Get-PhysicalDisk` devolvió `HealthStatus: Healthy`, descartando un disco defectuoso.
- Se liberó espacio con el Liberador de espacio (`cleanmgr`) sobre archivos temporales y de actualización, más caché de navegador y descargas antiguas (con confirmación del usuario antes de borrar nada).
- Se deshabilitaron 4 programas innecesarios del inicio (Administrador de tareas → Inicio).
- Se verificó que el uso de CPU volvió a niveles normales y los programas abrieron con tiempos de respuesta normales.
- Se recomendó al usuario mantener al menos 15-20% de espacio libre en disco.

---

[⬅ Volver al índice](../README.md)
