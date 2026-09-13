[⬅ Volver al índice](../README.md)

## TICKET-018
**Categoría:** Cuentas / Accesos (Active Directory)

**Título:** Usuario olvidó su contraseña y no puede iniciar sesión (autoservicio)

**Descripción del usuario:**
> Se me olvidó la contraseña de mi computadora, no logro acordarme de cuál es. No está bloqueada, simplemente no me acuerdo cuál puse.

**Diagnóstico paso a paso:**
1. Diferenciar de un bloqueo de cuenta: aquí el usuario simplemente no recuerda la contraseña, la cuenta no está bloqueada por intentos fallidos (evita confundir con TICKET-003).
2. Confirmar identidad del usuario según el proceso de verificación establecido antes de tocar la cuenta.
3. Preguntar si tiene configurado el restablecimiento de contraseña por autoservicio (SSPR) o si depende de que IT restablezca manualmente.
4. Si tiene autoservicio disponible, guiar al usuario paso a paso por el portal correspondiente usando otro dispositivo (celular) ya que no puede iniciar sesión en su equipo.
5. Si no tiene autoservicio configurado o falla, proceder con restablecimiento manual desde Active Directory.

**Solución aplicada:**
- Se confirmó que el usuario no tenía configurado el restablecimiento por autoservicio.
- Se verificó su identidad según el proceso establecido (cédula/datos de la organización) antes de continuar.
- Se restableció la contraseña desde Active Directory Users and Computers, marcando "El usuario debe cambiar la contraseña en el próximo inicio de sesión".
- Se le entregó la contraseña temporal de forma segura (no por correo/chat abierto) y se confirmó el cambio exitoso a una nueva contraseña personal.
- Se aprovechó para ofrecerle configurar el autoservicio de restablecimiento de contraseña para casos futuros, y se le explicó cómo hacerlo.

---

[⬅ Volver al índice](../README.md)
