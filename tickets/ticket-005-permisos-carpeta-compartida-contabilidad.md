[⬅ Volver al índice](../README.md)

## TICKET-005
**Categoría:** Cuentas / Accesos (Active Directory — permisos)

**Título:** No puede acceder a la carpeta compartida del departamento de Contabilidad

**Descripción del usuario:**
> No puedo entrar a la carpeta de Contabilidad en el servidor, antes sí podía. Me sale un mensaje de que no tengo permiso o algo así. Necesito los archivos para hoy.

**Diagnóstico paso a paso:**
1. Confirmar la ruta exacta y el mensaje de error exacto.
2. Preguntar si recientemente cambió de puesto/departamento o si hubo reorganización de permisos.
3. Revisar en Active Directory a qué grupos de seguridad pertenece el usuario.
4. Revisar en el servidor de archivos qué grupos tienen permiso sobre esa carpeta (permisos NTFS y del recurso compartido — ambos deben coincidir).
5. Comparar: ¿el usuario pertenece al grupo correcto? ¿fue removido por error o nunca fue agregado?

**Solución aplicada:**
- Se confirmó que el usuario no pertenecía al grupo de seguridad "GG_Contabilidad_Lectura", que controla el acceso a esa carpeta.
- Se verificó con el supervisor del usuario que sí debía tener acceso antes de modificar permisos.
- Se agregó al usuario al grupo correspondiente en AD.
- Se ejecutó `gpupdate /force` en su equipo para actualizar el token de grupos sin esperar al próximo inicio de sesión.
- Se confirmó acceso exitoso a la carpeta.

---

[⬅ Volver al índice](../README.md)
