*This project has been discontinued.*

## Install gitlab-ci-multi-runner and manage runners

This role can be used to install [gitlab-ci-multi-runner](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner) and manage runners (register and unregister them as requested).

[![Build Status](https://travis-ci.org/gtrafimenkov/ansible-role-gitlab-ci-multi-runner.svg)](http://travis-ci.org/gtrafimenkov/ansible-role-gitlab-ci-multi-runner)
[![Ansible Role](https://img.shields.io/badge/role-gtrafimenkov.gitlab--ci--multi--runner-blue.svg?maxAge=2592000)](https://galaxy.ansible.com/gtrafimenkov/gitlab-ci-multi-runner)

### Limitations

- runners' configuration cannot be changed after registration
- every runner should have a unique name even tough `gitlab-ci-multi-runner` allows to create multiple runners with the same name

### Usage

```
---
- hosts:
    - testhost
  become: yes
  vars:
    # concurent = 4
    gitlab_multirunner:
      runners:
        - name: runner21
          state: present
          ci_server: https://gitlab.example/ci
          token: uJLVTcWMrsuYzhBn9Y1N
          executor: shell
          env: 
            - "VAR1=value"
            - "VAR2=value"
          tags:
            - my1
            - my2
        - name: old-runner1
          state: absent
        - name: old-runner2
          state: absent
        - name: docker-runner1
          state: present
          ci_server: https://gitlab.example/ci
          token: uJLVTcWMrsuYzhBn9Y1N
          executor: docker
          docker_image: ubuntu:14.04
  roles:
    - gtrafimenkov.gitlab-ci-multi-runner
```

### Supported Platforms

The playbook was tested on following platforms:

- Debian 7
- Debian 8
- Ubuntu 12.04
- Ubuntu 14.04
- Ubuntu 16.04

### Supported Executors

`gitlab-ci-multi-runner` supports [multiple executors](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/tree/master/docs/executors), but these role supports only limited subset.

At the moment it is only:

- shell
- docker

### TODO

- add support for CentOS
- add integration tests
- support more executors
- make it possible to unregister existing runners

### Configuration options may change

Configuration options may change in the future releases in backward incompatible way.

### History

[changelog.md](/changelog.md)

### License

MIT
