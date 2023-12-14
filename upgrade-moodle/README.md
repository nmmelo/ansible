# Update Moodle Version

This Ansible role automates the update of Moodle.

## Requirements

- Ansible 2.10+
- Supported target systems: Ubuntu 20.04 with PHP 7.4 and MYSQL 8.0.34.
- If the option is update-by-file, we need the file in /tmp folder with format moodle-latest.zip
- Check the plugins that need to be copy to the new folder. ( See defaults/main.yml for moodle_blocks, moodle_mod, moodle_theme, moodle_local, moodle_admin)
- Check the version that need to be download from moodle page. ( See defaults/main.yml for the moodle_url)
- Updated tnsname.ora file  (templates/tnsnames.j2)

## Role Variables

The following variables are already defined on the defaults/main.yml file. 


```
apache_path: "/var/www/"
moodle_path: "/var/www/moodle"
moodle_old: "/var/www/moodle_old"
folder_zip: "/tmp/"
moodle_url: "https://packaging.moodle.org/stable401/moodle-latest-401.zip"
moodle_file: "moodle-latest.zip"
http_proxy: "http://proxy01.com:8080/"
https_proxy: "http://proxy01.com:8080/"
moodle_blocks:
- attendance
- admin_presets
- checklist
- quickmail
moodle_mod:
- attendance
- customcert
- checklist
- hotpot
- hvp
- icontent
- journal
- lightboxgallery
- mindmap
- pcast
- questionnaire
- revealjs
- scheduler
moodle_theme:
- fap
- bootstrapbase
- adaptable
moodle_local:
- mailtest
- contact
- catdup
moodle_admin:
- mergeusers
```

You can set these variables in your playbook in order to overwrite the ones on the defaults/main.yml file.

## Example Playbook

Here's an example playbook that uses the 'update-moodle' role:

```yaml
---
- name: Upgrade a plataforma Moodle
  hosts: test
  become: true
  roles:
    - upgrade-moodle
```

In order to run:

```

Upgrade-by-file:
ansible-playbook oracle-install.yml --tags upgrade-by-file

Upgrade-by-url:
ansible-playbook oracle-install.yml --tags upgrade-by-url

```