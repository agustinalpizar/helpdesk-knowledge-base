# Base de Conocimiento — Tickets Simulados de Soporte Técnico (Help Desk N1)

18 tickets simulados, con diagnóstico paso a paso y solución aplicada, cubriendo problemas comunes de un puesto de Help Desk N1: red/conectividad, impresoras, VPN, cuentas y accesos en Active Directory, correo, hardware y almacenamiento compartido.

**Categorías cubiertas:** Red, Impresoras, Cuentas/Accesos (Active Directory), Hardware, Software.

---

## Índice

1. [TICKET-001 — WiFi se desconecta constantemente en el área de ventas](#ticket-001)
2. [TICKET-002 — No puede imprimir en la impresora de red del segundo piso](#ticket-002)
3. [TICKET-003 — Cuenta bloqueada por múltiples intentos fallidos de contraseña](#ticket-003)
4. [TICKET-004 — Computadora muy lenta para abrir programas](#ticket-004)
5. [TICKET-005 — No puede acceder a la carpeta compartida del departamento de Contabilidad](#ticket-005)
6. [TICKET-006 — No puede conectarse a la VPN de la empresa desde su casa](#ticket-006)
7. [TICKET-007 — Outlook pide la contraseña constantemente y no sincroniza el correo](#ticket-007)
8. [TICKET-008 — La impresora de recepción imprime hojas en blanco](#ticket-008)
9. [TICKET-009 — Configurar acceso para empleado nuevo que inicia mañana](#ticket-009)
10. [TICKET-010 — El equipo no permite iniciar sesión — error de "relación de confianza"](#ticket-010)
11. [TICKET-011 — Internet lento solo en el área de Contabilidad (segundo piso)](#ticket-011)
12. [TICKET-012 — La computadora se reinicia sola o muestra pantalla azul](#ticket-012)
13. [TICKET-013 — El equipo tiene acceso a la red local pero no a Internet](#ticket-013)
14. [TICKET-014 — Un programa se cierra solo apenas se abre](#ticket-014)
15. [TICKET-015 — La impresora de red no aparece en la lista al configurarla en un equipo nuevo](#ticket-015)
16. [TICKET-016 — No puede guardar archivos en la carpeta compartida — "no hay suficiente espacio"](#ticket-016)
17. [TICKET-017 — La laptop no detecta ninguna red WiFi después de reinstalar Windows](#ticket-017)
18. [TICKET-018 — Usuario olvidó su contraseña y no puede iniciar sesión (autoservicio)](#ticket-018)

---

<a id="ticket-001"></a>
## TICKET-001
**Categoría:** Red / Conectividad

**Título:** WiFi se desconecta constantemente en el área de ventas

**Descripción del usuario:**
> Hola, buenas. Desde ayer el internet se me corta cada rato en la computadora, como cada 10-15 minutos se desconecta el WiFi y tengo que volver a conectarme. A veces ni aparece la red. Ya reinicié la compu pero sigue igual. Necesito esto resuelto porque tengo una reunión por Teams en la tarde.

**Diagnóstico paso a paso:**
1. Preguntar si el problema ocurre solo en ese equipo o también en otros de la misma área (aísla si es del dispositivo o de la infraestructura).
2. Preguntar desde cuándo empezó y si coincide con algún cambio (actualización de Windows, cambio de ubicación del equipo, etc.).
3. Revisar intensidad de señal WiFi y banda usada (2.4GHz vs 5GHz).
4. Revisar el adaptador de red en Administrador de dispositivos: drivers desactualizados y configuración de ahorro de energía (causa muy común de desconexiones intermitentes).
5. Revisar interferencia: distancia al AP, otros dispositivos en la zona.
6. Si hay acceso, revisar logs del AP/switch (desconexiones, cambios de canal).
7. Si el problema es generalizado en el área, escalar a revisión de infraestructura WiFi.

**Solución aplicada:**
- Se identificó que el adaptador WiFi tenía activada la opción "Permitir que el equipo apague este dispositivo para ahorrar energía" (Propiedades del adaptador → Administración de energía), causa típica de desconexiones intermitentes.
- Se desactivó esa opción y se actualizó el driver del adaptador a la versión más reciente del fabricante.
- Se confirmó conexión estable por 30+ minutos sin cortes.
- Se documentó el caso por si se repite en otros equipos del mismo modelo/área.

---

<a id="ticket-002"></a>
## TICKET-002
**Categoría:** Impresoras

**Título:** No puede imprimir en la impresora de red del segundo piso

**Descripción del usuario:**
> Buenas, necesito imprimir unos documentos urgentes y la impresora del pasillo no me deja, sale un error que dice algo de que no se puede conectar. Ayer sí funcionaba bien.

**Diagnóstico paso a paso:**
1. Pedir el mensaje de error exacto (o captura de pantalla).
2. Preguntar si otros usuarios de la misma impresora tienen el mismo problema o es solo este equipo.
3. Hacer ping a la IP configurada de la impresora desde el equipo del usuario.
4. Verificar si la IP de la impresora cambió (muy común cuando la impresora usa DHCP en vez de IP fija).
5. Revisar la cola de impresión local por trabajos atascados.
6. Verificar que el puerto de impresora configurado coincida con la IP actual del dispositivo.
7. Si el ping falla desde varios equipos, revisar el estado físico/de red de la impresora directamente.

**Solución aplicada:**
- El ping a la IP del driver no respondió: la impresora había tomado una IP distinta por DHCP tras un reinicio.
- Se confirmó la IP actual desde el panel de la impresora.
- Se actualizó la IP en las propiedades del puerto en el equipo del usuario.
- Se recomendó configurar una reserva DHCP para esa impresora y evitar que vuelva a pasar.
- Se confirmó impresión de página de prueba exitosa.

---

<a id="ticket-003"></a>
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

<a id="ticket-004"></a>
## TICKET-004
**Categoría:** Hardware / Software

**Título:** Computadora muy lenta para abrir programas

**Descripción del usuario:**
> Mi compu está bien lenta, se tarda un montón en abrir Excel o Chrome, a veces se queda pensando y no responde. Ya la reinicié pero sigue igual.

**Diagnóstico paso a paso:**
1. Preguntar desde cuándo empezó y si coincide con alguna instalación, actualización o falta de espacio en disco.
2. Revisar Administrador de Tareas: uso de CPU, RAM y disco en reposo, para identificar procesos que consumen recursos.
3. Revisar espacio libre en disco (disco casi lleno es una causa muy común de lentitud, sobre todo en SSD).
4. Revisar programas de inicio (demasiados cargando al arrancar Windows).
5. Verificar actualizaciones de Windows corriendo en segundo plano.
6. Revisar si hay un análisis de antivirus en curso.
7. Si la lentitud es severa y persistente, revisar el estado SMART del disco.

**Solución aplicada:**
- Se encontró el disco al 95% de capacidad, causando lentitud generalizada.
- Se liberó espacio eliminando temporales, caché de navegador y descargas antiguas (con confirmación del usuario antes de borrar nada).
- Se deshabilitaron 4 programas innecesarios del inicio (Administrador de tareas → Inicio).
- Se verificó que el uso de CPU volvió a niveles normales y los programas abrieron con tiempos de respuesta normales.
- Se recomendó al usuario mantener al menos 15-20% de espacio libre en disco.

---

<a id="ticket-005"></a>
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

<a id="ticket-006"></a>
## TICKET-006
**Categoría:** Red / VPN

**Título:** No puede conectarse a la VPN de la empresa desde su casa

**Descripción del usuario:**
> Buenas, necesito conectarme a la VPN para trabajar desde la casa hoy y no me deja. Me sale un error cuando trato de conectar, dice algo de que no se pudo establecer la conexión. Ya intenté varias veces.

**Diagnóstico paso a paso:**
1. Pedir el mensaje de error exacto o el código (los clientes VPN suelen dar un código específico, no un texto genérico).
2. Confirmar que está usando las credenciales de dominio correctas y que la cuenta no está bloqueada o con la contraseña vencida.
3. Verificar que el cliente VPN esté en la versión soportada por la empresa.
4. Confirmar que el usuario tiene Internet funcional desde su red doméstica (probar acceder a cualquier página).
5. Revisar si el firewall/antivirus local está bloqueando el cliente VPN.
6. Del lado de IT: confirmar que el usuario tiene el grupo/permiso de acceso VPN asignado en el servidor.
7. Si varios usuarios reportan lo mismo a la vez, escalar a revisión del concentrador VPN.

**Solución aplicada:**
- Se confirmó que la contraseña de dominio había expirado (política de 90 días) y el cliente VPN seguía intentando con la credencial vieja.
- Se guio al usuario para actualizar su contraseña vía portal de autoservicio y reingresarla en el cliente VPN.
- Se confirmó conexión exitosa tras el cambio.
- Se recomendó activar el aviso de expiración de contraseña con anticipación para evitar que se repita.

---

<a id="ticket-007"></a>
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

<a id="ticket-008"></a>
## TICKET-008
**Categoría:** Impresoras

**Título:** La impresora de recepción imprime hojas en blanco

**Descripción del usuario:**
> La impresora está imprimiendo las hojas en blanco, no sale nada del documento aunque en la pantalla de la compu se ve que sí se está imprimiendo.

**Diagnóstico paso a paso:**
1. Confirmar si es láser o inyección de tinta (el diagnóstico cambia según el tipo de impresora).
2. Preguntar si pasa con todos los documentos o solo con uno (aísla si es de la impresora o del archivo).
3. Revisar niveles de tóner/tinta desde el panel de la impresora.
4. Si es láser, revisar si el cartucho está bien colocado o si tiene el sello protector de fábrica sin retirar (muy común en cartuchos recién instalados).
5. Imprimir una página de prueba directo desde el panel físico de la impresora — aísla si el problema es de la impresora o del driver/configuración en el equipo del usuario.
6. Si la página de prueba también sale en blanco: problema de hardware (tóner, tambor, cabezal). Si sale bien: revisar el driver del usuario.

**Solución aplicada:**
- La página de prueba desde el panel físico también salió en blanco → problema de hardware, no del equipo del usuario.
- Se revisó el cartucho y se encontró el sello protector de fábrica sin retirar (cartucho reemplazado recientemente sin completar bien la instalación).
- Se retiró el sello, se reinstaló el cartucho según indicaciones del fabricante.
- Se imprimió una nueva página de prueba con resultado correcto y se confirmó con el usuario.

---

<a id="ticket-009"></a>
## TICKET-009
**Categoría:** Cuentas / Accesos (Active Directory)

**Título:** Configurar acceso para empleado nuevo que inicia mañana

**Descripción del usuario** (en este caso, la solicitud viene de un supervisor/RRHH, no del usuario final):
> Hola, mañana empieza Andrea en el departamento de Ventas. Necesito que tenga su usuario, correo y acceso a la carpeta compartida de Ventas antes de que llegue.

**Diagnóstico paso a paso:**
1. Confirmar con el solicitante: nombre completo, departamento, puesto, recursos que necesita (carpetas, impresoras, sistemas) y supervisor directo.
2. Buscar una cuenta de referencia de otro usuario del mismo puesto para copiar membresías de grupo — reduce errores y mantiene consistencia.
3. Revisar la convención de nombres de usuario/correo de la organización para evitar conflictos con cuentas existentes.
4. Confirmar la fecha de inicio exacta antes de crear la cuenta (evita crearla antes de tiempo o dejarla para el último momento).

**Solución aplicada:**
- Se creó la cuenta en Active Directory dentro de la OU de Ventas, siguiendo la convención de nombres establecida.
- Se copiaron las membresías de grupo de un usuario existente del mismo puesto (grupo de Ventas, impresora del área, carpeta compartida "Ventas").
- Se configuró la cuenta de correo con contraseña temporal y cambio obligatorio en el primer inicio de sesión.
- Se probó el inicio de sesión con las credenciales temporales y se confirmó acceso a la carpeta compartida antes de la fecha de inicio.
- Se documentó la cuenta y los accesos otorgados.

---

<a id="ticket-010"></a>
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

<a id="ticket-011"></a>
## TICKET-011
**Categoría:** Red

**Título:** Internet lento solo en el área de Contabilidad (segundo piso)

**Descripción del usuario:**
> Todos en el área de Contabilidad nos quejamos de que el internet está bien lento desde esta mañana, las páginas cargan lentísimo y los correos tardan en enviarse. En otras áreas dicen que está normal.

**Diagnóstico paso a paso:**
1. Confirmar que el problema es exclusivo de esa área comparando con otro piso/área (aísla si es local o general).
2. Preguntar desde cuándo empezó y si coincide con algo puntual (equipo nuevo conectado, backup programado, etc.).
3. Revisar el switch que da servicio a esa área: uso de ancho de banda por puerto, errores o un puerto saturado.
4. Si aplica, revisar el punto de acceso WiFi de la zona (clientes conectados, canal, interferencia).
5. Buscar algún dispositivo con consumo anormal de ancho de banda (descarga grande, streaming, sincronización masiva).
6. Verificar la utilización del enlace hacia el switch de core/router, para descartar cuello de botella en el uplink.

**Solución aplicada:**
- Al revisar el switch del piso se encontró un puerto con tráfico anormalmente alto: un equipo estaba haciendo una sincronización masiva de OneDrive tras una reinstalación reciente, saturando el uplink compartido del área.
- Se contactó al usuario de ese equipo y se pausó temporalmente la sincronización.
- Se recomendó programar sincronizaciones grandes fuera de horario pico.
- Se confirmó con los usuarios del área que la velocidad volvió a la normalidad.

---

<a id="ticket-012"></a>
## TICKET-012
**Categoría:** Hardware

**Título:** La computadora se reinicia sola o muestra pantalla azul

**Descripción del usuario:**
> Mi compu se ha estado reiniciando sola, a veces sale una pantalla azul con letras y números y se reinicia. Pasa como 2-3 veces al día, en cualquier momento.

**Diagnóstico paso a paso:**
1. Preguntar si el reinicio ocurre haciendo alguna tarea específica o es completamente aleatorio.
2. Pedir el código de error de la pantalla azul si lo alcanzó a ver o tomar foto (ej. "MEMORY_MANAGEMENT", "IRQL_NOT_LESS_OR_EQUAL") — orienta la causa.
3. Revisar el Visor de eventos de Windows (Registro del sistema) buscando eventos de BugCheck alrededor de la hora del reinicio.
4. Revisar temperatura del equipo — sobrecalentamiento es causa común, sobre todo en laptops con ventiladores sucios.
5. Verificar si hubo una actualización de drivers o de Windows reciente coincidiendo con el inicio del problema.
6. Ejecutar Windows Memory Diagnostic si se sospecha de un módulo de RAM defectuoso.

**Solución aplicada:**
- El Visor de eventos mostró errores de BugCheck consistentes con fallas de memoria (MEMORY_MANAGEMENT).
- Se ejecutó el diagnóstico de memoria de Windows y se confirmó un error en uno de los módulos RAM.
- Se reemplazó el módulo defectuoso.
- Se monitoreó el equipo por 2 días sin nuevos reinicios ni pantallas azules, confirmando la resolución.

---

<a id="ticket-013"></a>
## TICKET-013
**Categoría:** Red

**Título:** El equipo tiene acceso a la red local pero no a Internet

**Descripción del usuario:**
> Puedo ver la carpeta compartida y la impresora de la oficina, pero no me carga ninguna página de internet ni me llegan correos.

**Diagnóstico paso a paso:**
1. Confirmar el síntoma exacto: ¿el navegador dice "sin conexión" o carga infinitamente? ¿el ícono de red muestra advertencia de "sin Internet"?
2. Revisar la configuración IP del equipo (`ipconfig /all`): dirección IP, máscara, gateway y DNS asignados.
3. Hacer ping a la puerta de enlace (gateway) — si responde, el problema está más allá del gateway; si no, el problema es local.
4. Si el gateway responde, hacer ping a una IP pública conocida (ej. 8.8.8.8) para descartar problema de ruta vs. DNS.
5. Si el ping a IP pública funciona pero los sitios no cargan, sospechar de DNS y probar resolver un nombre de dominio.
6. Confirmar si el problema es solo de este equipo o de toda el área/red.

**Solución aplicada:**
- El ping al gateway funcionó, pero el ping a 8.8.8.8 y a nombres de dominio falló, y se confirmó el mismo síntoma en otros equipos de la red.
- Se determinó que el problema era de salida a Internet a nivel de router/firewall, no del equipo del usuario.
- Se escaló al proveedor de Internet (ISP), quien confirmó una interrupción de servicio en la zona.
- Se confirmó navegación normal una vez el ISP restableció el servicio.

---

<a id="ticket-014"></a>
## TICKET-014
**Categoría:** Software

**Título:** Un programa se cierra solo apenas se abre

**Descripción del usuario:**
> Cuando abro el sistema de facturación se abre un segundito y se cierra solo, no me deja ni empezar a trabajar. Ayer funcionaba bien.

**Diagnóstico paso a paso:**
1. Confirmar el nombre exacto del programa y su versión.
2. Preguntar si muestra algún mensaje antes de cerrarse o se cierra sin aviso.
3. Revisar el Visor de eventos (Registro de aplicación) buscando errores del proceso a la hora del cierre.
4. Confirmar si hubo una actualización reciente de Windows, del propio programa, o instalación de otro software que pudiera generar conflicto.
5. Verificar si el problema ocurre con otro usuario en el mismo equipo, o con el mismo usuario en otro equipo — aísla si es del perfil, del equipo o del programa.
6. Revisar si el antivirus puso en cuarentena algún archivo del programa.

**Solución aplicada:**
- El Visor de eventos mostró un error de falta de un archivo DLL del programa, coincidiendo con una actualización reciente de Windows que había dañado esa dependencia.
- Se reinstaló el programa por completo (desinstalación y reinstalación desde el instalador oficial) para restaurar los archivos faltantes.
- Se confirmó apertura y funcionamiento normal.
- Se documentó el caso para revisar si se repite en otros equipos tras la misma actualización.

---

<a id="ticket-015"></a>
## TICKET-015
**Categoría:** Impresoras

**Título:** La impresora de red no aparece en la lista al configurarla en un equipo nuevo

**Descripción del usuario:**
> Me dieron una compu nueva y estoy tratando de agregar la impresora de la oficina pero no aparece en la lista cuando busco impresoras de red.

**Diagnóstico paso a paso:**
1. Confirmar el método usado para buscarla (descubrimiento automático de Windows, o intento de agregarla por nombre/IP directo).
2. Verificar que el equipo nuevo esté en la misma red/VLAN que la impresora — en subredes distintas, el descubrimiento automático normalmente no funciona.
3. Hacer ping a la IP de la impresora desde el equipo nuevo para confirmar conectividad básica.
4. Verificar si el descubrimiento de red está activado (perfil de red configurado como privada vs. pública en Windows).
5. Si el ping funciona pero no aparece en la búsqueda automática, agregarla manualmente por IP.

**Solución aplicada:**
- El ping fue exitoso, pero el perfil de red del equipo estaba como "Pública" en vez de "Privada", lo cual desactiva el descubrimiento de red por defecto en Windows.
- Se cambió el perfil a "Privada".
- Se optó, de todas formas, por agregar la impresora manualmente por IP (Agregar impresora → "La impresora que quiero no está en la lista" → Agregar por dirección TCP/IP) para mayor confiabilidad.
- Se confirmó impresión de página de prueba exitosa.

---

<a id="ticket-016"></a>
## TICKET-016
**Categoría:** Red / Almacenamiento compartido

**Título:** No puede guardar archivos en la carpeta compartida — "no hay suficiente espacio"

**Descripción del usuario:**
> Estoy tratando de guardar un archivo en la carpeta compartida del proyecto y me sale un error que dice que no hay espacio suficiente en el disco. Pero en mi computadora sí tengo espacio.

**Diagnóstico paso a paso:**
1. Confirmar el mensaje de error exacto y la ruta de red exacta donde intenta guardar.
2. Aclarar que el espacio relevante es el del servidor que aloja la carpeta compartida, no el disco local del usuario — error común de confusión.
3. Verificar con otro usuario si también presenta el mismo error en esa misma carpeta (aísla si es del servidor o de permisos puntuales del usuario).
4. Si se tiene acceso, revisar el espacio disponible en el volumen del servidor donde vive el recurso compartido.
5. Revisar si hay cuotas de disco (quotas) configuradas por carpeta o por usuario en el servidor de archivos.
6. Revisar el tamaño del archivo que intenta guardar vs. límites configurados (tamaño máximo de archivo, si aplica).

**Solución aplicada:**
- Se confirmó que el volumen del servidor estaba casi lleno (98% de uso), afectando a todos los usuarios de esa carpeta compartida, no solo a este.
- Se identificaron carpetas de respaldo antiguas y archivos duplicados que ocupaban espacio innecesario, y se coordinó con el responsable del área su limpieza/archivo en almacenamiento secundario.
- Se liberó espacio suficiente para restaurar la operación normal.
- Se recomendó configurar una alerta de espacio en disco (ej. al 85%) para anticipar el problema en el futuro.

---

<a id="ticket-017"></a>
## TICKET-017
**Categoría:** Hardware / Red

**Título:** La laptop no detecta ninguna red WiFi después de reinstalar Windows

**Descripción del usuario:**
> Le reinstalé Windows a mi laptop porque estaba muy lenta y ahora no me aparece ninguna red WiFi para conectarme, ni siquiera la de mi casa la ve.

**Diagnóstico paso a paso:**
1. Confirmar que efectivamente no aparece ninguna red (ni la propia ni las de vecinos) — descarta que sea un problema de configuración de una red específica y apunta a que el adaptador no está funcionando.
2. Revisar en el Administrador de dispositivos si el adaptador de red inalámbrica aparece listado, y si tiene algún ícono de advertencia (signo de exclamación amarillo).
3. Si no aparece o aparece como "Dispositivo desconocido", es señal de que falta el driver — muy común después de una reinstalación limpia de Windows, ya que Windows no siempre trae el driver específico del chip WiFi del fabricante.
4. Confirmar la marca/modelo exacto del equipo para buscar el driver correcto del fabricante.
5. Revisar si el modo avión está desactivado y si hay un interruptor físico o combinación de teclas para activar el WiFi en esa laptop en particular (algunos modelos lo desactivan por hardware).

**Solución aplicada:**
- En el Administrador de dispositivos, el adaptador de red inalámbrica aparecía como "Dispositivo desconocido" bajo Otros dispositivos, confirmando que faltaba el driver.
- Se descargó el driver de red inalámbrica correcto desde el sitio del fabricante (usando el modelo exacto del equipo) usando otra computadora con Internet, y se transfirió por USB.
- Se instaló el driver y el equipo detectó las redes disponibles de inmediato.
- Se conectó a la red de la empresa y se confirmó acceso a Internet.

---

<a id="ticket-018"></a>
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
