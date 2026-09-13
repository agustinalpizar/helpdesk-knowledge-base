[⬅ Volver al índice](../README.md)

## TICKET-011
**Categoría:** Red

**Título:** Internet lento solo en el área de Contabilidad (segundo piso)

**Descripción del usuario:**
> Todos en el área de Contabilidad nos quejamos de que el internet está bien lento desde esta mañana, las páginas cargan lentísimo y los correos tardan en enviarse. En otras áreas dicen que está normal.

**Diagnóstico paso a paso:**
1. Confirmar que el problema es exclusivo de esa área comparando con otro piso/área (aísla si es local o general).
2. Preguntar desde cuándo empezó y si coincide con algo puntual (equipo nuevo conectado, backup programado, etc.).
3. Revisar el switch que da servicio a esa área: uso de ancho de banda por puerto, errores o un puerto saturado.
4. Si aplica, revisar el punto de acceso WiFi de la zona (clientes conectados, canal, interferencia).
5. Buscar algún dispositivo con consumo anormal de ancho de banda (descarga grande, streaming, sincronización masiva).
6. Verificar la utilización del enlace hacia el switch de core/router, para descartar cuello de botella en el uplink.

**Solución aplicada:**
- Al revisar el switch del piso se encontró un puerto con tráfico anormalmente alto: un equipo estaba haciendo una sincronización masiva de OneDrive tras una reinstalación reciente, saturando el uplink compartido del área.
- Se contactó al usuario de ese equipo y se pausó temporalmente la sincronización.
- Se recomendó programar sincronizaciones grandes fuera de horario pico.
- Se confirmó con los usuarios del área que la velocidad volvió a la normalidad.

---

[⬅ Volver al índice](../README.md)
