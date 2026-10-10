# 📝 Incident Report: INC-002 - Unauthorized Privilege Escalation

## 📌 Resumen General
- **ID del Incidente:** `INC-002`
- **Fecha/Hora:** 2026-09-27
- **Host Objetivo:** `WS2025-DC01` (Agente Wazuh `001`)
- **Severidad:** Alta (High)
- **Estado:** Contenido y Resuelto

---

## 🔍 Detección & Telemetría en SIEM (Wazuh)
Se identificó la adición no autorizada de un usuario no estándar (`UsuarioHacker`) al grupo local de privilegios elevados `Administradores`.

- **Regla Wazuh:** `60143` (*User added to a local security group*) / `60109`
- **Event ID Windows:** `4732`
- **Target User:** `UsuarioHacker`
- **Target Group:** `Administradores`

---

## 🛠️ Acciones de Mitigación y Respuesta (PowerShell)
Se ejecutó la revocación de privilegios y depuración inmediata del objeto de usuario:

powershell
# Remoción de la cuenta del grupo y purga del sistema
net user UsuarioHacker /delete
---

## 🎯 Mapeo MITRE ATT&CK
- **Táctica:** Privilege Escalation (`TA0004`) / Persistence (`TA0003`)
- **Técnica:** Account Manipulation (`T1098`)
