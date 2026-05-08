# Checklist de Auditoría Interna: ISO/IEC 27001:2022

Este documento presenta una guía de verificación para la evaluación de controles de seguridad, enfocada en los nuevos controles tecnológicos y organizacionales de la actualización 2022 de la norma.

## 📋 Programa de Auditoría (Ejemplo)
**Alcance:** Infraestructura Cloud (Azure) y Ciclo de Vida de Desarrollo (Node.js/React).

### 1. Controles Tecnológicos (Tema 8)
| ID Control | Descripción | Punto de Verificación (Evidencia Sugerida) | Estado |
| :--- | :--- | :--- | :---: |
| **8.9** | Gestión de la configuración (Hardening) | ¿Existen documentos de configuración segura para Azure SQL y servidores Linux/Windows? | 🔲 |
| **8.15** | Registro de eventos (Logging) | ¿Se están centralizando los logs en un SIEM o Azure Log Analytics? | 🔲 |
| **8.23** | Filtrado web | ¿Se han implementado reglas de salida en los Firewalls/NSG para restringir el acceso a sitios maliciosos? | 🔲 |
| **8.28** | Codificación segura | ¿Se realizan escaneos de vulnerabilidades (SAST/DAST) en el código de Node.js antes del despliegue? | 🔲 |

### 2. Controles Organizacionales y Personas (Temas 5 y 6)
| ID Control | Descripción | Punto de Verificación (Evidencia Sugerida) | Estado |
| :--- | :--- | :--- | :---: |
| **5.7** | Inteligencia de amenazas | ¿La organización recibe boletines de seguridad o fuentes de inteligencia para prevenir ataques emergentes? | 🔲 |
| **5.15** | Gestión de identidades | ¿Está implementado el MFA y el principio de "Menor Privilegio" mediante Microsoft Entra ID? | 🔲 |
| **6.3** | Concienciación en seguridad | ¿Existen registros de capacitaciones en ciberseguridad para el personal técnico y administrativo? | 🔲 |

---

## 🛠️ Herramientas de Apoyo para la Auditoría
Para validar los puntos anteriores, se utilizan las siguientes herramientas:

1.  **Azure Advisor & Security Center:** Para evaluar el cumplimiento de la línea base de seguridad en la nube.
2.  **Snyk / SonarQube:** Para auditar la seguridad del código fuente (Control 8.28).
3.  **Nmap / Nessus:** Para validación técnica de puertos y servicios abiertos (Control 8.8).

## 📝 Notas del Auditor
> *"La auditoría no solo busca el cumplimiento, sino la mejora continua. En el caso de infraestructuras híbridas, es crítico verificar que las políticas de seguridad en local sean consistentes con las de la nube (Azure)."*

---
**Elaborado por:** Yeison Valdeblanquez  
**Certificación:** Auditor Interno ISO 27001:2022
