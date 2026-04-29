# 🔐 Certificate Deployment via KeePassXC (Ansible)

Denne playbook bruges til automatisk udrulning af SSL/PFX-certifikater fra en KeePassXC database til Windows hosts.

Den er designet til drift, hvor certifikater skal kunne eksporteres og installeres ensartet på tværs af servere uden manuel håndtering.

---

## ⚙️ Funktionalitet

Playbooken udfører følgende proces:

### 1. Forberedelse

* opretter midlertidig mappe på Windows hosts
  `C:\temp\certificates`
* gør klar til eksport af certifikater

---

### 2. Hentning fra KeePassXC

* logger ind i KeePassXC database
* finder alle entries under gruppen `Certificates`

Henter følgende:

* entry-navne
* passwords
* attachments (`.pfx` / `.p12`)

---

### 3. Eksport

* ekstraherer certifikater fra KeePassXC database
* gemmer dem lokalt på Windows host i temp folder

---

### 4. Installation

Importerer certifikater til:

`LocalMachine\My`

Dette sikrer:

* korrekt password pr. certifikat
* private keys følger med
* ensartet installation på alle hosts

---

### 5. Verifikation

* lister installerede certifikater
* viser `Subject` og `Thumbprint` til validering

---

## 🚀 Kørsel (Deployment Guide)

### 1. Hent repository

```bash id="ovhwsu"
git clone https://github.com/Allan111281/ansible-automation.git
```

---

### 2. Gå ind i projektet

```bash id="6u17ec"
cd ansible-automation
```

---

### 3. Kontrollér inventory

Sørg for at Windows hosts er korrekt defineret i:

`inventory.ini`

### Eksempel

```ini id="4czwsk"
[windows]
server1
server2
server3
```

---

### 4. Kør playbooken

```bash id="1dpkp1"
ansible-playbook windows_certificates_keepass_deploy.yml
```

---

### 5. KeePass login

Ved execution bliver du bedt om:

`KeePass master password`

Dette bruges til at dekryptere databasen og hente certifikaterne.

---

## 🧠 Drift og adfærd

Denne playbook sikrer:

* central certificate management
* automatisk deployment af PFX/P12 certifikater
* ensartet certificate store setup
* ingen manuel eksport/import
* sikker håndtering af passwords via Ansible prompt

---

## 📌 Formål

Denne playbook bruges til:

* certificate management
* SSL/PFX deployment
* drift og sikkerhedsopsætning
* standardisering af Windows certificate stores
