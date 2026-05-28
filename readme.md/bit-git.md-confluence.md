# 📌 Git/Bit → Confluence Sync Playbook

## 🔎 Hvad gør denne playbook?

Denne playbook synkroniserer automatisk en Markdown-fil fra et Git/Bit repository til en Confluence-side.

Den:
- Henter et Git/Bit repository via SSH
- Finder en `.md` fil
- Konverterer Markdown til HTML
- Opretter eller opdaterer en Confluence-side
- Rydder automatisk op efter sig selv

👉 Kører lokalt (localhost)  
👉 Kræver ingen inventory file  
👉 Midlertidige filer slettes efter kørsel  

---

## 🔑 Krav

- SSH adgang til Git/Bit repository
- Confluence adgang (email + API token/password)

---
## 📍 Confluence placering

Disse værdier bestemmer hvor siden oprettes i Confluence:

```yaml
confluence_base_url: "https://confluence.umit.dk"
confluence_space_key: "SASDOK"
parent_page_id: "231933858"
```
- Forklaring
- confluence_base_url → Confluence server (ændres normalt ikke)
- confluence_space_key → hvilket Confluence space siden oprettes i
- parent_page_id → hvilken side i Confluence den bliver placeret under

👉 Hvis siden skal flyttes i Confluence, er det primært parent_page_id der skal ændres

---

## ⚙️ Kørsel

```bash
ansible-playbook bit-git.md-confluence.yml
```
Du bliver spurgt om:
- Git/Bit SSH URL  
- Confluence email  
- Confluence API token/password  
- Confluence page title 👉 Dette bliver sidens navn i Confluence  

---

## 📌 Resultat

Når playbooken er færdig:

- Markdown hentes fra Git  
- HTML genereres automatisk  
- Confluence side oprettes eller opdateres hvis man bruger samme navn på siden  
- Alt midlertidigt data fjernes igen  
