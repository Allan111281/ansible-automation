# 🪟 Windows Services Control (Interactive Ansible Playbook)

Denne playbook bruges til centraliseret og interaktiv styring af Windows services på tværs af flere servere.

Den gør det muligt hurtigt at få overblik over services og udføre handlinger uden direkte login på serverne.

## ⚙️ Funktionalitet

Playbooken arbejder i tre faser:

### 1. Service indsamling

* henter Windows services fra alle hosts
* filtrerer tekniske og irrelevante services fra
* gemmer en samlet service-liste pr. host

### 2. Brugerinteraktion

* viser samlet service-overblik
* brugeren vælger services
* brugeren vælger handling:

1 = Stop
2 = Start
3 = Restart

Eksempel:

`service1, service2`

### 3. Execution

* udfører valgt handling på alle Windows hosts
* sikrer ensartet handling på tværs af miljøet
* fejl på enkelte services ignoreres for fuld execution

## 🚀 Kør playbooken

Hent repository:

```bash
git clone https://github.com/Allan111281/ansible-automation.git
```

Gå ind i projektet:

```bash
cd ansible-automation
```

Kontrollér inventory:

```ini
[windows]
server1
server2
server3
```

Kør playbooken:

```bash
ansible-playbook win_services_control_interactive.yml
```

## 📌 Formål

Denne playbook bruges til:

* hurtig service kontrol i Windows miljøer
* drift og incident response
* samlet overblik over services på tværs af servere
* standardiseret drift uden RDP eller GUI adgang
