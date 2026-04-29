# 🔐 Certificate Deployment via KeePassXC (Ansible)

Denne playbook bruges til automatisk deployment af SSL/PFX-certifikater fra en KeePassXC database til Windows hosts.

Den sikrer ensartet installation af certifikater uden manuel eksport og import.

## ⚙️ Funktionalitet

Playbooken udfører følgende proces:

### 1. Forberedelse

* opretter midlertidig mappe:

`C:\temp\certificates`

* klargør Windows hosts til certificate deployment

### 2. Hentning fra KeePassXC

* logger ind i KeePassXC databasen
* finder entries under gruppen `Certificates`
* henter:

  * entry-navne
  * passwords
  * attachments (`.pfx` / `.p12`)

### 3. Eksport

* eksporterer certifikater fra KeePassXC
* gemmer dem lokalt på Windows host

### 4. Installation

Importerer certifikater til:

`LocalMachine\My`

Dette sikrer:

* korrekt password pr. certifikat
* private keys følger med
* ensartet installation på alle hosts

### 5. Verifikation

* lister installerede certifikater
* viser Subject og Thumbprint til validering

## 🚀 Kør playbooken

Hent repository:

```bash
git clone https://github.com/Allan111281/ansible-automation.git
```

Gå ind i projektet:

```bash
cd ansible-automation
```

Kontrollér inventory:

```ini
[windows]
server1
server2
server3
```

Kør playbooken:

```bash
ansible-playbook windows_certificates_keepass_deploy.yml
```

Ved kørsel bliver du bedt om:

* KeePass master password

Dette bruges til at dekryptere databasen og hente certifikaterne.

## 📌 Formål

Denne playbook bruges til:

* central certificate management
* automatisk deployment af PFX/P12 certifikater
* drift og sikkerhedsopsætning
* standardisering af Windows certificate stores
