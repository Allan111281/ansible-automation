# 🔄 Git → Confluence README Sync (Ansible)

Denne Ansible playbook automatiserer synkronisering af en `README.md` fra et Git repository til en Confluence side.

Formålet er at sikre, at dokumentation altid er **centralt opdateret i Confluence direkte fra Git**.

---

# ⚙️ Hvad gør playbooken?

Playbooken udfører følgende steps:

## 1. Klargøring
- Rydder lokal workspace (`/tmp/repo`)

## 2. Git integration
- Cloner GitHub repository
- Henter `README.md` fra `main` branch

## 3. Data processing
- Decoder README.md fra base64
- Forbereder content til Confluence

## 4. Confluence integration
- Henter nuværende side metadata (version control)
- Beregner næste version
- Opdaterer Confluence siden via REST API

## 5. Cleanup
- Sletter midlertidigt repo fra lokal maskine

---

# 🌐 Integration flow

```text id="flow1"
GitHub Repo → Ansible → README.md → Confluence Page
