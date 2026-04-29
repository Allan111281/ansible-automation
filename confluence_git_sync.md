# 📌 Git → Confluence Sync (Ansible)

Denne playbook holder Confluence automatisk synkroniseret med dokumentation fra Git.

Git er den primære kilde (*source of truth*), mens Confluence fungerer som et læsevenligt dokumentationslag.

---

## ⚙️ Funktion

Playbooken håndterer automatisk:

* læser alle `.md` filer fra Git repository
* opretter en Confluence side pr. fil
* opdaterer eksisterende sider hvis filen ændres
* bruger filnavnet (uden `.md`) som sidens titel
* opretter alle sider som child pages under en defineret parent page

### Eksempel

`win_services_control_interactive.md`
→ `win_services_control_interactive`

---

## 📍 Sideplacering i Confluence

Alle sider oprettes som child pages under:

`https://confluence.umit.dk/spaces/SASDOK/pages/231933858/Ansible+Playbooks`

Placeringen styres af følgende værdier i playbooken:

```yaml
confluence_base_url: "https://confluence.umit.dk"
confluence_space_key: "SASDOK"
parent_page_id: "231933858"
```

### Definition

* `confluence_base_url` → Confluence system URL
* `confluence_space_key` → hvilket Space sider oprettes i
* `parent_page_id` → hvilken parent page alle sider oprettes under

---

## ✏️ Ændring af placering

### Gå til projektet

```bash
cd ansible-automation
```

### Åbn playbooken

```bash
sudo nano confluence_git_sync.yml
```

### Ret disse værdier

* `confluence_space_key`
* `parent_page_id`

---

## 🔎 Find ny parent page

Eksempel:

`https://confluence.umit.dk/spaces/SASDOK/pages/231933858/Ansible+Playbooks`

Her er page ID:

`231933858`

Dette bruges som `parent_page_id`.

---

## 🚀 Kørsel

```bash
git clone https://github.com/Allan111281/ansible-automation.git
cd ansible-automation
ansible-playbook confluence_git_sync.yml
```

Ved kørsel bruges:

* Confluence email
* API token password

---

## 📌 Formål

Denne løsning sikrer:

* centraliseret dokumentation i Git
* automatisk synkronisering til Confluence
* ensartet struktur uden manuel vedligeholdelse
* tydelig adskillelse mellem udvikling og visning
