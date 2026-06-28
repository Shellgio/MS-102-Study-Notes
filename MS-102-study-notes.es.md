# Apuntes de estudio MS-102

> [!IMPORTANT]
> Estos son apuntes personales de repaso para el examen Microsoft MS-102. No son una guía completa del examen y no cubren todos los objetivos. Comprueba siempre Microsoft Learn y el temario oficial del examen para confirmar los requisitos actuales.

## Implementar y administrar un inquilino de Microsoft 365

### Administración del inquilino

> [!NOTE]
> **Visibilidad del estado del servicio:** los usuarios con el rol Administrador global o Administrador de soporte técnico de servicios pueden ver el estado del servicio en el Centro de administración de Microsoft 365.

> [!NOTE]
> **Estado del servicio vs. Centro de mensajes:** usa Estado del servicio para comprobar si un servicio está caído por errores, interrupciones o incidencias regionales. Usa el Centro de mensajes para revisar actualizaciones planificadas.

> [!NOTE]
> **Multi-Geo / residencia de datos:** para una implementación de Microsoft 365 en varias regiones, un único inquilino con residencia de datos configurada por país o región suele ser lo más fácil de administrar.

### Uso compartido y colaboración externa

> [!NOTE]
> **Impedir el uso compartido externo en SharePoint y OneDrive:** la configuración de uso compartido a nivel de organización se cambia desde **Configuración de la organización > Servicios** en el Centro de administración de Microsoft 365. La configuración más granular, incluidos dominios y grupos de seguridad, se administra desde **Directivas > Uso compartido** en el Centro de administración de SharePoint.

> [!NOTE]
> **Configuración de invitación de invitados:** si en Microsoft Entra la colaboración externa permite invitar solo a usuarios con roles administrativos concretos, solo Administradores globales, Administradores de usuarios e Invitadores de invitados pueden invitar usuarios externos.

> [!NOTE]
> **Declaración de privacidad y contacto global de privacidad:** estos campos se configuran desde la hoja de propiedades del Centro de administración de Microsoft Entra. Si no se rellenan, los invitados externos verán un mensaje indicando que la organización no proporcionó términos para revisar.

### Grupos y usuarios

> [!NOTE]
> **Grupos de Microsoft 365 públicos:** los grupos creados desde el Centro de administración de Microsoft Entra son privados de forma predeterminada y no se pueden marcar como públicos durante la creación. Los grupos creados desde el Centro de administración de Microsoft 365 pueden ser privados o públicos, y el valor se puede cambiar más adelante.

> [!NOTE]
> **Usuarios eliminados:** las cuentas de usuario eliminadas permanecen en estado suspendido durante 30 días y pueden restaurarse durante ese periodo.

> [!NOTE]
> **Grupos eliminados:** los grupos de Microsoft 365 y los grupos de seguridad de Microsoft Entra eliminados se conservan durante 30 días y pueden restaurarse. Esto no aplica a grupos de distribución y el periodo de 30 días no es personalizable.

> [!NOTE]
> **Importación de usuarios:** al importar usuarios en el Centro de administración de Microsoft 365, los únicos valores obligatorios son Username, que será el nombre principal de usuario, y Display Name.

> [!NOTE]
> **Pertenencia dinámica:** solo los grupos de Microsoft 365 y los grupos de seguridad admiten pertenencia dinámica.

> [!NOTE]
> **Informe de usuarios y licencias:** `Get-MgUser` puede usarse para generar un informe de usuarios activos y sus licencias. `Get-MgUserLicenseDetail` se usa por usuario.

### Roles y permisos

> [!NOTE]
> **Configuración de MFA:** el rol Administrador de autenticación con privilegios puede administrar la configuración de MFA de los usuarios.

> [!IMPORTANT]
> **Administración de Microsoft Secure Score:** Administradores globales, Administradores de seguridad, Administradores de Exchange y Administradores de SharePoint pueden administrar Microsoft Secure Score y sus acciones recomendadas. El rol Administrador de usuarios tiene acceso de solo lectura.

> [!NOTE]
> **Comparar permisos de roles:** el Centro de administración de Microsoft 365 permite comparar permisos de hasta tres roles a la vez, lo que ayuda a aplicar privilegio mínimo.

> [!NOTE]
> **Evaluaciones de Compliance Manager:** Compliance Data Administrator, Global Administrator y Compliance Administrator pueden ver evaluaciones de Microsoft Purview Compliance Manager. Compliance Data Administrator es la opción de menor privilegio entre esos roles. Organization Management puede ver plantillas de evaluación, pero no evaluaciones.

