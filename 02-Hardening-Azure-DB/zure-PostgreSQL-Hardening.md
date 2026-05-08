# Guía de Hardening: Azure & PostgreSQL

Este recurso detalla los controles técnicos necesarios para asegurar una instancia de base de datos en la nube y la infraestructura de red circundante, alineado con el **Benchmark de CIS (Center for Internet Security)**.

## 1. Seguridad a Nivel de Red (Azure Networking)
El objetivo es eliminar la exposición pública y segmentar el tráfico.

*   **Azure Private Link:** Deshabilitar el acceso público y utilizar *Private Endpoints* para que el tráfico viaje exclusivamente por la red privada de Microsoft.
*   **Network Security Groups (NSG):** Configurar reglas de entrada (Inbound) para permitir tráfico únicamente desde el segmento de red de la aplicación (Web-Subnet) hacia el puerto 5432.
*   **Azure Bastion:** Utilizar Bastion para acceso administrativo RDP/SSH, eliminando la necesidad de asignar IPs públicas a las máquinas de gestión.

## 2. Configuración de Base de Datos (PostgreSQL/Oracle)
*   **Cifrado en Reposo:** Habilitar *Transparent Data Encryption (TDE)* gestionado con Azure Key Vault (Customer Managed Keys).
*   **Cifrado en Tránsito:** Forzar el parámetro `ssl_enforcement = ON` para todas las conexiones.
*   **Logging y Auditoría:** Habilitar el envío de logs de auditoría (pgaudit) hacia un espacio de trabajo de **Azure Log Analytics** para detección de anomalías.

## 3. Identidad y Acceso (IAM)
*   **Autenticación Entra ID (Azure AD):** Deshabilitar el usuario `admin` local y utilizar autenticación basada en identidades de Microsoft Entra ID.
*   **Principio de Menor Privilegio (PoLP):** Utilizar identidades administradas (Managed Identities) para que la aplicación Node.js se conecte a la DB sin usar contraseñas quemadas en el código.

---

## 🛠️ Script de Auditoría Rápida (Azure PowerShell)
Este comando permite verificar rápidamente si existen bases de datos con acceso público habilitado en la suscripción:

```powershell
# Verificar servidores de PostgreSQL con acceso público abierto
$servers = Get-AzPostgreSqlFlexibleServer
foreach ($server in $servers) {
    if ($server.NetworkPublicNetworkAccess -eq "Enabled") {
        Write-Host "⚠️ ALERTA: El servidor $($server.Name) tiene acceso público habilitado." -ForegroundColor Red
    } else {
        Write-Host "✅ El servidor $($server.Name) está protegido (Acceso privado)." -ForegroundColor Green
    }
}
