
---

# 📄 2. `win_service.md`

```md
# 🪟 Windows Service Management via Ansible

## 📌 Beskrivelse
Denne løsning bruges til at administrere Windows services på tværs af flere servere.

Brugeren kan:
- Se services fra alle hosts
- Vælge services interaktivt
- Stoppe / starte / genstarte services

---

## 🏗️ Arkitektur

### 1. Data Collection
Alle Windows hosts indsamler services:
- Filtrerer system/irrelevante services
- Samler DisplayName

### 2. User Interaction
Brugeren vælger:
- Services (kommasepareret)
- Handling (stop/start/restart)

### 3. Execution
Valgte actions udføres på alle hosts

---

## 📁 Inventory krav

```ini
[windows]
server1
server2
server3
