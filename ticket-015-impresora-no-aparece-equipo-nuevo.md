[⬅ Volver al índice](../README.md)

## TICKET-015
**Categoría:** Impresoras

**Título:** La impresora de red no aparece en la lista al configurarla en un equipo nuevo

**Descripción del usuario:**
> Me dieron una compu nueva y estoy tratando de agregar la impresora de la oficina pero no aparece en la lista cuando busco impresoras de red.

**Diagnóstico paso a paso:**
1. Confirmar el método usado para buscarla (descubrimiento automático de Windows, o intento de agregarla por nombre/IP directo).
2. Verificar que el equipo nuevo esté en la misma red/VLAN que la impresora — en subredes distintas, el descubrimiento automático normalmente no funciona.
3. Hacer ping a la IP de la impresora desde el equipo nuevo para confirmar conectividad básica.
4. Verificar si el descubrimiento de red está activado (perfil de red configurado como privada vs. pública en Windows).
5. Si el ping funciona pero no aparece en la búsqueda automática, agregarla manualmente por IP.

**Solución aplicada:**
- El ping fue exitoso, pero el perfil de red del equipo estaba como "Pública" en vez de "Privada", lo cual desactiva el descubrimiento de red por defecto en Windows.
- Se cambió el perfil a "Privada".
- Se optó, de todas formas, por agregar la impresora manualmente por IP (Agregar impresora → "La impresora que quiero no está en la lista" → Agregar por dirección TCP/IP) para mayor confiabilidad.
- Se confirmó impresión de página de prueba exitosa.

---

[⬅ Volver al índice](../README.md)
