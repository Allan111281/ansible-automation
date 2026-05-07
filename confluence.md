# 📌 Git → Confluence Single Page Sync (Ansible)

## 🧭 Overblik

Denne løsning synkroniserer automatisk én Markdown fil fra et Git repository til én Confluence side.

Git er **source of truth**, og Confluence fungerer som read-only dokumentationsvisning.

---

# ⚙️ Konfiguration (VIGTIG)

Alle ændringer foretages i playbooken:  
👉 `confluence_git_sync.yml`

---

## 📁 Git repository (KILDE)

Dette er det repository der bliver synkroniseret fra:

git_repo: https://github.com/Allan111281/ansible-automation.git  

📌 Ændres hvis du vil skifte source repo

---

## 📂 Lokalt workspace

repo_dest: /tmp/repo  

👉 Midlertidig mappe hvor Git bliver cloned

---

## 📍 Confluence destination (SIDE PLACERING)

Disse værdier styrer hvor siden oprettes i Confluence:

confluence_base_url: https://confluence.umit.dk  
confluence_space_key: SASDOK  
parent_page_id: 231933858  

### Forklaring:

- confluence_base_url → Confluence server
- confluence_space_key → hvilket space siden ligger i
- parent_page_id → hvilken parent page siden oprettes under

📌 Hvis du vil flytte siden i Confluence → ændr parent_page_id

---

## 🏷️ Side navn (vigtigt)

Når du kører playbooken bliver du bedt om:

👉 Confluence page title

Dette bestemmer:

- om siden oprettes
- eller om en eksisterende side opdateres

📌 Dette er den eneste “runtime binding” til siden

---

# 🚀 Sådan kører du løsningen

## 1. Clone repo

git clone https://github.com/Allan111281/ansible-automation.git  

---

## 2. Gå ind i projekt

cd ansible-automation  

---

## 3. Kør playbook

ansible-playbook confluence.yml  

---

## 4. Indtast værdier

Ved kørsel bliver du spurgt om:

- Confluence email
- API token
- Page title

---

# 🔄 Hvad der sker når den kører

1. Git repo clones
2. `.md` fil findes automatisk
3. Pandoc installeres automatisk (hvis ikke installeret)
4. Markdown konverteres til HTML
5. Confluence side findes via title + space
6. Side oprettes eller opdateres
7. Ny version gemmes i Confluence

---

# 📄 Single Page Mode

✔ 1 repo → 1 Confluence side  
✔ ingen duplicates  
✔ altid update/create  
✔ versionsstyring i Confluence  

---

# ⚠️ VIGTIGT (READ THIS)

- Confluence må IKKE redigeres manuelt
- Alt content kommer fra Git
- Hver sync overskriver Confluence content
- Git er eneste source of truth

---

# 📌 Formål

✔ Git som source of truth  
✔ automatiseret Confluence sync  
✔ ingen manuel dokumentation  
✔ ensartet og centraliseret docs system  
