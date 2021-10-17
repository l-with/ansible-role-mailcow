# Ansible Role mailcow

Install mailcow with [mailcow-dockerized]('https://github.com/mailcow/mailcow-dockerized.git')

## Collection dependencies

The role depends on the collection community.docker.
Note that this also requires installation of the python libraries `docker` and `docker-compose`.

## Role Variables

### `mailcow_version`: `master`

the [version](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/git_module.html#parameter-version) to checkout

