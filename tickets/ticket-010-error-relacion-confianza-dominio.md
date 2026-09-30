[⬅ Volver al índice](../README.md)

## TICKET-010
**Categoría:** Red / Active Directory

**Título:** El equipo no permite iniciar sesión — error de "relación de confianza"

**Descripción del usuario:**
> Prendí la compu hoy y no me deja entrar con mi usuario normal, sale un mensaje en inglés que habla de que falló la relación de confianza entre esta estación y el dominio, o algo así. Nunca había visto ese error.

**Diagnóstico paso a paso:**
1. Confirmar el mensaje exacto para descartar que sea otro error de red o de credenciales.
2. Preguntar si el equipo estuvo apagado mucho tiempo, se restauró desde una imagen/snapshot antigua, o se reinstaló el sistema recientemente — causas típicas de este error.
3. Confirmar conectividad de red al controlador de dominio (ping al nombre del dominio o al DC).
4. Intentar iniciar sesión con una cuenta de administrador local, para descartar que el problema sea solo del perfil de dominio.
5. Revisar la fecha/hora del sistema — un desfase mayor a 5 minutos respecto al controlador de dominio rompe la autenticación Kerberos con mensajes similares. Comparar con `w32tm /query /status` y resincronizar con `w32tm /resync` si aplica.
6. Confirmar el diagnóstico antes de actuar: `Test-ComputerSecureChannel` devuelve `False` cuando la contraseña de la cuenta de máquina está desincronizada frente al dominio, que es exactamente este error.

**Solución aplicada:**
- Se confirmó que el equipo se había restaurado a un punto de restauración antiguo tras una falla de disco, dejando desactualizada la contraseña de la cuenta de máquina frente al controlador de dominio.
- Se inició sesión con la cuenta de administrador local del equipo y `Test-ComputerSecureChannel` devolvió `False`, confirmando el diagnóstico.
- Se reparó el canal seguro sin sacar el equipo del dominio:
  ```powershell
  Test-ComputerSecureChannel -Repair -Credential (Get-Credential DOMINIO\administrador)
  ```
  Esto restablece la contraseña de la cuenta de máquina contra el controlador de dominio y evita el ciclo de salir y volver a unir, que además destruye el perfil local si se hace mal.
- Se volvió a ejecutar `Test-ComputerSecureChannel` (ahora `True`), se reinició y se confirmó inicio de sesión con la cuenta de dominio original.
- Se verificó que el perfil y los archivos del usuario quedaron intactos, sin necesidad de recrearlos.
- Nota: si la reparación falla (por ejemplo, si la cuenta de máquina fue eliminada del directorio), el procedimiento de respaldo sigue siendo remover el equipo del dominio y volver a unirlo.

---

[⬅ Volver al índice](../README.md)