> [!NOTE]
> **Roles con acceso al portal de cumplimiento de Purview:** incluyen Global Administrator, Compliance Data Administrator, Compliance Administrator, Security Administrator y roles de Information Protection en versión preliminar, como Admins, Analysts, Investigators y Readers.

> [!NOTE]
> **Password Administrator vs. Helpdesk Administrator:** Helpdesk Administrator puede administrar contraseñas de usuarios y administradores. Password Administrator puede restablecer contraseñas de usuarios, pero no de administradores.

### Valores de seguridad predeterminados

> [!IMPORTANT]
> **Valores predeterminados de seguridad:** habilitarlos en Microsoft Entra contribuye a recomendaciones de Secure Score como requerir MFA para administradores, permitir que los usuarios completen MFA y bloquear autenticación heredada.

## Implementar y administrar identidad y acceso con Microsoft Entra

### Identidad híbrida y sincronización

> [!NOTE]
> **Puertos de Microsoft Entra Cloud Sync:** se requieren los puertos 80 y 443. El puerto 80 descarga listas de revocación de certificados durante la validación TLS/SSL y el puerto 443 gestiona la comunicación saliente con Microsoft Entra ID.

> [!NOTE]
> **Ámbito de Cloud Sync:** configura el ámbito de Microsoft Entra Cloud Sync desde el Centro de administración de Microsoft Entra, en administración híbrida y sincronización en la nube. Puedes seleccionar qué unidades organizativas se sincronizan.

> [!IMPORTANT]
> **Ciclo manual de Microsoft Entra Connect Sync:** usa `Start-ADSyncSyncCycle -PolicyType Delta` para sincronizar solo cambios en vez de ejecutar una sincronización completa.

> [!NOTE]
> **Sincronizar objetos concretos:** selecciona los dominios necesarios y las unidades organizativas de cada dominio.

> [!NOTE]
> **Información de Microsoft Entra Connect Health:** Extranet lockout trends, failed sign-in report e informes compatibles con privacidad están disponibles en Microsoft Entra Connect Health. Inicios de sesión de riesgo, usuarios eliminados e informes de MFA fallido son características de Microsoft Entra ID.

> [!NOTE]
> **Atributos únicos:** `mail`, `signInName` y `userPrincipalName` deben ser únicos para que la sincronización con Microsoft Entra funcione. Un error común es `AttributeValueMustBeUnique`.

> [!NOTE]
> **Análisis de errores de sincronización:** los errores pueden analizarse desde el servidor de Microsoft Entra Connect y desde Microsoft Entra Connect Health.

> [!NOTE]
> **Autenticación de paso a través y federada:** ambas permiten usar un dominio local de Active Directory para autenticar en Microsoft 365.

> [!NOTE]
> **Protección de contraseñas en controladores de dominio:** el servicio DC Agent inicia la descarga de nuevas directivas de protección de contraseñas desde Microsoft Entra.

> [!NOTE]
> **Umbral de eliminación accidental:** el valor predeterminado de Microsoft Entra Cloud Sync es 500. Puede reducirse para ajustarlo al tamaño y riesgo del entorno.

### Unidades administrativas

> [!NOTE]
> Si un administrador tiene los roles Groups Administrator y User Administrator con ámbito en una unidad administrativa, pero solo se agrega un grupo de seguridad a esa unidad, el administrador puede administrar la pertenencia del grupo. Para administrar usuarios directamente, los usuarios deben agregarse directamente a la unidad administrativa.

### Autenticación y acceso seguro

> [!NOTE]
> **Coincidencia de números en Authenticator:** configura directivas de Microsoft Authenticator para requerir coincidencia de números en notificaciones push.

> [!NOTE]
> **Piloto de notificaciones de aplicación para MFA:** configura Microsoft Authenticator en modo Push y requiere que los usuarios vuelvan a registrarse en MFA para forzar el método.

> [!TIP]
> **RDP sin contraseña con Windows Hello for Business:** Certificate Trust es la solución que admite RDP sin contraseña.

> [!NOTE]
> **Cookie persistente del navegador:** el valor máximo es 365 días.

### Licencias e Identity Protection

> [!NOTE]
> **Requisitos de Microsoft Entra ID Protection:** Microsoft 365 E3 y EMS E3 no incluyen Microsoft Entra ID P2. Microsoft 365 E5 y EMS E5 incluyen las capacidades necesarias para detección de riesgo y corrección automática. También puede usarse un complemento de Microsoft Entra P2 con niveles inferiores como Microsoft 365 E3 o Business Premium.

