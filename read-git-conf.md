# 📄 Sync README.md til Confluence

## 🔧 Formål

Denne playbook henter alle `.md` filer fra et Git repository og opretter dem som sider i Confluence.

Hver `.md` fil bliver:

* en selvstændig side i Confluence
* navngivet efter filen (fx `win_service.md` → **win_service**)
* placeret under en fælles parent-side

---

## ⚙️ Funktion

Playbooken udfører følgende:

1. Kloner Git repository
2. Finder alle `.md` filer
3. Tjekker om siden allerede findes i Confluence
4. Hvis siden ikke findes:

   * opretter ny side
   * indsætter indhold fra `.md`
5. Hvis siden findes:

   * springer over (ingen fejl)

---

## ⚠️ Vigtigt (Auto-generated sider)

Alle sider oprettet af denne playbook indeholder følgende besked:

* Siden er **automatisk genereret fra Git**
* Ændringer i Confluence vil kunne blive overskrevet
* Rettelser skal foretages i **README.md i Git**

👉 Confluence bruges kun til visning – ikke redigering

---

## 📁 Struktur

Git:

```
win_service.yml
win_service.md
im_kp_cert.yml
im_kp_cert.md
```

Confluence:

```
Ansible Playbooks Readme
├── win_service
└── im_kp_cert
```

---

## 🚀 Kørsel

```
ansible-playbook read-md-conf.yml
```

---

## 📌 Kort sagt

* Git = source of truth
* README.md = dokumentation
* Ansible = synkronisering
* Confluence = præsentation

---
