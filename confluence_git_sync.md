# 📌 Git → Confluence Sync (Ansible)

Denne playbook synkroniserer automatisk `.md` filer fra Git til Confluence.

Git fungerer som den primære kilde for dokumentation (*source of truth*), mens Confluence bruges som den læsevenlige visning for brugerne.

Playbooken opretter nye sider og opdaterer eksisterende sider automatisk.

## ⚙️ Funktion

Playbooken håndterer automatisk:

* læser alle `.md` filer fra Git repository
* opretter én Confluence side pr. fil
* opdaterer eksisterende sider hvis filen ændres
* bruger filnavnet (uden `.md`) som sidens titel
* opretter alle sider som child pages under en valgt parent page

Eksempel:

`win_services_control_interactive.md`

bliver til siden:

`win_services_control_interactive`

## 📍 Sideplacering i Confluence

Alle sider oprettes som child pages under denne parent page:

https://confluence.umit.dk/spaces/SASDOK/pages/231933858/Ansible+Playbooks

Placeringen styres af disse værdier i playbooken:

```yaml
confluence_base_url: "https://confluence.umit.dk"
confluence_space_key: "SASDOK"
parent_page_id: "231933858"
```

### Forklaring

* `confluence_base_url` = Confluence URL
* `confluence_space_key` = hvilket Space siderne oprettes i
* `parent_page_id` = hvilken parent page siderne oprettes under

## ✏️ Ændre placering

Gå til projektet:

```bash
cd ansible-automation
```

Åbn playbooken:

```bash
sudo nano confluence_git_sync.yml
```

Ret disse værdier:

* `confluence_space_key`
* `parent_page_id`

## 🔎 Find parent page ID

Eksempel:

https://confluence.umit.dk/spaces/SASDOK/pages/231933858/Ansible+Playbooks

Her er page ID:

`231933858`

Dette bruges som `parent_page_id`.

## 🚀 Kør playbooken

Hent repository:

```bash
git clone https://github.com/Allan111281/ansible-automation.git
```

Gå ind i projektet:

```bash
cd ansible-automation
```

Kør playbooken:

```bash
ansible-playbook confluence_git_sync.yml
```

Ved kørsel bruges:

* Confluence email
* API token password

## 📌 Formål

Denne løsning sikrer:

* central dokumentation i Git
* automatisk synkronisering til Confluence
* ensartet struktur uden manuel vedligeholdelse
* tydelig adskillelse mellem Git og Confluence
