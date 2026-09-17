[⬅ Volver al índice](../README.md)

## TICKET-002
**Categoría:** Impresoras

**Título:** No puede imprimir en la impresora de red del segundo piso

**Descripción del usuario:**
> Buenas, necesito imprimir unos documentos urgentes y la impresora del pasillo no me deja, sale un error que dice algo de que no se puede conectar. Ayer sí funcionaba bien.

**Diagnóstico paso a paso:**
1. Pedir el mensaje de error exacto (o captura de pantalla).
2. Preguntar si otros usuarios de la misma impresora tienen el mismo problema o es solo este equipo.
3. Hacer ping a la IP configurada de la impresora desde el equipo del usuario.
4. Verificar si la IP de la impresora cambió (muy común cuando la impresora usa DHCP en vez de IP fija).
5. Revisar la cola de impresión local por trabajos atascados.
6. Verificar que el puerto de impresora configurado coincida con la IP actual del dispositivo.
7. Si el ping falla desde varios equipos, revisar el estado físico/de red de la impresora directamente.

**Solución aplicada:**
- El ping a la IP del driver no respondió: la impresora había tomado una IP distinta por DHCP tras un reinicio.
- Se confirmó la IP actual desde el panel de la impresora.
- Se actualizó la IP en las propiedades del puerto en el equipo del usuario.
- Se recomendó configurar una reserva DHCP para esa impresora y evitar que vuelva a pasar.
- Se confirmó impresión de página de prueba exitosa.

---

[⬅ Volver al índice](../README.md)
