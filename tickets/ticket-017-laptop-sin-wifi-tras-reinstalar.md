[⬅ Volver al índice](../README.md)

## TICKET-017
**Categoría:** Hardware / Red

**Título:** La laptop no detecta ninguna red WiFi después de reinstalar Windows

**Descripción del usuario:**
> Le reinstalé Windows a mi laptop porque estaba muy lenta y ahora no me aparece ninguna red WiFi para conectarme, ni siquiera la de mi casa la ve.

**Diagnóstico paso a paso:**
1. Confirmar que efectivamente no aparece ninguna red (ni la propia ni las de vecinos) — descarta que sea un problema de configuración de una red específica y apunta a que el adaptador no está funcionando.
2. Revisar en el Administrador de dispositivos si el adaptador de red inalámbrica aparece listado, y si tiene algún ícono de advertencia (signo de exclamación amarillo).
3. Si no aparece o aparece como "Dispositivo desconocido", es señal de que falta el driver — muy común después de una reinstalación limpia de Windows, ya que Windows no siempre trae el driver específico del chip WiFi del fabricante.
4. Confirmar la marca/modelo exacto del equipo para buscar el driver correcto del fabricante.
5. Revisar si el modo avión está desactivado y si hay un interruptor físico o combinación de teclas para activar el WiFi en esa laptop en particular (algunos modelos lo desactivan por hardware).

**Solución aplicada:**
- En el Administrador de dispositivos, el adaptador de red inalámbrica aparecía como "Dispositivo desconocido" bajo Otros dispositivos, confirmando que faltaba el driver.
- Se descargó el driver de red inalámbrica correcto desde el sitio del fabricante (usando el modelo exacto del equipo) usando otra computadora con Internet, y se transfirió por USB.
- Se instaló el driver y el equipo detectó las redes disponibles de inmediato.
- Se conectó a la red de la empresa y se confirmó acceso a Internet.

---

[⬅ Volver al índice](../README.md)
