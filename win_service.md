
---

## 🔁 Service actions
Playbooken understøtter:

- ▶️ Start services
- ⏹ Stop services
- 🔄 Restart services

---

# 🏗️ Architecture

Playbooken er opdelt i 3 faser:

### 1. Data Collection (alle hosts)
- Henter services fra hver Windows server
- Gemmer data pr. host i `host_services`

---

### 2. User Interaction (kun første host)
- Bygger samlet overview
- Viser services
- Indsamler bruger input

---

### 3. Execution (alle hosts)
- Udfører valgt action på valgte services
- Bruger `win_service` modul

---

# 📁 Inventory krav

Playbooken kræver en inventory med en Windows gruppe:

```ini
[windows]
server1
server2
server3
