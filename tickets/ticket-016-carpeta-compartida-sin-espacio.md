[⬅ Volver al índice](../README.md)

## TICKET-016
**Categoría:** Red / Almacenamiento compartido

**Título:** No puede guardar archivos en la carpeta compartida — "no hay suficiente espacio"

**Descripción del usuario:**
> Estoy tratando de guardar un archivo en la carpeta compartida del proyecto y me sale un error que dice que no hay espacio suficiente en el disco. Pero en mi computadora sí tengo espacio.

**Diagnóstico paso a paso:**
1. Confirmar el mensaje de error exacto y la ruta de red exacta donde intenta guardar.
2. Aclarar que el espacio relevante es el del servidor que aloja la carpeta compartida, no el disco local del usuario — error común de confusión.
3. Verificar con otro usuario si también presenta el mismo error en esa misma carpeta (aísla si es del servidor o de permisos puntuales del usuario).
4. Si se tiene acceso al servidor, revisar el espacio del volumen que aloja el recurso: `Get-Volume` muestra tamaño y espacio libre de cada uno.
5. Revisar si hay cuotas configuradas, que producen el mismo mensaje aunque el volumen tenga espacio: `Get-FsrmQuota` si el servidor usa el Administrador de recursos del servidor de archivos (FSRM), o `fsutil quota query <unidad>` para cuotas por usuario.
6. Revisar el tamaño del archivo que intenta guardar vs. límites configurados (tamaño máximo de archivo, si aplica).

**Solución aplicada:**
- Otro usuario reprodujo el mismo error en la misma carpeta, lo que descartó un problema de permisos puntuales.
- `Get-Volume` en el servidor mostró el volumen que aloja el recurso al 98% de uso, afectando a todos los usuarios de esa carpeta y no solo a este.
- Se identificaron carpetas de respaldo antiguas y archivos duplicados que ocupaban espacio innecesario, y se coordinó con el responsable del área su limpieza/archivo en almacenamiento secundario.
- Se liberó espacio suficiente para restaurar la operación normal.
- Se recomendó configurar una alerta de espacio en disco (ej. al 85%) para anticipar el problema en el futuro.

---

[⬅ Volver al índice](../README.md)
