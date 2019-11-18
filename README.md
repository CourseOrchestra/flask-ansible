Flask Ansible
=============
Роль для установки flask сервера

Variables
--------
```yaml
artifactory_root: artifactory.corchestra.ru/artifactory

artifactory_url: "https://{{ artifactory_user }}:{{ artifactory_pwd }}@{{ artifactory_root }}"

flask_app: manage

migrate: false
scheduler: false
static: false
worker: false
webapp: false

webapp_command: "gunicorn {{ flask_app }}:app -b 0.0.0.0:{{ flaskapp_port }}"
scheduler_command: flask run-scheduler
worker_command: flask run-worker
venv_lib: pyvenv
admin_part: yes  # установка пакетов, создание пользователя

```

Example Playbook
----------------
```yaml
---
- name: Gather facts for all hosts (if using --limit)
  hosts: all
  gather_facts: false
  tasks:
    - name: Gather facts
      setup:
        delegate_to: "{{item}}"
        delegate_facts: true
        with_items:
          - "{{ groups.all }}"

- hosts: flask
  gather_facts: false
  roles:
    - role: supervisor

- hosts: app
  gather_facts: false
  roles:
    - role: flask
  vars:
    webapp: true
    static: true

- hosts: worker
  gather_facts: false
  roles:
    - role: flask
  vars:
    worker: true
    scheduler: true
```