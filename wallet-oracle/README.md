# Renew of certificates on Oracle Wallet Version

This Ansible role automates the Renew of the Certificate from the Oracle Database Wallet.

## Requirements

- Ansible 2.10+
- Renew the certificates:
  - Remove the oldest version of the subcat and ca certificate from the wallet
  - Copy the 2 certificate to /tmp folder
  - Add the new 2 certificate to the oracle Wallet
- Create a new Oracle Wallet and Add new credential to the wallet
  - Create a new Oracle Wallet
  -  Add by hostname the new credential to the wallet

## Role Variables

The following variables are already defined on the defaults/main.yml file, the file is encrypt. 


```
wallet_path: "/oracle/wallets/fapdb"
oracle_base: "/oracle"
oracle_home: "/oracle/app/oracle/product/19c/db"
certificate_ca_dn: CN=USERTrust RSA Certification Authority,O=The USERTRUST Network,L=Jersey City,ST=New Jersey,C=US
certificate_subca_dn: CN=Sectigo RSA Domain Validation Secure Server CA,O=Sectigo Limited,L=Salford,ST=Greater Manchester,C=GB
wallet_password: XXXXXXXXXXXXXwallet_name: "fapdb"
wallet_base: "/oracle/wallets"
wallet_path: "/oracle/wallets/fapdb"
oracle_base: "/oracle"
oracle_home: "/oracle/app/oracle/product/19c/db"
orapki_path: "/oracle/app/oracle/product/19c/db/bin"
mkstore_path: "/oracle/app/oracle/product/19c/db/bin"
certificate_ca_dn: CN=USERTrust RSA Certification Authority,O=The USERTRUST Network,L=Jersey City,ST=New Jersey,C=US
certificate_subca_dn: CN=Sectigo RSA Domain Validation Secure Server CA,O=Sectigo Limited,L=Salford,ST=Greater Manchester,C=GB
wallet_password: XXXXXX

databases:
  - hostname: "faplab-dboracle01.faplab.pt"
    wallets:
      - tnsnames: "FAPDEVDB"
        username: "sys" # DBA
        password: "XXXXX"
      - tnsnames: "ADMINDB"
        username: "dbbackup"
        password: "XXXXXX"

  - hostname: "faplab-dboraclest.faplab.pt"
    wallets:
      - tnsnames: "FAPDEVDB"
        username: "sys" # DBA
        password:  "XXXXXX"
      - tnsnames: "ADMINDB"
        username: "dbbackup"
        password: "XXXXXXX"


You can set these variables in your playbook in order to overwrite the ones on the defaults/main.yml file.

## Example Playbook

Here's an example playbook that uses the 'wallet-oracle' role:

```yaml
---
- hosts: Lab
  become: true
  roles:
    - wallet-oracle
  tags:
  - Oracle
```

In order to run:

```
Renew the certificates CA and SUBCA:
ansible-playbook wallet-oracle.yml --tags "renew-certificates"

Create a new wallet and add credential to the wallet:
ansible-playbook wallet-oracle.yml --tags "create-wallet"

```