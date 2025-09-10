# Informe de Auditoría de Sistemas - Examen de la Unidad I

**Nombres y apellidos:** Jorge Luis Briceño Diaz
**Fecha:** 10/09/2025
**URL GitHub:** https://github.com/J0rgZ/ExamenAuditoria.git

---

## 1. Proyecto de Auditoría de Riesgos

### Login

**Evidencia:**

![Captura del Login Ficticio]


**Descripción:**
La funcionalidad de inicio de sesión ficticio se ha implementado en [menciona el archivo o la sección del código] utilizando credenciales predefinidas (`usuario: admin`, `contraseña: password123`). Al ingresar estas credenciales, el sistema simula un acceso exitoso, redirigiendo al usuario a la interfaz principal de la aplicación de auditoría. No se utiliza una base de datos para la autenticación; la validación se realiza directamente en el código. Esto permite demostrar la capacidad de integración de una capa de autenticación básica, según lo solicitado.

---

### Motor de Inteligencia Artificial

**Evidencia:**

![Captura del Código Fuente del Motor de IA Mejorado]


**Descripción:**
El motor de inteligencia artificial ha sido mejorado en el archivo `[nombre_del_archivo.py o .js, etc.]` en la función `[nombre_de_la_funcion_IA]`. Las mejoras se centraron en refinar los prompts para la generación de perfiles de riesgo más detallados y análisis de impacto más precisos, utilizando un modelo de lenguaje avanzado ejecutado localmente. Se han incorporado directrices específicas en los prompts para asegurar que las recomendaciones de mitigación estén alineadas con los controles de la norma ISO 27001, haciendo referencia a categorías como el control de acceso, seguridad de operaciones, gestión de incidentes, etc. Esto permite que el sistema ofrezca sugerencias más relevantes y estructuradas para la gestión de la seguridad de la información.

---

## 2. Hallazgos

Aquí se presentan los hallazgos de la auditoría para 5 activos de información seleccionados, utilizando el motor de IA mejorado para el análisis de riesgos y recomendaciones.

### Activo 1: Servidor de Base de Datos

**Evidencia:**

![Captura del Análisis del Servidor de Base de Datos]


**Condición:**
Se ha identificado que el servidor de base de datos principal almacena información sensible de clientes (números de cuenta, saldos) y no cuenta con cifrado de datos en reposo activado por defecto. Además, las políticas de contraseñas para los usuarios de la base de datos no exigen una complejidad mínima adecuada ni rotación periódica.

**Recomendación:**
Implementar el cifrado de datos en reposo (por ejemplo, TDE - Transparent Data Encryption) para proteger la información sensible almacenada. Fortalecer las políticas de contraseñas para los usuarios de la base de datos, exigiendo una longitud mínima de 12 caracteres, uso de mayúsculas, minúsculas, números y símbolos, y establecer una rotación obligatoria cada 90 días, alineado con el control A.9.2.1 de ISO 27001 (Política de control de acceso).

**Riesgo:** Alta

---

### Activo 2: API Transacciones

**Evidencia:**

![Captura del Análisis de API Transacciones]


**Condición:**
La API de transacciones, expuesta para servicios de banca móvil, no implementa un mecanismo robusto de limitación de tasa de solicitudes (rate limiting) y las claves API utilizadas son estáticas y no se rotan regularmente. Existe el riesgo de ataques de fuerza bruta o denegación de servicio distribuido (DDoS) a través de esta API.

**Recomendación:**
Implementar un sistema de rate limiting y throttling en el gateway de la API para prevenir ataques de fuerza bruta y DDoS. Establecer un proceso de rotación periódica de las claves API (cada 90 días) y asegurar que se utilice OAuth 2.0 con tokens de corta duración para la autenticación y autorización, conforme al control A.13.1.2 de ISO 27001 (Protección de los servicios de red).

**Riesgo:** Media

---

### Activo 3: Aplicación Web de Banca

**Evidencia:**

![Captura del Análisis de la Aplicación Web de Banca]


**Condición:**
La aplicación web de banca presenta formularios de entrada de datos que no validan adecuadamente la entrada del usuario, lo que podría permitir ataques de inyección SQL o Cross-Site Scripting (XSS). Además, la gestión de sesiones no invalida tokens de sesión después de un período de inactividad prolongado.

**Recomendación:**
Implementar validaciones robustas en el lado del servidor para todas las entradas de usuario y utilizar sentencias preparadas o ORM para interactuar con la base de datos, mitigando inyecciones SQL. Establecer un tiempo de inactividad para las sesiones de usuario (por ejemplo, 15 minutos) después del cual la sesión debe invalidarse automáticamente, alineado con el control A.14.1.2 de ISO 27001 (Desarrollo de software y sistema seguro).

**Riesgo:** Alta

---

### Activo 4: Firewall Perimetral

**Evidencia:**

![Captura del Análisis del Firewall Perimetral]


**Condición:**
Se observó que las reglas del firewall perimetral no se revisan ni actualizan periódicamente, y algunas reglas permiten el tráfico de puertos y protocolos innecesarios para la operación bancaria. No hay un registro centralizado y monitoreo constante de los eventos del firewall.

**Recomendación:**
Establecer un proceso formal para la revisión trimestral de las reglas del firewall, eliminando cualquier regla obsoleta o innecesaria. Implementar un sistema de gestión de logs centralizado (SIEM) para recopilar y monitorear los registros del firewall en tiempo real, permitiendo la detección temprana de actividades sospechosas, según el control A.12.4.1 de ISO 27001 (Registro de eventos).

**Riesgo:** Media

---

### Activo 5: Autenticación MFA

**Evidencia:**

![Captura del Análisis de Autenticación MFA]


**Condición:**
Aunque el banco utiliza autenticación multifactor (MFA) para el acceso a sistemas críticos, se ha detectado que en algunas configuraciones la MFA puede ser omitida bajo ciertas condiciones (por ejemplo, desde IPs de confianza no verificadas adecuadamente) o el segundo factor es vulnerable a ataques de phishing (SMS basado en OTP sin validación de canal).

**Recomendación:**
Revisar y fortalecer las políticas de MFA para asegurar que sea obligatoria en todas las condiciones de acceso remoto y para sistemas críticos, independientemente de la dirección IP de origen. Evaluar la implementación de factores de autenticación más robustos, como FIDO2 o aplicaciones de autenticación con push notifications, para mitigar riesgos de phishing y otros ataques de ingeniería social, conforme al control A.9.2.4 de ISO 27001 (Autenticación de información de usuario).

**Riesgo:** Media
