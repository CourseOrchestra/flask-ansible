Flask
=========

Установка и настройка flask приложения


Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

#### Variables

```yaml

python_version: 3.7.17

flaskapp_name: flask

flask_root_dir: /opt/api
flask_log_dir: /var/log/{{ flaskapp_name }}

flask_user: flask

flaskapp_port: 5000
workers_num: 4

virtualenv: virtualenv

sources_url: https://github.com/sdhutchins/flask-demo.git
checkout_style: git

flask_environment:
  FLASK_CONFIG: production
  APP_PORT: "{{ flaskapp_port }}"
  FLASK_APP: run

webapp_command: "/bin/bash -c 'source venv/bin/activate && gunicorn {{ flask_environment.FLASK_APP }} -b 0.0.0.0:{{ flaskapp_port }} --limit-request-line 0 --timeout 600 --workers {{ workers_num }}'"

flask_db_migrate: false


```

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml

  - hosts: app
    roles:
      - role: CourseIT.flask
        vars:
          flask_db_migrate: true
  - hosts: worker
    roles:
      - role: CourseIT.flask
        vars:
          flask_db_migrate: false

```
