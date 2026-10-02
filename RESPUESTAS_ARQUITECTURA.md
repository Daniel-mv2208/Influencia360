# Respuestas sobre Infraestructura de Publicación (Netlify)

A continuación, se describen las características de la plataforma elegida (**Netlify**) para alojar los reportes de Influencia360 (`dashboard_datos.html`, `dashboard_resultados.html` e `index.html`) y se responde a los interrogantes planteados.

## 1. Características Básicas de la Publicación
- **Hosting de Archivos Estáticos:** La plataforma sirve nativamente los archivos generados en RMarkdown (HTML, JS, CSS) a través de un servidor web.
- **Red de Entrega de Contenidos (CDN):** El sitio es copiado a servidores en múltiples regiones del mundo, mejorando los tiempos de respuesta.
- **SSL Automático:** Configuración automática de certificados seguros HTTPS usando Let's Encrypt.
- **Despliegue Continuo:** Se integra con el repositorio de GitHub para que cada commit a la rama principal actualice los reportes en internet automáticamente.

## 2. Soluciones a Necesidades Específicas

- **¿Tener una dirección de internet cualquiera para distribuir los reportes (es la solución por defecto?)**
  *Sí, es la solución por defecto.* Al realizar el primer despliegue, Netlify asigna instantáneamente un subdominio generado de manera aleatoria (por ejemplo: `https://famous-tarsier-90abc.netlify.app`), permitiendo la distribución del reporte inmediatamente sin configuraciones adicionales.

- **Tener una dirección de internet específica o de la empresa para distribuir los reportes.**
  Se puede configurar utilizando la funcionalidad de **Custom Domains**. En Netlify es posible vincular un dominio que se haya comprado previamente (como `mi-empresa.com`) o configurar un subdominio (`reportes.mi-empresa.com`). Esto se logra agregando registros de DNS (tipo A o CNAME) que apunten a los servidores de Netlify.

- **Tener mucho volumen de información para desplegar (¿es un problema o tema que involucra estos servicios?)**
  *Sí, es un tema relevante.* El plan gratuito tiene límites fijos de ancho de banda mensual (ej. 100 GB) y almacenamiento. Además, si hay miles de reportes muy pesados (que contengan los datasets completos dentro del HTML interactivo), el sitio consumirá los recursos gratuitos rápidamente. Para escalar a un volumen masivo, se requeriría pasar a un plan Pro de pago o externalizar los datos a una API o base de datos y conectar el reporte en tiempo real.

- **Publicar información para usuarios específicos o con credenciales (¿es un tema que se maneja con estos servicios?)**
  *Sí, se maneja perfectamente.* Usando herramientas como **Netlify Identity** y **Role-Based Access Control (RBAC)**, se pueden implementar muros de autenticación. De esta forma, si una persona intenta acceder a `https://tu-dominio.com/dashboard_resultados.html`, el servidor le exigirá un usuario y una contraseña válida. También es posible bloquear el sitio completo con una contraseña fija (Password Protection).

## 3. Características Avanzadas (Cuentas de Pago)

Con una cuenta de pago (planes Pro o Enterprise) en Netlify, se habilitan nuevas características profesionales. Dos de ellas son:

1. **Analíticas del lado del servidor (Netlify Analytics):**
   - *Qué es:* Métricas extraídas de los logs del servidor (visitas, páginas populares, ancho de banda usado) sin tener que inyectar scripts de seguimiento (como Google Analytics).
   - *Cómo se utilizaría:* Para medir qué partes del proyecto Influencia360 consultan más los directivos y asegurar la privacidad de los usuarios al no recolectar cookies.

2. **Inicio de Sesión Único Corporativo (SAML Single Sign-On):**
   - *Qué es:* Una función avanzada de Identity para conectar los reportes al directorio activo de una empresa (por ejemplo, Microsoft Entra ID u Okta).
   - *Cómo se utilizaría:* Para asegurar que los directivos de recursos humanos puedan acceder a los dashboards privados del proyecto simplemente ingresando con su correo de la compañía en lugar de tener que recordar contraseñas nuevas, automatizando también la gestión de roles.
