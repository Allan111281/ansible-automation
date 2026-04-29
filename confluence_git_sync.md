📌 Git → Confluence Sync (Ansible)

Denne playbook holder Confluence automatisk synkroniseret med dokumentation fra Git.

Git er den primære kilde (source of truth), mens Confluence fungerer som et læsevenligt dokumentationslag.

⚙️ Funktion

Playbooken håndterer følgende automatisk:

Læser alle .md filer fra Git repository
Opretter en Confluence side pr. fil
Opdaterer eksisterende sider hvis filen ændres
Bruger filnavnet (uden .md) som sidens titel
Opretter alle sider som child pages under en defineret parent page

Eksempel:
win_services_control_interactive.md → win_services_control_interactive

📍 Sideplacering i Confluence

Alle sider oprettes som child pages under:

https://confluence.umit.dk/spaces/SASDOK/pages/231933858/Ansible+Playbooks

Placeringen styres af følgende parametre i playbooken:

confluence_base_url: "https://confluence.umit.dk"
confluence_space_key: "SASDOK"
parent_page_id: "231933858"

Definition:
confluence_base_url → Confluence system URL
confluence_space_key → Space hvor sider oprettes
parent_page_id → parent page som alle sider bliver child pages under

✏️ Ændring af placering

For at ændre hvor sider oprettes i Confluence:

1. Gå til projektet

cd ansible-automation

2. Åbn playbook

sudo nano confluence_git_sync.yml

3. Ret følgende værdier
confluence_space_key
parent_page_id

🔎 Find ny parent page

Åbn ønsket side i Confluence:

https://confluence.umit.dk/spaces/SASDOK/pages/231933858/Ansible+Playbooks

Her er page ID:

231933858

Dette ID bruges som parent_page_id.

🔁 Drift og adfærd

Nye .md filer → nye Confluence sider
Ændrede filer → opdaterer eksisterende sider
Filnavn styrer Confluence sidens titel
Struktur i Confluence styres centralt via parent page

🚀 Kørsel

git clone https://github.com/Allan111281/ansible-automation.git

cd ansible-automation
ansible-playbook confluence_git_sync.yml

Ved kørsel:

Confluence email
API token password

🧠 Formål

Denne løsning sikrer:

centraliseret dokumentation i Git
automatisk synkronisering til Confluence
ensartet struktur uden manuel vedligeholdelse
tydelig adskillelse mellem udvikling (Git) og visning (Confluence)
