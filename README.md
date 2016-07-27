Ansible role for supervisor
===========================

###This role is forked from: [https://github.com/zenoamaro/ansible-supervisord](https://github.com/zenoamaro/ansible-supervisord)

A role for deploying and configuring [Supervisor](http://supervisord.org) and extensions on unix hosts using [Ansible](http://www.ansibleworks.com).

* Install and manage [supervisor](http://supervisord.org)
* Install [superlance](http://superlance.readthedocs.org)
* Manage supervisor tasks, group, events
* Provide handlers for reload and restart supervisor


Supports
--------
Supported Supervisor versions:

* Supervisor 3+

Supported targets:

* Ubuntu 14.04 LTS "Trusty Tahr"
* Ubuntu 12.04 LTS "Precise Pangolin"
* Debian (untested)
* RedHat (untested)


Installation methods
--------------------
* Binary packages from the github repository (role name: ansible.supervisord)
* Ansible Galaxy: ansible-galaxy install lciolecki.supervisord (role name: lciolecki.supervisord) 
 
Recommended way installation is ansible galaxy.


Usage
-----

```yaml
---
- hosts: all

  roles:
    - lciolecki.supervisord

  vars:
  ....

```


Variables
---------

```yaml
---

supervisord_superlance: yes
supervisord_user: "www-data"

supervisord_inet_server: yes
supervisord_inet_address: 0.0.0.0
supervisord_inet_authenticated: yes
supervisord_inet_username: admin
supervisord_inet_password: "magicpassword"

supervisord_tasks:
  - name: ping
    type: program
    command: ping google.com
    autostart: false
    autorestart: false
    startretries: 3
  - name: crashmail
    type: eventlistener
    command: crashmail -a -m "example-email@gmail.com" -o "[Supervisord crashmail]"
    events: PROCESS_STATE_EXITED
  - name: test_group
    type: group
    programs: google
```


License
-------
The MIT License (MIT)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.