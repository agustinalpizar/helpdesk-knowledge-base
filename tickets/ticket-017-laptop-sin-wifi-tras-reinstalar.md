[⬅ Volver al índice](../README.md)

## TICKET-017
**Categoría:** Hardware / Red

**Título:** La laptop no detecta ninguna red WiFi después de reinstalar Windows

**Descripción del usuario:**
> Le reinstalé Windows a mi laptop porque estaba muy lenta y ahora no me aparece ninguna red WiFi para conectarme, ni siquiera la de mi casa la ve.

**Diagnóstico paso a paso:**
1. Confirmar que efectivamente no aparece ninguna red (ni la propia ni las de vecinos) — descarta que sea un problema de configuración de una red específica y apunta a que el adaptador no está funcionando.
2. Revisar si el sistema ve algún adaptador inalámbrico: `Get-NetAdapter` no lo listará si falta el driver. Complementar con `Get-PnpDevice -Status Error,Unknown` para ver los dispositivos sin controlador, o el Administrador de dispositivos (`devmgmt.msc`) buscando el signo de exclamación amarillo.
3. Si no aparece o aparece como "Dispositivo desconocido", es señal de que falta el driver — muy común después de una reinstalación limpia de Windows, ya que Windows no siempre trae el driver específico del chip WiFi del fabricante.
4. Obtener el identificador del hardware para buscar el driver exacto: en el Administrador de dispositivos, Propiedades → Detalles → Id. de hardware (`PCI\VEN_xxxx&DEV_xxxx`). El modelo del equipo solo (`wmic csproduct get name`) no siempre basta, porque un mismo modelo puede traer distintos chips WiFi.
5. Revisar si el modo avión está desactivado y si hay un interruptor físico o combinación de teclas para activar el WiFi en esa laptop en particular (algunos modelos lo desactivan por hardware).

**Solución aplicada:**
- `Get-NetAdapter` no listó ningún adaptador inalámbrico, y el Administrador de dispositivos mostraba un "Dispositivo desconocido" bajo Otros dispositivos: faltaba el driver.
- Se tomó el Id. de hardware del dispositivo para identificar el chip exacto, y con eso se descargó el driver correcto desde el sitio del fabricante usando otra computadora con Internet, transfiriéndolo por USB.
- Se instaló el driver y el equipo detectó las redes disponibles de inmediato.
- Se conectó a la red de la empresa y se confirmó acceso a Internet.

---

[⬅ Volver al índice](../README.md)
