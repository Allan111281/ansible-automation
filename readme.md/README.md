# Guide: Ansible Vault, vault_password_file og ansible.cfg

## Formål

Denne guide forklarer helt simpelt hvordan vi håndterer passwords og settings i Ansible.

Vi bruger:

* Ansible Vault til at gemme passwords sikkert
* `vault_password_file` til automatisk dekryptering
* `ansible.cfg` til standard opsætning

Målet er:

* ingen passwords i clear text
* nem automation (Jenkins / scripts)
* ens setup på alle playbooks

---

# 1. Ansible Vault (hvad er det?)

Ansible Vault bruges til at kryptere sensitive data.

Det betyder:

❌ Ikke synlige passwords i Git
✔ Krypterede credentials i repo

---

## Eksempel på hvad der ligger i Vault

```yaml
ansible_user: alchr@ELEV1.LOCAL
ansible_password: SuperSecretPassword
ansible_connection: winrm
ansible_winrm_transport: kerberos
ansible_port: 5986
ansible_winrm_server_cert_validation: ignore
```

---

## Opret Vault fil

```bash
ansible-vault create group_vars/windows/vault.yml
```

## Redigér Vault fil

```bash
ansible-vault edit group_vars/windows/vault.yml
```

## Krypter eksisterende fil

```bash
ansible-vault encrypt group_vars/windows/vault.yml
```

---

# 2. vault_password_file

## Hvad er det?

`vault_password_file` er en lokal fil som indeholder passwordet til Ansible Vault.

Ansible bruger denne fil til automatisk at dekryptere Vault-filer uden at spørge om password hver gang.

---

## Sådan opretter du den

Opret filen i din hjemmemappe:

```bash
nano ~/.vault_pass
```

Indsæt et password (samme som bruges til Vault):

```text
MyVaultPassword123
```

Gem filen.

---

## Sæt korrekt sikkerhed

Filen må kun være læsbar for din egen bruger:

```bash
chmod 600 ~/.vault_pass
```

Dette betyder:

* Kun ejeren (dig) kan læse filen
* Andre brugere på systemet kan ikke se den

---

## Vigtigt

Denne fil gælder kun for **den bruger der ejer den**.

Eksempel:

* Hvis filen ligger i `/home/alchr/.vault_pass` → virker kun for bruger `alchr`
* Hvis Jenkins kører som `jenkins` → skal Jenkins have sin egen fil:

```text
/var/lib/jenkins/.vault_pass
```

👉 Hver bruger har sin egen Vault password file
👉 Der deles ikke én fælles fil mellem brugere

---

## VIGTIGT

❌ Må aldrig pushes til Git

Denne fil indeholder password til Ansible Vault. Hvis den bliver committed til Git, kan alle med adgang til repository dekryptere dine secrets.

Derfor skal den beskyttes via `.gitignore`.

---

## Hvad er .gitignore?

`.gitignore` er en simpel tekstfil i dit Git repository som fortæller Git hvilke filer der skal ignoreres.

Det betyder:

* Git vil ikke tracke filerne
* Git vil ikke vise dem som ændret
* Git vil ikke inkludere dem i commits

Det bruges især til:

* passwords
* lokale konfigurationsfiler
* logs
* midlertidige filer

---

## Sådan opretter du .gitignore

Gå til roden af dit repository og opret filen:

```bash
nano .gitignore
```

Eller:

```bash
touch .gitignore
```

---

## Eksempel på indhold

```gitignore
# Vault password file
.vault_pass

# Ansible retry files
*.retry

# Logs
*.log
```

---

## Hvordan virker det i praksis?

Når du har tilføjet en fil i `.gitignore`:

```text
.vault_pass
```

så vil Git automatisk ignorere den fil fremover.

⚠️ Hvis filen allerede er committed, skal den fjernes fra Git med:

```bash
git rm --cached .vault_pass
```

---

`.gitignore` er en fil som fortæller Git hvilke filer den skal ignorere.

Når en fil er tilføjet i `.gitignore`, vil Git:

* ikke tracke filen
* ikke vise den som ændret
* ikke pushe den til Git repository

---

---

# 3. ansible.cfg ansible.cfg

## Hvad er det?

Det er Ansible sin standard konfigurationsfil.

Den gør at du slipper for at skrive ting hver gang.

---

## Standard setup

```ini
[defaults]
inventory = inventories/dev.yml
vault_password_file = ~/.vault_pass
host_key_checking = False
```

---

## Forklaring

### inventory

Hvilke servere Ansible rammer som default.

---

### vault_password_file

Fortæller hvor password til Vault ligger.

Gør automation muligt uden prompt.

---

### host_key_checking

Slår SSH warning fra ved nye hosts.

Bruges i automation miljøer.

---

# 4. Hvordan det hænger sammen

Når du kører:

```bash
ansible-playbook -i inventory.ini playbook.yml
```

sker dette:

1. ansible.cfg læses
2. vault_password_file findes
3. vault.yml dekrypteres
4. credentials indlæses
5. connection til Windows servere
6. playbook køres

---

# 5. Regler (meget vigtigt)

## Må i Git

✔ playbooks
✔ inventory
✔ ansible.cfg
✔ krypteret vault.yml

## Må IKKE i Git

❌ .vault_pass
❌ passwords i clear text
❌ credentials

---

# 6. Kort opsummering

* Vault = sikker opbevaring af secrets
* vault_pass = lokal nøgle til dekryptering
* ansible.cfg = standard opsætning
* Git må aldrig indeholde passwords

---

# Målet

At gøre Ansible setup:

* sikkert
* simpelt
* ensartet
* klar til automation
