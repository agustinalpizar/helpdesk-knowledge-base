[⬅ Volver al índice](../README.md)

## TICKET-001
**Categoría:** Red / Conectividad

**Título:** WiFi se desconecta constantemente en el área de ventas

**Descripción del usuario:**
> Hola, buenas. Desde ayer el internet se me corta cada rato en la computadora, como cada 10-15 minutos se desconecta el WiFi y tengo que volver a conectarme. A veces ni aparece la red. Ya reinicié la compu pero sigue igual. Necesito esto resuelto porque tengo una reunión por Teams en la tarde.

**Diagnóstico paso a paso:**
1. Preguntar si el problema ocurre solo en ese equipo o también en otros de la misma área (aísla si es del dispositivo o de la infraestructura).
2. Preguntar desde cuándo empezó y si coincide con algún cambio (actualización de Windows, cambio de ubicación del equipo, etc.).
3. Revisar intensidad de señal WiFi y banda usada (2.4GHz vs 5GHz).
4. Revisar el adaptador de red en Administrador de dispositivos: drivers desactualizados y configuración de ahorro de energía (causa muy común de desconexiones intermitentes).
5. Revisar interferencia: distancia al AP, otros dispositivos en la zona.
6. Si hay acceso, revisar logs del AP/switch (desconexiones, cambios de canal).
7. Si el problema es generalizado en el área, escalar a revisión de infraestructura WiFi.

**Solución aplicada:**
- Se identificó que el adaptador WiFi tenía activada la opción "Permitir que el equipo apague este dispositivo para ahorrar energía" (Propiedades del adaptador → Administración de energía), causa típica de desconexiones intermitentes.
- Se desactivó esa opción y se actualizó el driver del adaptador a la versión más reciente del fabricante.
- Se confirmó conexión estable por 30+ minutos sin cortes.
- Se documentó el caso por si se repite en otros equipos del mismo modelo/área.

---

[⬅ Volver al índice](../README.md)
