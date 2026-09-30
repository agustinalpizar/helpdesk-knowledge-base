[⬅ Volver al índice](../README.md)

## TICKET-009
**Categoría:** Cuentas / Accesos (Active Directory)

**Título:** Configurar acceso para empleado nuevo que inicia mañana

**Descripción del usuario** (en este caso, la solicitud viene de un supervisor/RRHH, no del usuario final):
> Hola, mañana empieza Andrea en el departamento de Ventas. Necesito que tenga su usuario, correo y acceso a la carpeta compartida de Ventas antes de que llegue.

**Diagnóstico paso a paso:**
1. Confirmar con el solicitante: nombre completo, departamento, puesto, recursos que necesita (carpetas, impresoras, sistemas) y supervisor directo.
2. Buscar una cuenta de referencia de otro usuario del mismo puesto y listar sus grupos con `Get-ADUser <referencia> -Properties MemberOf | Select -ExpandProperty MemberOf`, para copiar membresías sin omitir ninguna.
3. Revisar la convención de nombres de la organización y comprobar que el identificador propuesto esté libre: `Get-ADUser -Filter "SamAccountName -eq 'aperez'"` sin resultado confirma que no hay conflicto.
4. Confirmar la fecha de inicio exacta antes de crear la cuenta (evita crearla antes de tiempo o dejarla para el último momento).

**Solución aplicada:**
- Se creó la cuenta en Active Directory dentro de la OU de Ventas siguiendo la convención de nombres, usando la opción **Copiar** sobre la cuenta de referencia en ADUC, que replica automáticamente las membresías de grupo y la OU.
- Se verificó con `Get-ADUser andrea.solis -Properties MemberOf` que quedaran los tres grupos esperados: Ventas, impresora del área y carpeta compartida "Ventas".
- Se configuró la cuenta de correo con contraseña temporal y cambio obligatorio en el primer inicio de sesión.
- Se probó el inicio de sesión con las credenciales temporales y se confirmó acceso a la carpeta compartida antes de la fecha de inicio.
- Se documentó la cuenta y los accesos otorgados.

---

[⬅ Volver al índice](../README.md)
