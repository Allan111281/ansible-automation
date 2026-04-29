🔐 Certificate Deployment via KeePassXC (Ansible)

Denne playbook bruges til automatisk udrulning af SSL/PFX-certifikater fra en KeePassXC database til Windows hosts.

Den er designet til drift, hvor certifikater skal kunne eksporteres og installeres konsistent på tværs af servere uden manuel håndtering.

⚙️ Funktionalitet

Playbooken udfører følgende proces:

1. Forberedelse
Opretter midlertidig mappe på Windows hosts (C:\temp\certificates)
Gør klar til eksport af certifikater

2. Hentning fra KeePassXC
Logger ind i KeePassXC database
Finder alle entries under gruppen Certificates
Henter:
entry-navne
passwords
attachments (.pfx / .p12)

3. Eksport
Ekstraherer certifikater fra KeePassXC database
Gemmer dem lokalt på Windows host i temp folder

4. Installation
Importerer certifikater til:
LocalMachine\My
Bruger korrekt password pr. certifikat
Sikrer at private keys følger med

5. Verifikation
Lister installerede certifikater
Viser Subject + Thumbprint for validering

🚀 Kørsel (deployment guide)

1. Hent repository

git clone https://github.com/Allan111281/ansible-automation.git

2. Gå ind i projektet

cd ansible-automation

3. Kontrollér inventory

Sørg for at Windows hosts er defineret korrekt:

inventory.ini

Eksempel:

[windows]
server1
server2
server3

4. Kør playbooken

ansible-playbook windows_certificates_keepass_deploy.yml

5. Indtast KeePass password

Ved execution bliver du bedt om:

KeePass master password

Dette bruges til at dekryptere database og hente certifikater.

🧠 Drift og adfærd

Certifikater deployes automatisk fra KeePassXC
Samme struktur anvendes på alle Windows hosts
Sikrer ensartet certificate store setup
Ingen manuel eksport/import nødvendig
Passwords håndteres sikkert via Ansible prompts

📌 Formål

Denne playbook bruges til:

central certificate management
automatisk udrulning af PFX/P12 certifikater
drift og sikkerhedsopsætning
standardisering af Windows certificate stores
