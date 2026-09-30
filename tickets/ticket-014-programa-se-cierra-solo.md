[⬅ Volver al índice](../README.md)

## TICKET-014
**Categoría:** Software

**Título:** Un programa se cierra solo apenas se abre

**Descripción del usuario:**
> Cuando abro el sistema de facturación se abre un segundito y se cierra solo, no me deja ni empezar a trabajar. Ayer funcionaba bien.

**Diagnóstico paso a paso:**
1. Confirmar el nombre exacto del programa y su versión.
2. Preguntar si muestra algún mensaje antes de cerrarse o se cierra sin aviso.
3. Registrar el síntoma en el Visor de eventos: `Get-WinEvent -FilterHashtable @{LogName='Application'; ID=1000} -MaxEvents 5` (Application Error) devuelve el ejecutable que cayó y el código de excepción. Este evento solo documenta *que* el programa falló; no dice por qué.
4. Confirmar si hubo una actualización reciente de Windows, del propio programa, o instalación de otro software que pudiera generar conflicto.
5. Verificar si el problema ocurre con otro usuario en el mismo equipo, o con el mismo usuario en otro equipo — aísla si es del perfil, del equipo o del programa.
6. Descartar al antivirus con evidencia, no por descarte: en Windows Defender, `Get-WinEvent -LogName "Microsoft-Windows-Windows Defender/Operational" -FilterXPath "*[System[(EventID=1116 or EventID=1117)]]" -MaxEvents 10` muestra las detecciones (1116) y la acción tomada, como cuarentena o eliminación (1117), con la ruta del archivo afectado. El mismo historial se ve en Seguridad de Windows → Protección contra virus y amenazas → Historial de protección.

**Solución aplicada:**
- El evento 1000 confirmó el síntoma: el ejecutable del sistema de facturación caía al iniciar, y coincidía con el inicio del problema el día anterior.
- El log `Microsoft-Windows-Windows Defender/Operational` mostró la causa: un evento 1116 (detección) sobre una DLL de la carpeta del programa, seguido de un evento 1117 con acción *Quarantine*, ambos minutos antes del primer fallo. El archivo se había marcado como amenaza tras una actualización de firmas: falso positivo.
- Se restauró el archivo desde Historial de protección (Acciones → Restaurar) y, previa validación con el responsable de seguridad, se agregó la carpeta del programa a las exclusiones de Defender.
- Se ejecutó `sfc /scannow` para descartar daño adicional en archivos del sistema.
- Se confirmó apertura y funcionamiento normal.
- Se documentó el caso y se avisó al responsable de seguridad para revisar si la misma detección afecta a otros equipos con el programa instalado.

---

[⬅ Volver al índice](../README.md)
