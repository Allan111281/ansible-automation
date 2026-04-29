# 🪟 Windows Services Control (Interactive Ansible Playbook)

Denne playbook bruges til centraliseret og interaktiv styring af Windows services på tværs af flere servere.

Den er designet til driftsscenarier, hvor man hurtigt skal kunne få overblik over services og udføre handlinger uden at logge direkte ind på servere.

---

## ⚙️ Funktionalitet

Playbooken kører i tre faser:

### 1. Service indsamling (alle hosts)

* henter alle Windows services fra alle hosts i inventory
* filtrerer tekniske/system-services fra
* gemmer en samlet service-liste pr. host

---

### 2. Central brugerinteraktion

* samler service-overblik fra alle servers
* viser listen til operatøren

Bruger input til:

* valg af services (kommasepareret, fx `service1,service2`)
* valg af handling:

```text
1 = Stop
2 = Start
3 = Restart
```

---

### 3. Execution (alle hosts)

* udfører valgt handling på de valgte services
* kører på alle Windows hosts i inventory
* sikrer ensartet handling på tværs af miljøet
* fejl på enkelte services ignoreres for at sikre fuld execution

---

## 🚀 Kørsel (Deployment Guide)

### 1. Hent repository

```bash id="u0pw7o"
git clone https://github.com/Allan111281/ansible-automation.git
```

---

### 2. Gå ind i projektet

```bash id="b7vxk7"
cd ansible-automation
```

---

### 3. Kontrollér inventory

Sørg for at din Windows inventory er korrekt sat op i fx:

`inventory.ini`

### Eksempel

```ini id="fg0f5h"
[windows]
server1
server2
server3
```

---

### 4. Kør playbooken

```bash id="o44v3r"
ansible-playbook win_services_control_interactive.yml
```

---

## 🧠 Drift og adfærd

Denne playbook sikrer:

* centraliseret service management på tværs af Windows miljø
* konsistent execution på alle hosts
* ingen manuel RDP nødvendig
* hurtig support og incident handling

---

## 📌 Formål

Denne playbook bruges til:

* hurtig service kontrol i Windows miljøer
* drift og incident response
* samlet overblik over services på tværs af servers
* standardiseret operation uden GUI adgang
