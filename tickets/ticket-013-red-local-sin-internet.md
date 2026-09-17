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
5. Si el ping a IP pública funciona pero los sitios no cargan, sospechar de DNS y probar resolver un nombre de dominio.
6. Confirmar si el problema es solo de este equipo o de toda el área/red.

**Solución aplicada:**
- El ping al gateway funcionó, pero el ping a 8.8.8.8 y a nombres de dominio falló, y se confirmó el mismo síntoma en otros equipos de la red.
- Se determinó que el problema era de salida a Internet a nivel de router/firewall, no del equipo del usuario.
- Se escaló al proveedor de Internet (ISP), quien confirmó una interrupción de servicio en la zona.
- Se confirmó navegación normal una vez el ISP restableció el servicio.

---

[⬅ Volver al índice](../README.md)
