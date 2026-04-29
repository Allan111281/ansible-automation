🪟 Windows Services Control (Interactive Ansible Playbook)

Denne playbook bruges til centraliseret og interaktiv styring af Windows services på tværs af flere servere.

Den er designet til driftsscenarier, hvor man hurtigt skal kunne få overblik over services og udføre handlinger uden at logge direkte ind på servere.

⚙️ Funktionalitet

Playbooken kører i tre faser:

1. Service indsamling (alle hosts)
Henter alle Windows services fra alle hosts i inventory
Filtrerer tekniske/system-services fra
Gemmer en samlet service-liste pr. host

2. Central brugerinteraktion
Samler service-overblik fra alle servers
Viser listen til operatøren
Bruger input til:
valg af services (kommasepareret F.eks xxx,yyy)
valg af handling:
1 = Stop
2 = Start
3 = Restart

3. Execution (alle hosts)
Udfører valgt handling på de valgte services
Kører på alle Windows hosts i inventory
Sikrer ensartet handling på tværs af miljøet
Fejl på enkelte services ignoreres for at sikre fuld execution

🚀 Kørsel (deployment guide)

1. Hent repository

git clone https://github.com/Allan111281/ansible-automation.git

2. Gå ind i projektet

cd ansible-automation

3. Kontrollér inventory (vigtigt)

Sørg for at din Windows inventory er korrekt sat op i fx:

inventory.ini

Eksempel:

[windows]
server1
server2
server3

4. Kør playbooken

ansible-playbook win_services_control_interactive.yml


🧠 Drift og adfærd

Centraliseret service management på tværs af Windows miljø
Konsistent execution på alle hosts
Ingen manuel RDP nødvendig
Designet til drift, support og incident handling

📌 Formål

Denne playbook bruges til:

hurtig service kontrol i Windows miljøer
drift og incident response
samlet overblik over services på tværs af servers
standardiseret operation uden GUI adgang
