[⬅ Volver al índice](../README.md)

## TICKET-007
**Categoría:** Software (Outlook / Correo)

**Título:** Outlook pide la contraseña constantemente y no sincroniza el correo

**Descripción del usuario:**
> Outlook me sigue pidiendo la contraseña una y otra vez, la pongo bien pero me la vuelve a pedir. No me están llegando correos nuevos desde hace rato.

**Diagnóstico paso a paso:**
1. Confirmar si pasa solo en Outlook de escritorio o también en Outlook Web/celular (aísla si es del cliente o de la cuenta).
2. Verificar si hubo un cambio de contraseña reciente — causa más común: Outlook sigue usando una credencial vieja guardada en Windows.
3. Revisar el estado de conexión en la barra inferior de Outlook (Desconectado, Intentando conectar, etc.).
4. Confirmar conectividad a Internet del equipo.
5. Listar las credenciales guardadas con `cmdkey /list` y buscar entradas de Office/Outlook (`MicrosoftOffice16_Data:...`); también se ven desde el Administrador de credenciales (`control keymgr.dll`).
6. Si nada de eso resuelve, considerar reparar o recrear el perfil de Outlook.

**Solución aplicada:**
- El acceso por Outlook Web funcionó con la contraseña actual, lo que confirmó que la cuenta estaba bien y el problema era del cliente de escritorio.
- `cmdkey /list` mostró una credencial de Office guardada con fecha anterior al último cambio de contraseña de dominio.
- Se eliminó esa entrada (`cmdkey /delete:<nombre>`) y se reinició Outlook, forzando el reingreso de la contraseña actual.
- Se confirmó sincronización normal de correo entrante y saliente sin más solicitudes.

---

[⬅ Volver al índice](../README.md)
