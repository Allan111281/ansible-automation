---

# 📌 Git → Confluence Sync (Ansible)

Denne side dokumenterer en automatiseret Ansible-løsning, der synkroniserer dokumentation fra et Git repository til Confluence.

Git fungerer som **source of truth**, mens Confluence fungerer som den **læsevenlige dokumentationsplatform**.

Indholdet på denne side opdateres automatisk ved hver kørsel af playbooken.

---

# ⚙️ Funktion

Løsningen håndterer automatisk:

- Henter `.md` filer fra Git repository
- Konverterer Markdown til HTML
- Opdaterer én Confluence side (single-page mode)
- Opretter siden hvis den ikke findes
- Overskriver indhold ved ændringer i Git

---

# 🧠 Single Page Mode

Denne løsning bruger **én Confluence side pr. repository**.

Det betyder:

✔ Ingen duplicates  
✔ Samlet dokumentation ét sted  
✔ Automatisk overwrite ved ændringer  
✔ Ingen side-sprawl i Confluence  

---

# 📍 Confluence struktur

Siden oprettes som child page under:
