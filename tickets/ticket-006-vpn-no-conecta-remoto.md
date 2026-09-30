[⬅ Volver al índice](../README.md)

## TICKET-006
**Categoría:** Red / VPN

**Título:** No puede conectarse a la VPN de la empresa desde su casa

**Descripción del usuario:**
> Buenas, necesito conectarme a la VPN para trabajar desde la casa hoy y no me deja. Me sale un error cuando trato de conectar, dice algo de que no se pudo establecer la conexión. Ya intenté varias veces.

**Diagnóstico paso a paso:**
1. Pedir el mensaje de error exacto o el código (los clientes VPN suelen dar un código específico, no un texto genérico).
2. Confirmar el estado de la cuenta antes de tocar el cliente: `net user <usuario> /domain` muestra *Password expires* y si la cuenta está bloqueada. Una contraseña vencida da errores de conexión que parecen de red.
3. Verificar que el cliente VPN esté en la versión soportada por la empresa.
4. Confirmar que el usuario tiene Internet funcional desde su red doméstica (probar acceder a cualquier página).
5. Revisar si el firewall/antivirus local está bloqueando el cliente VPN, y confirmar que el puerto del concentrador sea alcanzable desde la red del usuario con `Test-NetConnection vpn.empresa.com -Port 443`.
6. Del lado de IT: confirmar que el usuario tiene el grupo/permiso de acceso VPN asignado en el servidor.
7. Si varios usuarios reportan lo mismo a la vez, escalar a revisión del concentrador VPN.

**Solución aplicada:**
- `Test-NetConnection` al concentrador respondió correctamente, descartando bloqueo de red o firewall doméstico.
- `net user <usuario> /domain` mostró la fecha de *Password expires* ya pasada: la contraseña de dominio había expirado (política de 90 días) y el cliente VPN seguía intentando con la credencial vieja.
- Se guio al usuario para actualizar su contraseña vía portal de autoservicio y reingresarla en el cliente VPN.
- Se confirmó conexión exitosa tras el cambio.
- Se recomendó activar el aviso de expiración de contraseña con anticipación para evitar que se repita.

---

[⬅ Volver al índice](../README.md)
