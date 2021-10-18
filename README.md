# Ansible Role mailcow

Install mailcow with [mailcow-dockerized]('https://github.com/mailcow/mailcow-dockerized.git')

## Collection dependencies

The role depends on the collection community.docker.
Note that this also requires installation of the python libraries `docker` and `docker-compose`.

## Role Variables

### `mailcow_install_path`: `/opt/mailcow-dockerized`

the install path for mailcow

### `mailcow_hostname`

the host name for mailcow

### `mailcow_timezone`: `Europe/Berlin`

the time zone for mailcow

### `mailcow_version`: `master`

the [version](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/git_module.html#parameter-version) to checkout

### `mailcow_docker_compose_project_name`: `mailcow_dockerized`

the name for the mailcow docker compose project

### `mailcow_docker_compose_state`: `present`

state for [community.docker.docker_compose](https://docs.ansible.com/ansible/latest/collections/community/docker/docker_compose_module.html)

### `mailcow_admin_user`

the username of the mailcow administrator

### `mailcow_admin_password`

the password for the mailcow administrator

### `mailcow_api_key`

API key for mailcow read-write access (allowed characters: a-z, A-Z, 0-9, -)

### `mailcow_api_key_read_only`

API key for mailcow read-only access (allowed characters: a-z, A-Z, 0-9, -)

### `mailcow_api_allow_from`

comma separated list of IPs to allow API access from

### `mailcow_acme_staging`: `no`

if ACME staging should be used (s. https://mailcow.github.io/mailcow-dockerized-docs/firststeps-ssl/#test-against-staging-acme-directory)

### `mailcow_delete_admin_script`: `/root/ansible_mailcow_delete_admin.sh`

the path for the mailcow delete admin script

### `mailcow_set_admin_script`: `/root/ansible_mailcow_set_admin.sh`

the path for the mailcow set admin script

### `mailcow_additional_san`: `imap.*,smtp.*,autodiscover.*,autoconfig.*`

the additional domains (SSL Certificate Subject Alternative Names)
