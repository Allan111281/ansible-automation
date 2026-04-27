## 🔧 Formål

Denne playbook henter alle `.md` filer fra et Git repository og opretter dem som sider i Confluence.

Hver `.md` fil bliver til:

* én Confluence-side
* med samme navn som filen (fx `win_service.md` → **win_service**)
* placeret under en fælles parent-side

---

## ⚙️ Hvordan det virker

1. **Cloner Git repo**
2. **Finder alle `.md` filer**
3. **Tjekker om siden allerede findes i Confluence**
4. Hvis IKKE:

   * opretter ny side
   * indsætter indhold fra `.md`
5. Hvis JA:

   * springer over (ingen fejl)

---

## 📁 Struktur (eksempel)

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

## 🚀 Kør playbook

```bash
ansible-playbook read-md-conf.yml
```

Du bliver bedt om:

* username
* password 

---

## ⚠️ Vigtigt

* Kun `.md` filer bliver brugt (ikke `.yml`)
* Sider bliver **ikke opdateret**, kun oprettet hvis de mangler
* Playbooken kører kun når du selv starter den (ikke automatisk)

---

## 🧠 Tip

Brug samme navn på filer:

```
playbook.yml
playbook.md
```

Så hænger dokumentation og kode altid sammen 👍

---

## 🧹 Cleanup

Efter kørsel bliver repo slettet fra `/tmp/repo` automatisk.

---

## 📌 Kort sagt

✔ Git = source of truth
✔ Confluence = visning
✔ Ansible = automation

---
