# Ansible Role mailcow

Install mailcow with [mailcow-dockerized]('https://github.com/mailcow/mailcow-dockerized.git')

## Collection dependencies

The role depends on the collection community.docker.
Note that this also requires installation of the python libraries `docker` and `docker-compose`.

## Role Variables

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
