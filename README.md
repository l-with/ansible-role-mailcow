# Ansible Role mailcow

Install mailcow with [mailcow-dockerized]('https://github.com/mailcow/mailcow-dockerized.git')

## Collection dependencies

The role depends on the

- ansible role dns

## Role Variables

<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD034 -->
| group | variable | default | description |
| --- | --- | --- | --- |
| basic | `mailcow_install` | `true` | if mailcow should be installed |
| basic | `mailcow_configure` | `true` | if mailcow should be configured |
| basic | `mailcow_start` | `true` | if mailcow should be started |
| basic | `mailcow_hostname` | | the host name for mailcow |
| basic | `mailcow_install_path` | `/opt/mailcow-dockerized` | the install path for mailcow |
| basic | `mailcow_timezone` | `Europe/Berlin` | the time zone value for mailcow  (`MAILCOW_TZ`) |
| basic | `mailcow_branch` | `master` | the branch value for mailcow (`MAILCOW_BRANCH`) |
| basic | `mailcow_version` | `{{ mailcow_branch }}` | the [version](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/git_module.html#parameter-version) to checkout |
| basic | `mailcow_docker_compose_project_name` | `mailcowdockerized` | the name for the mailcow docker compose project |
| basic | `mailcow_docker_compose_state` | `present` | state for [community.docker.docker_compose](https://docs.ansible.com/ansible/latest/collections/community/docker/docker_compose_module.html) |
| security | `mailcow_admin_user` | | the username of the mailcow administrator |
| security | `mailcow_admin_password` | | the password for the mailcow administrator |
| security | `mailcow_dovecot_master_auto_generated` | `true` | if the dovecot master user and password should be auto-generated |
| security | `mailcow_dovecot_master_user` | | the username of the dovecot master user (DOVECOT_MASTER_USER) if not auto-generated |
| security | `mailcow_dovecot_master_password` | | the password for the dovecot master user (DOVECOT_MASTER_PASS) if not auto-generated |
| security | `mailcow_api_key` | | the API key for mailcow read-write access (allowed characters: a-z, A-Z, 0-9, -) |
| security | `mailcow_api_key_read_only` | | the API key for mailcow read-only access (allowed characters: a-z, A-Z, 0-9, -) |
| security | `mailcow_api_allow_from` | | list of IPs to allow API access from |
| security | `mailcow_db_password` | | the password for the mailcow database for user 'mailcow' |
| security | `mailcow_db_root_password` | | the password for the mailcow database for the root user |
| security | `mailcow_rspamd_ui_password` | | the password for the mailcow Rspamd UI |
| security | `mailcow_delete_default_admin_script` | `/root/ansible_mailcow_delete_default_admin.sh` | the path for the mailcow delete default admin script |
| security | `mailcow_set_admin_script` | `/root/ansible_mailcow_set_admin.sh` | the path for the mailcow set admin script |
| security | `mailcow_set_rspamd_ui_password_script` | `/root/ansible_set_rspamd_ui_password.sh` | the path for the mailcow set Rspamd UI password script |
| https | `mailcow_acme` | `out-of-the-box` | the way the Let's Encrypt certificate ist obtained: <br/> `out-the-box`:  The "acme-mailcow" container will try to obtain a LE certificate. <br/> `certbot`: The certbot cronjob will manage Let's Encrypt certificates |
| https | `mailcow_acme_staging` | `no` | if ACME staging should be used (s. https://mailcow.github.io/mailcow-dockerized-docs/firststeps-ssl/#test-against-staging-acme-directory) |
| https | `mailcow_additional_san` | `imap.*,smtp.*,autodiscover.*,autoconfig.*` | the additional domains (SSL Certificate Subject Alternative Names) |
| https | `mailcow_certbot_deploy_hook_script_full_path` | `/root/ansible_mailcow_certbot_deploy_hook.sh` | the certbot deploy-hook script |
| configuration | `mailcow_submission_port` | `587` | the SUBMISSION_PORT in mailcow.conf |
| configuration | `mailcow_greylisting` | `true` | if greylisting should be active |
| configuration | `mailcow_mynetworks` | `` | list of subnetwork masks to add to `mynetworks` in postfix <br /> if subnetwork masks are provided at the beginning `127.0.0.0/8 [::ffff:127.0.0.0]/104 [::1]/128 [fe80::]/10` is added (local) |
| configuration | `mailcow_rspamd_ip_whitelist` | `[]` | the list of ip adresses to be added to rspamd ip whitelist |
| configuration | `mailcow_accept_wildcard_alias` | `false` | if a postfix virtual_alias_maps rule should be added accepting all mails matching `<prefix>.<alias-suffix>@<domain>` if an alias `<prefix>._wilcard_@<domain>` is present |
| configuration | `mailcow_add_wildcard_alias` | `false` | if a postfix virtual_alias_maps rule should be added accepting all mails matching `<prefix>.<alias-suffix>@<domain>` if an alias `<prefix>._wilcard_@<domain>` is present and adding the address as alias in mailcow (needs also `mailcow_add_wildcard_alias` to be `true`) |
| oauth2 | `mailcow_configure_oauth2` | `false` | if oauth2 should be configured |
| oauth2 | `mailcow_oauth2_client_redirect_uri` | | the redirect uri for the mailcow oauth2 app |
| oauth2 | `mailcow_oauth2_client_scope` | `profile` | the scope for the mailcow oauth2 app |
| backup | `mailcow_configure_backup` | `false` | if backup of the mailcow should be configured for unattended backup |
| backup | `mailcow_path` | `/opt/mailcow` | the mailcow path for the backup artifacts (scripts) |
| backup | `mailcow_backup_path` | `/var/backups/mailcow` | the path for the mailcow backup |
| backup | `mailcow_backup_scripts_path` | `"{{ mailcow_path }}/scripts"` |
| backup | `mailcow_backup_script_name` | `mailcow-backup.sh` | the name of the mailcow backup script |
| backup | `mailcow_restore_script_name` | `mailcow-restore.sh` | the name of the mailcow restore script |
| backup | `mailcow_backup_script` | `"{{ mailcow_backup_scripts_path }}/{{ mailcow_backup_script_name }}"` | the mailcow backup script |
| backup | `mailcow_restore_script` | `"{{ mailcow_backup_scripts_path }}/{{ mailcow_restore_script_name }}"` | the mailcow restore script |
| cold-standby | `mailcow_cold_standby` | `false` | if a mailcow cold-standby host should be synchronized |
| cold-standby | `mailcow_cold_standby_host` | | the mailcow cold-standby host |
| cold-standby | `mailcow_cold_standby_ssh_private_key` | | the private ssh key for accessing the cold-standby host |
| cold-standby | `mailcow_cold_standby_schedule` | `true` | if the synchronize with the mailcow cold-standby host should be scheduled |
| cold-standby | `mailcow_cold_standby_schedule_user` | `root` | the cron schedule user for synchronizing |
| cold-standby | `mailcow_cold_standby_schedule_hour` | `"*"` | the cron schedule hour for synchronizing |
| cold-standby | `mailcow_cold_standby_schedule_minute` | `"42"` | the cron schedule minute for synchronizing |
| cold-standby | `mailcow_cold_standby_schedule_day` | `"*"` | the cron schedule day for synchronizing |
| cold-standby | `mailcow_cold_standby_schedule_weekday` | `"*"` | the cron schedule weekday for synchronizing |
| cold-standby | `mailcow_cold_standby_schedule_month` | `"*"` | the cron schedule month for synchronizing |

<!-- markdownlint-enable MD033 -->
<!-- markdownlint-enable MD034 -->

- The security variables need `mailcow_start`.
- The `mailcow_acme` variant `certbot` needs a LE certificate installed (build with DNS challenge) and `mailcow_start`.

### Domain and DNS

If DNS entries should be managed, there has to be a role `dns` with the following parameters:

| parameter | description |
| ---| --- |
| `dns_zone_name` | the name of the zone (the domain) |
| `dns_record_name` | the name for the dns record (typically the subdomain) |
| `dns_record_type` | the type for the dns record |
| `dns_record_value` | the value for the dns record (typically the ipv4 address) |

<!-- markdownlint-disable MD033 -->
| group | variable | default | description |
| --- | --- | --- | --- |
| domain/DNS | `mailcow_domain` | | the mail domain for mailcow (there could be more than one, but this role supports creating a single one) |
| domain | `mailcow_domain_description` | `mailcow_domain` | the description in mailcow for the `mailcow_domain` |
| domain | `mailcow_domain_max_aliases` | 400 | the maximum number of aliases for the `mailcow_domain` |
| domain | `mailcow_domain_max_mailboxes` | 20 | the maximum number of aliases for the `mailcow_domain` |
| domain | `mailcow_domain_default_mailbox_quota` | 2048 | the default mailbox quota for the `mailcow_domain` |
| domain | `mailcow_domain_max_mailbox_quota` | 4096 | the maximum for mailbox quota for the `mailcow_domain` |
| domain | `mailcow_domain_quota` | 40960 | the quota for the `mailcow_domain` |
| DNS | `mailcow_dns_do` | `true` | if the role should create the dns records with role `dns` (s. above) or only create the output variable `mailcow_dns_records` |
| DNS | `mailcow_dns` | `true` | defines the default for `mailcow_dns_*`, <br /> for creating DNS entries a defined `mailcow_domain` is required |
| DNS | `mailcow_dns_mx` | `true` | if the MX record for `mailcow_domain` should be created |
| DNS | `mailcow_dns_autoconfig` | `true` | if the autoconfig record for `mailcow_domain` should be created |
| DNS | `mailcow_dns_autodiscover` | `true` | if the autodiscover records for `mailcow_domain` should be created |
| DNS | `mailcow_dns_spf` | `true` | if the SPF record for `mailcow_domain` should be created |
| DNS | `mailcow_dns_tlsa` | `true` | if the TLSA record for `mailcow_domain` should be created |
| DNS | `mailcow_dns_dkim` | `true` | if the DKIM record for `mailcow_domain` should be created |
| DNS | `mailcow_dns_debug` | `false` | if debug information should be printed |
<!-- markdownlint-enable MD033 -->

### Output

| group | variable | description |
| --- | --- | --- |
| backup | `mailcow_path` | the mailcow path for the backup artifacts (scripts) |
| backup | `mailcow_backup_path` | the path for the mailcow backup |
| backup | `mailcow_backup_script` | the mailcow backup script |
| backup | `mailcow_restore_script` | the mailcow restore script |
| DNS | `mailcow_dns_records` | list of dns records (dict `dns_record`) |
| DNS | `mailcow_dns_record_TLSA` | the TLSA dns record |
| DNS | `mailcow_dns_record_DKIM` | the DKIM dns record |

| dict | element | default | description |
| --- | --- | --- | --- |
| `dns_record` | `zone_name` | | the name of the zone (the domain) |
| `dns_record` | `name` | | the name for the dns record (typically the subdomain) |
| `dns_record` | `type` | | the type for the dns record |
| `dns_record` | `value` | | the value for the dns record (typically the ipv4 address) |