> [!IMPORTANT]
> **Preguntas de seguridad:** los administradores no pueden usar preguntas de seguridad para restablecer su contraseña.

> [!IMPORTANT]
> **Detección de credenciales filtradas:** Microsoft Entra ID Protection requiere hashes de contraseña en Microsoft Entra ID, por lo que debe implementarse sincronización de hash de contraseñas.

> [!NOTE]
> **Informes de inicios de sesión de riesgo:** Global Reader, Security Administrator y Security Reader pueden acceder a los informes de inicios de sesión de riesgo de Microsoft Entra ID Protection.

> [!NOTE]
> **Directiva de riesgo de usuario:** requerir cambio de contraseña es el único requisito de permitir acceso dentro de una directiva de riesgo de usuario.

## Administrar seguridad y amenazas con Microsoft Defender XDR

### Microsoft Defender for Endpoint

> [!NOTE]
> **Dispositivos compatibles para incorporación:** Defender for Endpoint admite versiones compatibles de Windows, Windows Server 2012 y posteriores, Azure Virtual Desktop, Windows 365, macOS, Linux, Android e iOS.

> [!NOTE]
> **iOS sin inscripción:** Defender for Endpoint en iOS admite MAM, Intune MDM + MAM y MAM sin inscripción. MAM sin inscripción administra aplicaciones mediante directivas de protección de aplicaciones en dispositivos no inscritos en Intune MDM.

> [!IMPORTANT]
> **Activar RBAC:** solo Administradores globales y Administradores de seguridad pueden habilitar RBAC en Defender for Endpoint. Al activar RBAC, los usuarios con roles de solo lectura en Microsoft Entra, como Security Reader, pierden acceso hasta que se les asigna un rol RBAC de Defender for Endpoint.

> [!NOTE]
> **Incorporar clientes con Intune:** primero activa la conexión de Microsoft Intune en la configuración de Microsoft Defender XDR. Después habilita Microsoft Defender for Endpoint en Intune. Por último, crea un perfil de configuración usando la plantilla de Defender for Endpoint para dispositivos Windows.

> [!NOTE]
> **Exposure score de Vulnerability Management:** refleja el riesgo real de compromiso de un dispositivo considerando superficie de ataque, configuraciones incorrectas, contexto de red, riesgo de vulnerabilidades, configuración y explotabilidad.

### Informes, alertas y Secure Score

> [!NOTE]
> **Agregación de alertas:** cuando varios eventos coinciden con una directiva de alerta en poco tiempo, la agregación los añade a una alerta existente. En Microsoft 365 E5, el intervalo de agregación es de un minuto.

> [!NOTE]
> **Estados de acción recomendada que aumentan Secure Score:** Completed, Resolved through third party y Resolved through alternate mitigation.

> [!NOTE]
> **Propiedades de una alerta generada:** el estado y el comentario pueden modificarse después de generarse la alerta. La gravedad y la categoría se definen en la directiva de alerta y no se pueden modificar en la alerta generada.

> [!NOTE]
> **Rol View-Only Manage Alerts:** este rol de Microsoft Purview permite ver solo alertas con categoría Others.

> [!NOTE]
> **Notificaciones por correo de directivas de alerta:** el límite diario más alto es No limit. Otros valores disponibles son 1, 5, 10, 25, 50, 100, 150 y 200.

### Microsoft Defender for Office 365

> [!NOTE]
> **Attack simulation training:** al crear una simulación de credential harvest, Email es el tipo de payload disponible.

> [!NOTE]
> **Buzón de SecOps:** se usa cuando los mensajes de un usuario deben quedar sin filtrar y sin protección de Microsoft Defender for Office 365 para que el equipo de seguridad pueda recopilar y analizar mensajes.

> [!NOTE]
> **Asignar un buzón de SecOps:** se configura en el portal de Microsoft Defender, en Email & collaboration, directivas contra amenazas y Advanced delivery.

> [!NOTE]
> **Retención personalizada de cuarentena:** las directivas antispam y antiphishing tienen 15 días de cuarentena por defecto y se pueden personalizar. Las cuarentenas de antimalware y Safe Attachments usan 30 días y no son personalizables.

