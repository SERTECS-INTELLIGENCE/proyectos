# SERTECS INTELLIGENCE: SOC Automation & Adversary Emulation 🛡️

**Autor:** Rolando Mux Noj | Analista de Ciberseguridad en SERTECS

Este repositorio contiene la documentación, análisis de incidentes y validación de reglas de un entorno de detección y respuesta (SIEM/SOAR) construido a medida. El proyecto demuestra la capacidad de detectar, alertar y mitigar tácticas de adversarios avanzados mediante la emulación de amenazas con MITRE CALDERA.

## 🏗️ Arquitectura del Laboratorio

El entorno de pruebas simula una infraestructura corporativa segmentada, compuesta por:

*   **SIEM / SOAR:** Servidor Ubuntu (Bare-metal) alojando Wazuh Manager.
*   **Middleware de Respuesta:** Scripts en Python (`custom-soc.py`) integrados con Wazuh para el procesamiento de alertas (log-tailing) y ejecución de respuestas activas (aislamiento por Firewall mediante listas CDB).
*   **Endpoint Víctima:** Windows 10 Professional (22H2) configurado con Sysmon y el agente de Wazuh, con políticas de Script Block Logging (Event ID 4104) habilitadas para visibilidad *Deep Blue*.
*   **Adversary Emulation:** Servidor de Magma & Caldera para la ejecución de cargas útiles en red local.

## 🎯 Objetivos del Proyecto

1.  **Validación de Reglas FIM:** Comprobar la eficacia del File Integrity Monitoring de Wazuh ante modificaciones masivas (simulación de ransomware).
2.  **Detección de Movimiento Lateral y Acceso a Credenciales:** Monitorear el volcado de memoria de procesos críticos (`svchost.exe`) y la alteración de registros (RDP).
3.  **Respuesta Activa:** Evaluar la automatización de bloqueos de IP y aislamiento de red ante eventos de nivel crítico (Nivel 12+).
4.  **Endurecimiento (Hardening):** Demostrar la necesidad de capturar comandos ofuscados de PowerShell habilitando registros avanzados del sistema.

## 🔬 Fases de Emulación (MITRE ATT&CK)

Durante los ejercicios de simulación, se ejecutaron y detectaron las siguientes técnicas:

*   **T1059.001 (PowerShell):** Ejecución de scripts maliciosos y evasión.
*   **T1112 (Modify Registry):** Habilitación silenciosa de conexiones RDP.
*   **T1105 (Ingress Tool Transfer):** Despliegue de agentes maliciosos (`splunkid.exe`, `metaIA.exe`).
*   **T1003 (OS Credential Dumping):** Extracción de credenciales en memoria vía `rundll32.exe` y `comsvcs.dll`.
*   **T1486 (Data Encrypted for Impact):** Simulación de secuestro de datos en el directorio crítico de la organización.

## 📄 Documentación Adjunta

*   [Reporte de Análisis de Informe de Incidentes (PDF)](./Mi_Analisis_de_informe_de_incidentes.pdf): Documento detallado con capturas de pantalla del Discover de Wazuh, análisis de logs, alertas por correo electrónico y tabla de IoCs (Indicadores de Compromiso).

## 🚀 Conclusiones

La implementación de reglas personalizadas (ej. Reglas 100003 y 100004) combinada con el análisis profundo de los eventos de Sysmon, reduce drásticamente el tiempo de respuesta ante incidentes. La transición de una visibilidad ciega a la captura del código desofuscado mediante el Event ID 4104 resalta la importancia de una configuración minuciosa de los agentes de monitoreo.
