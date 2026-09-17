[⬅ Volver al índice](../README.md)

## TICKET-014
**Categoría:** Software

**Título:** Un programa se cierra solo apenas se abre

**Descripción del usuario:**
> Cuando abro el sistema de facturación se abre un segundito y se cierra solo, no me deja ni empezar a trabajar. Ayer funcionaba bien.

**Diagnóstico paso a paso:**
1. Confirmar el nombre exacto del programa y su versión.
2. Preguntar si muestra algún mensaje antes de cerrarse o se cierra sin aviso.
3. Revisar el Visor de eventos (Registro de aplicación) buscando errores del proceso a la hora del cierre.
4. Confirmar si hubo una actualización reciente de Windows, del propio programa, o instalación de otro software que pudiera generar conflicto.
5. Verificar si el problema ocurre con otro usuario en el mismo equipo, o con el mismo usuario en otro equipo — aísla si es del perfil, del equipo o del programa.
6. Revisar si el antivirus puso en cuarentena algún archivo del programa.

**Solución aplicada:**
- El Visor de eventos mostró un error de falta de un archivo DLL del programa, coincidiendo con una actualización reciente de Windows que había dañado esa dependencia.
- Se reinstaló el programa por completo (desinstalación y reinstalación desde el instalador oficial) para restaurar los archivos faltantes.
- Se confirmó apertura y funcionamiento normal.
- Se documentó el caso para revisar si se repite en otros equipos tras la misma actualización.

---

[⬅ Volver al índice](../README.md)
