[⬅ Volver al índice](../README.md)

## TICKET-003
**Categoría:** Cuentas / Accesos (Active Directory)

**Título:** Cuenta bloqueada por múltiples intentos fallidos de contraseña

**Descripción del usuario:**
> No puedo entrar a mi computadora, me sale un mensaje de que la cuenta está bloqueada. Yo no hice nada raro, solo intenté entrar como siempre.

**Diagnóstico paso a paso:**
1. Confirmar identidad del usuario antes de tocar la cuenta (verificación de seguridad estándar).
2. Preguntar si cambió la contraseña recientemente y si la tiene guardada en otro dispositivo (celular, correo sincronizado) que podría estar reintentando con la contraseña vieja.
3. Confirmar el estado real de la cuenta: `net user <usuario> /domain` muestra si está bloqueada y la fecha del último cambio de contraseña. Para ver todas las cuentas bloqueadas del dominio, `Search-ADAccount -LockedOut`.
4. Identificar el origen del bloqueo en el Visor de eventos del controlador de dominio con rol PDC Emulator, filtrando el registro de Seguridad por **Event ID 4740**: el campo *Caller Computer Name* indica desde qué equipo o dispositivo vienen los intentos.
5. Verificar dispositivos móviles o clientes de correo con la contraseña anterior guardada.

**Solución aplicada:**
- El evento 4740 mostró el nombre del equipo del usuario como origen de los intentos, coincidiendo con un cambio de contraseña del día anterior que no se había actualizado en el cliente de correo de su celular.
- Se desbloqueó la cuenta en AD (`Unlock-ADAccount <usuario>`, o Desbloquear cuenta desde ADUC).
- Se actualizó la contraseña en la configuración de correo del celular.
- Se explicó al usuario la política de bloqueo (intentos permitidos y tiempo de espera) para futuras referencias.

---

[⬅ Volver al índice](../README.md)
