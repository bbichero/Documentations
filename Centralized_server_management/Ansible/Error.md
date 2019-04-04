Errors
------

When executing task on Debian 8.9 host:
```
fatal: [task]: FAILED! => {"changed": false, "module_stderr": "Shared connection to 127.0.0.1 closed.\r\n", "module_stdout": "sudo: unable to resolve host debian\r\n\r\n\r\n/bin/sh: 1: /usr/bin/python: not found\r\n", "msg": "MODULE FAILURE\nSee stdout/stderr for the exact error", "rc": 127}
```
Ansible need `python` binary to execture task, but only `python3.5` is present.   
You need to execute pre-tasks on host, add this in the beguinning of your playbook:
```
gather_facts: false
pre_tasks:
  - name: Install python for Ansible
    raw: test -e /usr/bin/python || (apt -y update && apt install -y python-minimal)
    register: output
    changed_when: output.stdout != ""
    tags: always
  - setup: # aka gather_facts
```
