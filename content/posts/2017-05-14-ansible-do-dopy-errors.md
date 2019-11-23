---
title: "Ansible: Misleading dopy errors"
date: 2017-05-14T19:33:25.000Z
feature_image: https://images.unsplash.com/photo-1503252947848-7338d3f92f31?ixlib=rb-0.3.5&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=1080&fit=max&ixid=eyJhcHBfaWQiOjExNzczfQ&s=01ac2b385a2b44489d14e52a26d15022
tags:
  - linux
  - tech
  - automation
  - en
---

[Ansible](https://www.ansible.com/) works pretty well with [DigitalOcean](https://www.digitalocean.com/), and where it is not, it is mostly the fault of [dopy](https://pypi.python.org/pypi/dopy), not DigitalOcean’s or Ansible’s. I am using macOS and out of convenience I installed Ansible via [Homebrew](https://brew.sh/). When trying certain actions, for example destroying a Droplet, I got this error message:

`dopy >= 0.2.3 required for this module`

This was weird, as I was sure I had installed dopy via pip (and pip via Homebrew). After double-checking and some digging I found the issue to be with the Ansible installation. To fix the issue at hand, one can [either](https://groups.google.com/forum/?hl=ru#!topic/ansible-project/gjQM-rArtTg) add

`localhost ansible_connection=local ansible_python_interpreter=python`

to the hosts file, [or](https://github.com/ansible/ansible-modules-core/issues/360) run `/usr/local/Cellar/ansible/2.3.0.0_2/libexec/bin/pip install dopy==0.3.7a`.
