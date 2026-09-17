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
5. Revisar la fecha/hora del sistema — una desincronización puede causar fallos de autenticación Kerberos con mensajes similares.

**Solución aplicada:**
- Se confirmó que el equipo se había restaurado a un punto de restauración antiguo tras una falla de disco, dejando desactualizada la contraseña de la cuenta de máquina frente al controlador de dominio.
- Se inició sesión con la cuenta de administrador local del equipo.
- Se removió el equipo del dominio y se volvió a unir (Sistema → Cambiar nombre de equipo → salir del dominio → reiniciar → volver a unir con credenciales de administrador de dominio).
- Se reinició el equipo y se confirmó inicio de sesión exitoso con la cuenta de dominio original.
- Se verificó que el perfil y los archivos del usuario quedaron intactos.

---

[⬅ Volver al índice](../README.md)
