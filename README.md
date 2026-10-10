# 🛡️ Enterprise SOC Threat Hunting & Incident Response Lab (Wazuh SIEM)

## 📌 Resumen Ejecutivo
Este laboratorio documenta la implementación de un entorno operativo de **Centro de Operaciones de Seguridad (SOC)** enfocado en la detección de amenazas en tiempo real, análisis forense de telemetría y respuesta ante incidentes. 

El entorno utiliza **Wazuh SIEM Cloud**, **Sysmon** (con configuración avanzada de SwiftOnSecurity) y **Active Directory en Windows Server 2025** para auditar y monitorear tácticas del marco **MITRE ATT&CK**.

---

## 🏗️ Arquitectura de la Infraestructura

| Componente | Rol / Función | Sistema Operativo / Servicio |
| :--- | :--- | :--- |
| `WS2025-DC01` | Domain Controller / Agente Monitoreado | Windows Server 2025 + Sysmon (SwiftOnSecurity) |
| `Wazuh Cloud` | SIEM / Centralizador de Logs & Alertas | Wazuh Indexer & OpenSearch (DQL Queries) |
| `Analista SOC` | Estación de Respuesta e Investigación | Workstation Linux Mint |

---

## 🎯 Escenarios de Ataque Simulados & Detecciones en SIEM

### 1. Detección de Autenticación Anómala y Fuerza Bruta (MITRE T1110 / T1078)
- **Descripción:** Simulación e investigación de intentos masivos de autenticación fallidos por la red (`Logon Type 3` / `Logon Type 10`).
- **Telemetría:** Windows Event ID `4625` / Wazuh Rule ID `60115` (*Windows Logon Failure*).
- **Mitigación:** Aislamiento y desactivación preventiva de cuenta mediante PowerShell (`Disable-LocalUser` / `Disable-ADAccount`).

### 2. Detección de Persistencia vía Creación de Usuarios (MITRE T1136)
- **Descripción:** Monitoreo en tiempo real de cuentas locales creadas de forma no autorizada para mantener acceso persistente en el sistema.
- **Telemetría:** Windows Event ID `4720` / Wazuh Rule ID `60109` (*User account enabled or created*).
- **Mitigación:** Identificación del evento de auditoría y depuración forzada del usuario no autorizado.

### 3. Detección de Escalación de Privilegios (MITRE T1098)
- **Descripción:** Adición no autorizada de cuentas de usuario estándar al grupo privilegiado `Administradores`.
- **Telemetría:** Windows Event ID `4732` / Wazuh Rule ID `60143` (*Security group modification*).
- **Mitigación:** Revocación inmediata de privilegios y purga de la cuenta de origen.

### 4. Detección de Persistencia por Tareas Programadas (MITRE T1053)
- **Descripción:** Inserción de tareas persistentes en el sistema mediante `schtasks` para ejecución automática de código.
- **Telemetría:** Windows Event ID `4698` / Sysmon Event ID `1` / Wazuh Rule ID `60642` / `60178`.
- **Mitigación:** Eliminación forzada de la tarea programada (`schtasks /delete`).

---

## 📑 Reportes de Incidentes (SOC Playbooks)
Los casos de uso e investigaciones paso a paso redactados durante los triage se encuentran archivados en la carpeta [`/playbooks/`](./playbooks/):
- `INC-001-BruteForce-AccountDisable.md`
- `INC-002-PrivilegeEscalation.md`
- `INC-003-PersistenceScheduledTasks.md`

---

## 🚀 Certificaciones & Habilidades Clave
- **Cisco Cybersecurity Defense Analyst Career Path** (SOC Operations & Splunk Fundamentals).
- **Habilidades Tácticas:** Threat Hunting, DQL/Lucene Querying, Windows Event Auditing, Sysmon Fine-Tuning, PowerShell Mitigation Scripts, MITRE ATT&CK Mapping.
