[⬅ Volver al índice](../README.md)

## TICKET-003
**Categoría:** Cuentas / Accesos (Active Directory)

**Título:** Cuenta bloqueada por múltiples intentos fallidos de contraseña

**Descripción del usuario:**
> No puedo entrar a mi computadora, me sale un mensaje de que la cuenta está bloqueada. Yo no hice nada raro, solo intenté entrar como siempre.

**Diagnóstico paso a paso:**
1. Confirmar identidad del usuario antes de tocar la cuenta (verificación de seguridad estándar).
2. Preguntar si cambió la contraseña recientemente y si la tiene guardada en otro dispositivo (celular, correo sincronizado) que podría estar reintentando con la contraseña vieja.
3. Revisar en Active Directory Users and Computers el estado de la cuenta y el contador de intentos fallidos.
4. Revisar el Visor de eventos del controlador de dominio (Event ID 4740) para identificar el origen del bloqueo.
5. Verificar dispositivos móviles o clientes de correo con la contraseña anterior guardada.

**Solución aplicada:**
- El log mostró que los intentos fallidos venían del propio equipo del usuario, coincidiendo con un cambio de contraseña del día anterior que no se había actualizado en su celular.
- Se desbloqueó la cuenta en AD (Unlock account).
- Se actualizó la contraseña en la configuración de correo del celular.
- Se explicó al usuario la política de bloqueo (intentos permitidos y tiempo de espera) para futuras referencias.

---

[⬅ Volver al índice](../README.md)