> [!NOTE]
> **Entidades restringidas:** las cuentas que superan límites de correo saliente pueden agregarse a Restricted entities. Para permitir que envíen de nuevo, desbloquea la cuenta en Microsoft Defender, en Email & collaboration > Review > Restricted entities. Pueden desbloquear usuarios los Administradores globales, Administradores de seguridad o miembros de Exchange Organization Management.

> [!NOTE]
> **Tenant Allow/Block List:** Microsoft Defender for Office 365 Plan 1 admite 1.000 entradas allow y 1.000 block. Plan 2 admite 5.000 allow y 10.000 block. Organization Management es el grupo de roles de menor privilegio para agregar y quitar entradas.

> [!NOTE]
> **Informe detallado de URL threat protection:** las exportaciones detalladas admiten un intervalo máximo de un día. Los informes resumen pueden cubrir periodos más largos.

### Microsoft Defender for Cloud Apps

> [!NOTE]
> **Conector de aplicaciones de Microsoft 365:** agregar el conector de Microsoft 365 a Defender for Cloud Apps requiere permisos de Administrador global durante la autorización inicial.

> [!NOTE]
> **Una directiva de sesión no bloquea descargas:** si las descargas siguen ocurriendo y los intentos bloqueados no se registran, agrega los dominios que faltan para que todo el tráfico pase por el proxy inverso de Defender for Cloud Apps.

> [!IMPORTANT]
> **Tipos de directivas de MDCA:** las directivas de actividad filtran actividades de usuario y umbrales en el tiempo. Las directivas de detección de anomalías identifican comportamientos anómalos. Las directivas de detección de aplicaciones evalúan tráfico descubierto desde logs. Las directivas de sesión aplican controles en tiempo real durante sesiones con proxy.

## Administrar cumplimiento con Microsoft Purview

### Retención

> [!NOTE]
> **Número mínimo de directivas de retención para Teams:** los mensajes de canales de Teams y los mensajes de canales privados de Teams requieren directivas de retención separadas. Otras ubicaciones como correo de Exchange, sitios de SharePoint, cuentas de OneDrive y carpetas públicas de Exchange pueden configurarse en una misma directiva. En ese escenario se necesitan al menos tres directivas.

> [!NOTE]
> **Precedencia de retención:** una directiva de retención publicada y aplicada manualmente al contenido tiene prioridad sobre las directivas aplicadas a una ubicación.

> [!NOTE]
> **Retención en chats de Teams:** los chats de Teams solo pueden recibir configuración de retención mediante una directiva de retención. Las directivas de etiquetas de retención pueden aplicar retención a Exchange Online, SharePoint Online, OneDrive y grupos de Microsoft 365.

> [!NOTE]
> **Directiva MRM para buzones de Exchange Online:** habilita el archivo de buzón, crea una etiqueta de retención MRM en Microsoft Purview, crea una directiva de retención MRM y aplícala a los buzones desde el Centro de administración de Exchange.

### DLP

> [!NOTE]
> **Prioridad de Policy Tips en DLP:** las reglas DLP se ejecutan por prioridad, donde gana el número de prioridad más bajo. Solo se muestra la sugerencia de directiva de la primera regla coincidente.

> [!NOTE]
> **Dispositivos compatibles con Endpoint DLP:** Microsoft Purview Endpoint DLP admite Windows 10 o posterior y macOS.

> [!NOTE]
> **Informes DLP:** DLP Policy Matches muestra archivos que coinciden con directivas DLP, pero no da detalle a nivel de regla. DLP Incidents muestra coincidencias en el tiempo a nivel de regla.

> [!TIP]
> **Programar informe DLP Policy Matches:** puede programarse semanal o mensualmente.

> [!WARNING]
> **Ubicaciones DLP:** una directiva DLP puede aplicarse a todas las ubicaciones excepto Microsoft 365 Copilot. Para Microsoft 365 Copilot se requiere una directiva separada.

> [!NOTE]
> **Falsos positivos:** los usuarios solo pueden reportar falsos positivos de elementos identificados por DLP cuando la directiva DLP está en estado On.

> [!NOTE]
> **Archivos en chats uno a uno de Teams:** los archivos subidos a chats uno a uno o grupales se almacenan en OneDrive del remitente y se comparten con los participantes. Los archivos de canal se almacenan en la carpeta de SharePoint del equipo.

### Sensitivity labels y configuración de sitios

> [!NOTE]
> **Privacidad predeterminada de SharePoint:** la configuración de privacidad predeterminada de un sitio de SharePoint Online puede configurarse en una etiqueta de sensibilidad.

