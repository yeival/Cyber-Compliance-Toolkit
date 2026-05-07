# Metodología y Matriz de Riesgos (Ejemplo Práctico)

Este documento describe la metodología aplicada para la identificación, análisis y tratamiento de riesgos de seguridad de la información, siguiendo el estándar **ISO/IEC 27005** y la metodología **MAGERIT**.

## 1. Identificación de Activos Críticos
Se han identificado los activos esenciales para la operación, clasificados por su valor en la triada de la información (C-I-D):

| Activo | Tipo | Descripción |
| :--- | :--- | :--- |
| **DB-PRD-01** | Datos | Base de Datos de clientes en PostgreSQL (Producción). |
| **Azure-VNet-01** | Infraestructura | Red virtual que soporta los servicios web de la compañía. |
| **Código Fuente** | Software | Repositorios de aplicaciones Node.js/React. |

## 2. Matriz de Análisis de Riesgos
Escala de valoración: 1 (Muy Bajo) a 5 (Crítico).

| Activo | Amenaza | Vulnerabilidad | Impacto (I) | Prob. (P) | Riesgo (I*P) |
| :--- | :--- | :--- | :---: | :---: | :---: |
| DB-PRD-01 | Acceso no autorizado | Falta de MFA en cuentas administrativas. | 5 | 3 | **15 (Alto)** |
| Azure-VNet-01 | Infiltración de red | Puertos de gestión (RDP/SSH) abiertos al público. | 4 | 4 | **16 (Alto)** |
| Código Fuente | Fuga de información | Credenciales expuestas en archivos de configuración. | 5 | 2 | **10 (Medio)** |

## 3. Plan de Tratamiento de Riesgos (RTP)
Basado en el **Anexo A de ISO 27001:2022**:

1. **Tratamiento para Acceso no autorizado (DB):**
   - **Control:** A.5.15 - Gestión de identidades.
   - **Acción:** Implementar Acceso Condicional y MFA mediante **Microsoft Entra ID**.
   - **Riesgo Residual:** Bajo.

2. **Tratamiento para Infiltración de red:**
   - **Control:** A.8.22 - Segmentación de redes.
   - **Acción:** Configurar **Azure Bastion** y cerrar puertos públicos en los Network Security Groups (NSG).
   - **Riesgo Residual:** Muy Bajo.

---
*Nota: Este es un modelo educativo para demostración de competencias en auditoría y gestión de seguridad.*
