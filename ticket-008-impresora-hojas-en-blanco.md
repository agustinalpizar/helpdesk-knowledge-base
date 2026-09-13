[⬅ Volver al índice](../README.md)

## TICKET-008
**Categoría:** Impresoras

**Título:** La impresora de recepción imprime hojas en blanco

**Descripción del usuario:**
> La impresora está imprimiendo las hojas en blanco, no sale nada del documento aunque en la pantalla de la compu se ve que sí se está imprimiendo.

**Diagnóstico paso a paso:**
1. Confirmar si es láser o inyección de tinta (el diagnóstico cambia según el tipo de impresora).
2. Preguntar si pasa con todos los documentos o solo con uno (aísla si es de la impresora o del archivo).
3. Revisar niveles de tóner/tinta desde el panel de la impresora.
4. Si es láser, revisar si el cartucho está bien colocado o si tiene el sello protector de fábrica sin retirar (muy común en cartuchos recién instalados).
5. Imprimir una página de prueba directo desde el panel físico de la impresora — aísla si el problema es de la impresora o del driver/configuración en el equipo del usuario.
6. Si la página de prueba también sale en blanco: problema de hardware (tóner, tambor, cabezal). Si sale bien: revisar el driver del usuario.

**Solución aplicada:**
- La página de prueba desde el panel físico también salió en blanco → problema de hardware, no del equipo del usuario.
- Se revisó el cartucho y se encontró el sello protector de fábrica sin retirar (cartucho reemplazado recientemente sin completar bien la instalación).
- Se retiró el sello, se reinstaló el cartucho según indicaciones del fabricante.
- Se imprimió una nueva página de prueba con resultado correcto y se confirmó con el usuario.

---

[⬅ Volver al índice](../README.md)
