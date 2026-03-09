# 🔒 ES (Session Terminator)

> PowerShell script that **terminates non-console RDP/session logins** — keeps only console (local) sessions. Runs as a background job every 5 seconds.

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🔒 **Session Control** | Lists and terminates non-console sessions |
| ⏰ **Background Job** | Runs every 5 seconds via scheduled task |
| 📋 **Persistence** | Registers `RunESAtLogon` under SYSTEM |
| 📝 **Logging** | Logs to `%TEMP%\SessionTerminator.log` |
| 📂 **Copy** | Installs to `C:\Windows\Setup\Scripts\Bin` |

---

## 📋 Requirements

| Requirement | Details |
|-------------|---------|
| **OS** | Windows 10/11, Server |
| **PowerShell** | 5.1+ |
| **Privileges** | Administrator |

---

## 🚀 Usage

```powershell
# Run once — registers scheduled task and starts background job
.\ES.ps1
```

---

## ⚠️ Warning

Terminating sessions will disconnect remote users (RDP, etc.). Use only when you want to prevent remote logins.

---

<p align="center">
  <sub>🛡️ Gorstak Security Tooling</sub>
</p>
