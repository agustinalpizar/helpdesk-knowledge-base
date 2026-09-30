[⬅ Volver al índice](../README.md)

## TICKET-014
**Categoría:** Software

**Título:** Un programa se cierra solo apenas se abre

**Descripción del usuario:**
> Cuando abro el sistema de facturación se abre un segundito y se cierra solo, no me deja ni empezar a trabajar. Ayer funcionaba bien.

**Diagnóstico paso a paso:**
1. Confirmar el nombre exacto del programa y su versión.
2. Preguntar si muestra algún mensaje antes de cerrarse o se cierra sin aviso.
3. Revisar el Visor de eventos buscando el error de aplicación: `Get-WinEvent -FilterHashtable @{LogName='Application'; ID=1000} -MaxEvents 5` devuelve el nombre del ejecutable, el módulo que falló y el código de excepción.
4. Confirmar si hubo una actualización reciente de Windows, del propio programa, o instalación de otro software que pudiera generar conflicto.
5. Verificar si el problema ocurre con otro usuario en el mismo equipo, o con el mismo usuario en otro equipo — aísla si es del perfil, del equipo o del programa.
6. Revisar si el antivirus puso en cuarentena algún archivo del programa.

**Solución aplicada:**
- El evento 1000 identificó el módulo que fallaba: una DLL del propio programa, con código de excepción de módulo no encontrado.
- Se revisó la cuarentena del antivirus y ahí estaba el archivo: se había marcado como falso positivo tras una actualización de firmas.
- Se restauró el archivo desde la cuarentena y se agregó la carpeta del programa a las exclusiones, coordinándolo con el responsable de seguridad.
- Se ejecutó `sfc /scannow` para descartar daño adicional en archivos del sistema.
- Se confirmó apertura y funcionamiento normal.
- Se documentó el caso para revisar si se repite en otros equipos tras la misma actualización.

---

[⬅ Volver al índice](../README.md)
