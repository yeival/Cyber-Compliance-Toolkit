# Estrategia de Recuperación ante Desastres (DRP)

Este documento define el marco de trabajo para restaurar los servicios tecnológicos críticos tras una interrupción mayor, alineado con el dominio de **Continuidad del Negocio (ISO 27001 Control A.5.29 y A.5.30)**.

## 1. Métricas Críticas de Recuperación
Para cada servicio, se deben definir las siguientes metas:

*   **RTO (Recovery Time Objective):** Tiempo máximo permitido para que el servicio esté fuera de línea. (Ej: 4 horas para el Core Bancario).
*   **RPO (Recovery Point Objective):** Cantidad máxima de datos que la organización puede permitirse perder (tiempo desde el último backup). (Ej: 1 hora de transacciones).

## 2. Estrategia de Respaldo (Backup 3-2-1)
Implementamos la regla de oro del respaldo:
1.  **3 copias de los datos:** (Producción + 2 respaldos).
2.  **2 medios diferentes:** (Disco local + Almacenamiento en la Nube).
3.  **1 copia fuera del sitio (Off-site):** Almacenada en una región de **Azure** distinta a la de producción.

## 3. Arquitectura de Recuperación en Azure
Utilizamos las siguientes herramientas para garantizar la resiliencia:

| Componente | Estrategia | Herramienta Azure |
| :--- | :--- | :--- |
| **Bases de Datos** | Geo-Replicación / Point-in-time Restore | Azure SQL / Flexible Server PostgreSQL |
| **Máquinas Virtuales** | Replicación de sitio a sitio | **Azure Site Recovery (ASR)** |
| **Archivos/Files** | Backup inmutable (Protección contra Ransomware) | **Azure Backup (Recovery Services Vault)** |

## 4. Flujo de Respuesta ante Incidencias
1.  **Detección:** Alerta de monitoreo (Azure Monitor) indicando caída de servicios.
2.  **Evaluación:** Clasificación del incidente como "Desastre" por el comité de crisis.
3.  **Activación:** Ejecución de los *Runbooks* de recuperación.
4.  **Restauración:** Levantamiento de la infraestructura en la región secundaria.
5.  **Comunicación:** Notificación a las partes interesadas (Stakeholders).

## 5. Plan de Pruebas y Simulacros
El DRP no es válido si no se prueba.
*   **Frecuencia:** Semestral.
*   **Método:** Simulación de fallo de región o ataque de Ransomware.
*   **Resultado:** Informe de lecciones aprendidas y ajuste de tiempos RTO/RPO.

---
**Responsable del diseño:** Yeison Valdeblanquez  
**Especialidad:** Gestión de Infraestructura y Resiliencia de Datos
