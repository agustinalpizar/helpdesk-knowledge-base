[⬅ Volver al índice](../README.md)

## TICKET-002
**Categoría:** Impresoras

**Título:** No puede imprimir en la impresora de red del segundo piso

**Descripción del usuario:**
> Buenas, necesito imprimir unos documentos urgentes y la impresora del pasillo no me deja, sale un error que dice algo de que no se puede conectar. Ayer sí funcionaba bien.

**Diagnóstico paso a paso:**
1. Pedir el mensaje de error exacto (o captura de pantalla).
2. Preguntar si otros usuarios de la misma impresora tienen el mismo problema o es solo este equipo.
3. Ver a qué IP está apuntando realmente el equipo: `Get-Printer | Format-List Name,PortName` y luego `Get-PrinterPort -Name <puerto> | Format-List Name,PrinterHostAddress`.
4. Hacer `ping` a esa IP desde el equipo del usuario.
5. Contrastar con la IP real del dispositivo, impresa en la página de configuración que la impresora genera desde su propio panel — muy común que hayan divergido cuando la impresora toma DHCP en vez de IP fija.
6. Revisar la cola local por trabajos atascados: `Get-PrintJob -PrinterName <nombre>`; si el spooler quedó trabado, `Restart-Service Spooler`.
7. Si el ping falla desde varios equipos, revisar el estado físico/de red de la impresora directamente.

**Solución aplicada:**
- El `ping` a la IP configurada en el puerto no respondió, mientras que la página de configuración impresa desde el panel mostraba otra IP: la impresora había tomado una dirección distinta por DHCP tras un reinicio.
- Se actualizó la dirección del puerto en el equipo del usuario (Propiedades de impresora → Puertos → Configurar puerto).
- Se recomendó configurar una reserva DHCP para esa impresora y evitar que vuelva a pasar.
- Se confirmó impresión de página de prueba exitosa.

---

[⬅ Volver al índice](../README.md)
