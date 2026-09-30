[⬅ Volver al índice](../README.md)

## TICKET-013
**Categoría:** Red

**Título:** El equipo tiene acceso a la red local pero no a Internet

**Descripción del usuario:**
> Puedo ver la carpeta compartida y la impresora de la oficina, pero no me carga ninguna página de internet ni me llegan correos.

**Diagnóstico paso a paso:**
1. Confirmar el síntoma exacto: ¿el navegador dice "sin conexión" o carga infinitamente? ¿el ícono de red muestra advertencia de "sin Internet"?
2. Revisar la configuración IP del equipo (`ipconfig /all`): dirección IP, máscara, gateway y DNS asignados.
3. Hacer ping a la puerta de enlace (gateway) — si responde, el problema está más allá del gateway; si no, el problema es local.
4. Si el gateway responde, hacer ping a una IP pública conocida (ej. 8.8.8.8) para descartar problema de ruta vs. DNS.
5. Si el ping a IP pública funciona pero los sitios no cargan, sospechar de DNS: `nslookup google.com` y comparar contra un resolutor externo con `nslookup google.com 8.8.8.8`.
6. Trazar la ruta con `tracert 8.8.8.8` para ver en qué salto se corta: dentro de la red o ya en el proveedor.
7. Confirmar si el problema es solo de este equipo o de toda el área/red.

**Solución aplicada:**
- El ping al gateway funcionó, pero el ping a 8.8.8.8 y la resolución de nombres fallaron, y se confirmó el mismo síntoma en otros equipos de la red.
- `tracert 8.8.8.8` avanzó hasta el router de borde y se detuvo en el primer salto del proveedor, ubicando la falla fuera de la red interna.
- Con eso quedó descartado el equipo del usuario, el switch y el DNS interno: el problema era de salida a Internet.
- Se escaló al proveedor de Internet (ISP), quien confirmó una interrupción de servicio en la zona.
- Se confirmó navegación normal una vez el ISP restableció el servicio.

---

[⬅ Volver al índice](../README.md)
