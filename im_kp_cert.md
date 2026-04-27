# 🔐 Ansible Certificate Deployment via KeePassXC

Denne Ansible playbook automatiserer eksport og installation af SSL-/PFX-certifikater fra en KeePassXC database til Windows hosts.

Playbooken er designet til sikker, automatiseret deployment af certifikater til `LocalMachine\My` store.

---

## ⚙️ Hvad gør playbooken?

Playbooken udfører følgende trin:

1. Opretter midlertidig mappe på Windows host
2. Henter alle certificate entries fra KeePassXC
3. Udtrækker:
   - Entry navne
   - Passwords
   - Attachments (.pfx / .p12)
4. Eksporterer certifikater fra KeePassXC database
5. Importerer certifikater til Windows Certificate Store
6. Verificerer installation
7. (Valgfrit) Rydder op i temp filer

---

## 📦 Krav

### Control node (Ansible)
- Ansible 2.14+
- `ansible.windows` collection

Install:
```bash
ansible-galaxy collection install ansible.windows
