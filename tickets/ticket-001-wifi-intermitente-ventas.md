[⬅ Volver al índice](../README.md)

## TICKET-001
**Categoría:** Red / Conectividad

**Título:** WiFi se desconecta constantemente en el área de ventas

**Descripción del usuario:**
> Hola, buenas. Desde ayer el internet se me corta cada rato en la computadora, como cada 10-15 minutos se desconecta el WiFi y tengo que volver a conectarme. A veces ni aparece la red. Ya reinicié la compu pero sigue igual. Necesito esto resuelto porque tengo una reunión por Teams en la tarde.

**Diagnóstico paso a paso:**
1. Preguntar si el problema ocurre solo en ese equipo o también en otros de la misma área (aísla si es del dispositivo o de la infraestructura).
2. Preguntar desde cuándo empezó y si coincide con algún cambio (actualización de Windows, cambio de ubicación del equipo, etc.).
3. Revisar señal y banda con `netsh wlan show interfaces` (campos *Signal*, *Radio type* y *Channel*): una señal por debajo de ~60% ya explica cortes.
4. Generar el informe de historial inalámbrico con `netsh wlan show wlanreport` (ejecutado como administrador): produce un HTML con las sesiones de los últimos 3 días y el motivo de cada desconexión.
5. Revisar el adaptador en Administrador de dispositivos (`devmgmt.msc`) → Propiedades → Administración de energía, y la versión del driver en la pestaña Controlador.
6. Revisar interferencia: distancia al AP, otros dispositivos en la zona, y canales solapados con `netsh wlan show networks mode=bssid`.
7. Si hay acceso, revisar logs del AP/switch (desconexiones, cambios de canal).
8. Si el problema es generalizado en el área, escalar a revisión de infraestructura WiFi.

**Solución aplicada:**
- El informe de `netsh wlan show wlanreport` mostró desconexiones periódicas sin pérdida de señal, lo que descartó interferencia o cobertura y apuntó al adaptador.
- Se identificó que el adaptador WiFi tenía activada la opción "Permitir que el equipo apague este dispositivo para ahorrar energía" (Propiedades del adaptador → Administración de energía), causa típica de desconexiones intermitentes.
- Se desactivó esa opción y se actualizó el driver del adaptador a la versión más reciente del fabricante.
- Se confirmó conexión estable por 30+ minutos sin cortes.
- Se documentó el caso por si se repite en otros equipos del mismo modelo/área.

---

[⬅ Volver al índice](../README.md)
