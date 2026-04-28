# 📄  win_service.md


# 🪟 Windows Service Management via Ansible

# 📌 Beskrivelse
Denne løsning bruges til at administrere Windows services på tværs af flere servere.

Brugeren kan:
- Se services fra alle hosts
- Vælge services interaktivt
- Stoppe / starte / genstarte services


# 🏗️ Arkitektur

#  Data Collection
Alle Windows hosts indsamler services:
- Filtrerer system/irrelevante services
- Samler DisplayName

#  User Interaction
Brugeren vælger:
- Services (kommasepareret)
- Handling (stop/start/restart)

#  Execution
Valgte actions udføres på alle hosts


#  📁 Inventory krav


[windows]
server1
server2
server3
