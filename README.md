# Ansible Role mailcow

Install mailcow with [mailcow-dockerized]('https://github.com/mailcow/mailcow-dockerized.git')

## Collection dependencies

The role depends on the 
- collection community.docker
- ansible role 
Note that this also requires installation of the python libraries `docker` and `docker-compose`.

## Role Variables

| group | variable | default | description |
| --- | --- | ---| --- |
| basic | `mailcow_hostname` | | the host name for mailcow |
| basic | `mailcow_install_path` | `/opt/mailcow-dockerized` | the install path for mailcow |
| basic | `mailcow_timezone` | `Europe/Berlin` | the time zone for mailcow |
| basic | `mailcow_version` | `master` | the [version](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/| basic git_module.html#parameter-version) to checkout |
| basic | `mailcow_docker_compose_project_name` | `mailcow_dockerized` | the name for the mailcow docker compose project |
| basic | `mailcow_docker_compose_state` | `present` | state for [community.docker.docker_compose](https://docs.ansible.com/ansible/latest/collections/community/docker/docker_compose_module.html) |
| security | `mailcow_admin_user` | | the username of the mailcow administrator |
| security | `mailcow_admin_password` | | the password for the mailcow administrator |
| security | `mailcow_api_key` | | API key for mailcow read-write access (allowed characters: a-z, A-Z, 0-9, -) |
| security | `mailcow_api_key_read_only` | | API key for mailcow read-only access (allowed characters: a-z, A-Z, 0-9, -) |
| security | `mailcow_api_allow_from` | | comma separated list of IPs to allow API access from |
| security | `mailcow_rspamd_ui_password` | | the password for the mailcow Rspamd UI |
| security | `mailcow_delete_admin_script` |  `/root/ansible_mailcow_delete_admin.sh` | the path for the mailcow delete admin script |
| security | `mailcow_set_admin_script` | `/root/ansible_mailcow_set_admin.sh` | the path for the mailcow set admin script |
| security | `mailcow_set_rspamd_ui_password_script` | `/root/ansible_set_rspamd_ui_password.sh` | the path for the mailcow set Rspamd UI password script |
| https | `mailcow_acme` | `out-of-the-box` | the way the Let's Encrypt certificate ist obtained: <br/> `out-the-box`:  The "acme-mailcow" container will try to obtain a LE certificate. <br/> `certbot`: The certbot cronjob will manage Let's Encrypt certificates |
| https | `mailcow_acme_staging` | `no` | if ACME staging should be used (s. https://mailcow.github.io/mailcow-dockerized-docs/firststeps-ssl/#test-against-staging-acme-directory) |
| https | `mailcow_additional_san` | `imap.*,smtp.*,autodiscover.*,autoconfig.*` | the additional domains (SSL Certificate Subject Alternative Names) |
| configuration | `mailcow_greylisting` | `true` | if greylisting should be active |

### DNS
If DNS entries should be managed, there has to be a role `dns` with the following parameters:

| parameter | description |
| ---| --- |
| `dns_zone_name` | the name of the zone (the domain) |
| `dns_record_name` | the name for the dns record (typically the subdomain) |
| `dns_record_type` | the type for the dns record |
| `dns_record_value` | the value for the dns record (typically the ipv4 address) |

| group | variable | default | description |
| --- | --- | ---| --- |
| DNS | `mailcow_domain` | | the mail domain for mailcow (there could be more than one, but this role supports creating a single one) |
| DNS | `mailcow_dns_mx` | `false` | if the MX record for `mailcow_domain` should be created |
| DNS | `mailcow_dns_autoconfig` | `false` | if the autoconfig record for `mailcow_domain` should be created |
| DNS | `mailcow_dns_autodiscover` | `false` | if the autodiscover records for `mailcow_domain` should be created |
| DNS | `mailcow_dns_spf` | `false` | if the SPF record for `mailcow_domain` should be created |
| DNS | `mailcow_dns_tlsa` | `false` | if the TLSA record for `mailcow_domain` should be created |
