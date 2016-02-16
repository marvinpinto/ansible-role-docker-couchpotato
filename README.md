docker-couchpotato
==================

[![Build Status](https://img.shields.io/travis/marvinpinto/ansible-role-docker-couchpotato/master.svg?style=flat-square)](https://travis-ci.org/marvinpinto/ansible-role-docker-couchpotato)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-docker--couchpotato-blue.svg?style=flat-square)](https://galaxy.ansible.com/marvinpinto/docker-couchpotato)
[![License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.txt)

Ansible Galaxy role to manage and run a [couchpotato](https://couchpota.to)
docker container.

This role wires together the couchpotato [docker
container](https://hub.docker.com/r/linuxserver/couchpotato) created by
[linuxserver](https://github.com/linuxserver/docker-couchpotato), along with
various boilerplate to get things going.


Requirements
------------

This role has been tested on Ubuntu 14.04 and will likely only work on an
Ubuntu-like system. You will also need a functioning docker environment and a
recent-is version of `docker-py` for this role to work.

If you have neither and would like ansible to set this up for you, have a look
at the [marvinpinto.docker](https://galaxy.ansible.com/marvinpinto/docker)
Galaxy role.


Role Variables
--------------

```yaml
# Docker container name
docker_couchpotato_container_name: 'couchpotato'

# Couchpotato host port
docker_couchpotato_exposed_port: '5050'

# Directory that will be used as the root of all couchpotato-related
# configuration & data. Note that these sub-directories *will* be automatically
# created if they don't already exist.
#
# So, assuming 'docker_couchpotato_mounted_directory' is set to:
# /tmp/couchpotato_mount, the following directories will be created
# automatically:
#
# /tmp/couchpotato_mount/config
# /tmp/couchpotato_mount/raw_movie_downloads
# /tmp/couchpotato_mount/movies
docker_couchpotato_mounted_directory: '/tmp/couchpotato_mount'
```


Examples
--------

Install this module from Ansible Galaxy into the './roles' directory:
```bash
ansible-galaxy install marvinpinto.docker-couchpotato -p ./roles
```

Use it in a playbook as follows:
```yaml
- hosts: '127.0.0.1'
  roles:
    - role: 'marvinpinto.docker-couchpotato'
      become: true
```


Mounted Directory
-----------------

The reasoning behind storing all related configuration in the
`docker_couchpotato_mounted_directory` root directory is because a person now
has the ability to manage all the configuration + data outside of Ansible.

This becomes especially useful when said mounted directory resides on a
separate filesystem (EBS, USB disk, etc).
