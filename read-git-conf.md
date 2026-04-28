# 🔐 Certificate Deployment via KeePassXC (Ansible)

# 📌 Beskrivelse
Denne playbook automatiserer eksport og installation af SSL/PFX-certifikater fra en KeePassXC database til Windows hosts.

Certifikater importeres direkte i:
Local Computer\Personal\Certificates


# ⚙️ Hvad gør playbooken?

Playbooken udfører følgende trin:

1. Opretter midlertidig mappe på Windows hosts
2. Henter alle certificate entries fra KeePassXC
3. Udtrækker:
   - Entry navne
   - Passwords
   - Attachments (.pfx / .p12)
4. Eksporterer certifikater fra KeePassXC database
5. Importerer certifikater til Windows Certificate Store
6. Verificerer installation


# 📦 Krav

### Control node
- Ansible 2.14+
- ansible.windows collection

Install:
ansible-galaxy collection install ansible.windows
