# 📝 Incident Report: INC-003 - Persistence via Scheduled Tasks

## 📌 Resumen General
- **ID del Incidente:** `INC-003`
- **Fecha/Hora:** 2026-09-27
- **Host Objetivo:** `WS2025-DC01` (Agente Wazuh `001`)
- **Severidad:** Alta (High)
- **Estado:** Contenido y Resuelto

---

## 🔍 Detección & Telemetría en SIEM (Wazuh / Sysmon)
Se detectó la creación anómala de una tarea programada (`ServiceUpdate_SOC`) configurada para ejecutar `powershell.exe` en segundo plano, simulando un mecanismo de persistencia para mantener acceso en el servidor objetivo.

- **Reglas Wazuh:** `60178` / `60642` (*Scheduled task created / modified*)
- **Sysmon Event ID:** `1` (*Process Creation*)
- **Task Name:** `\ServiceUpdate_SOC`
- **Command Executed:** `powershell.exe -WindowStyle Hidden -NoProfile`

---

## 🛠️ Acciones de Mitigación y Respuesta (PowerShell / CLI)
Se procedió a la eliminación forzada del mecanismo de persistencia para dejar el sistema operativo en estado seguro:

powershell
# Depuración de la tarea programada no autorizada
schtasks /delete /tn "ServiceUpdate_SOC" /f

---

## 🎯 Mapeo MITRE ATT&CK
- **Táctica:** Persistence (`TA0003`) / Execution (`TA0002`)
- **Técnica:** Scheduled Task/Job (`T1053.005`)
