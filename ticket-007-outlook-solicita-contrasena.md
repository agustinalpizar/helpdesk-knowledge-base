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
5. Revisar el Administrador de credenciales de Windows (Panel de Control → Cuentas de usuario) buscando una entrada guardada para Office/Outlook.
6. Si nada de eso resuelve, considerar reparar o recrear el perfil de Outlook.

**Solución aplicada:**
- Se encontró una credencial vieja guardada en el Administrador de credenciales de Windows, anterior al cambio de contraseña de dominio.
- Se eliminó esa entrada y se reinició Outlook, forzando el reingreso de la contraseña actual.
- Se confirmó sincronización normal de correo entrante y saliente sin más solicitudes.

---

[⬅ Volver al índice](../README.md)
