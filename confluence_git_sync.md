# 📚 Full Git → Confluence Sync (Create + Update)

# 📌 Beskrivelse

Denne playbook synkroniserer automatisk `.md` filer fra et Git repository til Confluence.

Formålet er at gøre Git til den centrale source of truth for dokumentation, mens Confluence bruges som læsevenlig visning for brugerne.

Playbooken kan både:

* oprette nye sider
* opdatere eksisterende sider

Det betyder, at ændringer i Git automatisk bliver pushed til Confluence ved næste deployment.

Brugere kan derfor altid stole på, at Confluence viser den nyeste version af dokumentationen.

# ⚙️ Hvad gør playbooken?

Playbooken udfører følgende trin:

1. Rydder midlertidigt workspace på control node

2. Cloner Git repository lokalt

3. Finder alle `.md` filer i repository

4. Tjekker om siden allerede findes i Confluence

5. Henter page ID og version number for eksisterende sider

6. Læser indholdet af markdown-filerne

7. Opretter nye sider med POST hvis siden ikke findes

8. Opdaterer eksisterende sider med PUT hvis siden allerede findes

9. Tilføjer informationsbanner i toppen af siden

10. Rydder op efter execution

# 🔁 Create + Update logik

Hvis siden ikke findes:

→ siden oprettes automatisk

Hvis siden allerede findes:

→ siden opdateres automatisk med nyeste indhold fra Git

Dermed bliver Git altid master-versionen, og Confluence bliver automatisk opdateret.

# 📦 Krav

# Control node

* Ansible 2.14+
* Git installeret
* adgang til Git repository
* adgang til Confluence REST API
* gyldig Confluence API token

# 🔐 Authentication

Login sker med:

* Confluence email
* Confluence API token

Vigtigt:

Hvis API token er oprettet på en service account, skal samme bruger bruges ved login.

Username og token skal altid høre sammen.

# 📝 Resultat i Confluence

Hver side får automatisk:

* tydelig besked om at siden er genereret via Ansible
* advarsel om at siden kan blive overskrevet
* besked om at ændringer skal laves i Git
* automatisk opdatering ved næste deployment

# ▶️ Kør playbooken

ansible-playbook read-git-conf.yml

# 🚀 Typisk brug

Bruges typisk til:

* driftsvejledninger
* deployment guides
* playbook dokumentation

