# 📝 Incident Report: INC-001 - Brute Force & Account Containment

## 📌 Resumen General
- **ID del Incidente:** `INC-001`
- **Fecha/Hora:** 2026-09-26
- **Host Objetivo:** `WS2025-DC01` (Agente Wazuh `001`)
- **Severidad:** Media / Alta
- **Estado:** Contenido y Resuelto

---

## 🔍 Detección & Telemetría en SIEM (Wazuh)
Durante el monitoreo en tiempo real, se detectaron múltiples intentos fallidos de autenticación en un corto intervalo de tiempo contra el servidor de dominio (`WS2025-DC01`).

- **Regla Wazuh:** `60115` (*Windows Logon Failure*)
- **Event ID Windows:** `4625`
- **Usuario Afectado:** `UsuarioPruebaSOC`
- **Tipo de Logon:** `LogonType 3` (Red / Autenticación remota)

---

## 🛠️ Acciones de Mitigación y Respuesta (PowerShell)
Como medida de contención inmediata para neutralizar el vector de ataque y prevenir un compromiso mayor, se procedió a deshabilitar la cuenta objetivo:

powershell
# Desactivación preventiva de la cuenta atacada
Disable-LocalUser -Name "UsuarioPruebaSOC"
---

## 📊 Verificación de Remedición
Se confirmó en la consola web de Wazuh Cloud la emisión de la alerta de verificación tras la desactivación exitosa de la cuenta:
- **Regla Wazuh:** `60109` / Event ID `4725` (*An account was disabled*)

---

## 🎯 Mapeo MITRE ATT&CK
- **Táctica:** Credential Access (`TA0006`)
- **Técnica:** Brute Force (`T1110`)
