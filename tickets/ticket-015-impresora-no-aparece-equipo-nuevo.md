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
4. Verificar el perfil de red con `Get-NetConnectionProfile`: si `NetworkCategory` es `Public`, Windows desactiva el descubrimiento de red y la impresora no aparecerá en la búsqueda automática aunque sea alcanzable.
5. Si el ping funciona pero no aparece en la búsqueda automática, agregarla manualmente por IP.

**Solución aplicada:**
- El `ping` a la impresora respondió, confirmando conectividad, pero `Get-NetConnectionProfile` devolvió `NetworkCategory : Public`, lo que desactiva el descubrimiento de red por defecto en Windows.
- Se corrigió el perfil con `Set-NetConnectionProfile -InterfaceAlias Ethernet -NetworkCategory Private`.
- Se optó, de todas formas, por agregar la impresora manualmente por IP (Agregar impresora → "La impresora que quiero no está en la lista" → Agregar por dirección TCP/IP) para mayor confiabilidad.
- Se confirmó impresión de página de prueba exitosa.

---

[⬅ Volver al índice](../README.md)
