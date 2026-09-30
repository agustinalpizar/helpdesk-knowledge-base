[⬅ Volver al índice](../README.md)

## TICKET-005
**Categoría:** Cuentas / Accesos (Active Directory — permisos)

**Título:** No puede acceder a la carpeta compartida del departamento de Contabilidad

**Descripción del usuario:**
> No puedo entrar a la carpeta de Contabilidad en el servidor, antes sí podía. Me sale un mensaje de que no tengo permiso o algo así. Necesito los archivos para hoy.

**Diagnóstico paso a paso:**
1. Confirmar la ruta exacta y el mensaje de error exacto.
2. Preguntar si recientemente cambió de puesto/departamento o si hubo reorganización de permisos.
3. Revisar a qué grupos pertenece el usuario: `whoami /groups` desde su propio equipo muestra el token actual de la sesión, que es lo que realmente se evalúa al abrir la carpeta.
4. Contrastarlo con la pertenencia en el directorio: `net user <usuario> /domain` o `Get-ADUser <usuario> -Properties MemberOf`. Si difieren, el token de la sesión está desactualizado.
5. Revisar en el servidor de archivos qué grupos tienen permiso sobre esa carpeta: `icacls "D:\Compartidas\Contabilidad"` para los permisos NTFS, y las propiedades del recurso compartido para los permisos de share — el acceso efectivo es el más restrictivo de ambos.
6. Comparar: ¿el usuario pertenece al grupo correcto? ¿fue removido por error o nunca fue agregado?

**Solución aplicada:**
- `icacls` mostró que el acceso a la carpeta lo concede el grupo "GG_Contabilidad_Lectura", y `whoami /groups` confirmó que el usuario no lo tenía.
- Se verificó con el supervisor del usuario que sí debía tener acceso antes de modificar permisos.
- Se agregó al usuario al grupo correspondiente en AD.
- Se cerró y reabrió la sesión del usuario: la pertenencia a grupos se resuelve al generar el token de inicio de sesión, así que `gpupdate /force` por sí solo no la actualiza. Se verificó con `whoami /groups` que el grupo ya apareciera.
- Se confirmó acceso exitoso a la carpeta.

---

[⬅ Volver al índice](../README.md)
