![](https://cdn.rawgit.com/fabric8io/fabric8-devops/93ca9bc/grafana2/src/main/fabric8/icon.png) Ansible role: grafana
=====================

A Simple Ansible role to manage [grafana](https://grafana.com/), configure datasources [ well just [Prometheus](http://prometheus.io) ATM] and import dashboards.

Here's what it does:

 * Install grafana package and dependencies and start service
 * Update default password
 * Install grafana plugins
 * Configure Prometheus datasource
 * Import dashboards from the files directory into /var/lib/grafana/dsahboards

TODO / WIP (Pull request anyone ? ;)
------------------------------------
 * Add support of adding grafana dashboards via git

Role Variables
--------------

#### role flags:
* `grafana_configure: true` - if you want no configuration this is the option for you to set to `false`
* `grafana_prometehus: true` - configures grafana with a datasource named Prometheus as the default datasource.

#### Variables worth mentioning:

* `grafana_http_port: 3000`
* `grafana_admin_user: admin`
* `grafana_admin_password: admin123`

* Grafana plugins using `grafana-cli`:

        grafana_plugins:
          - grafana-clock-panel
          - grafana-simple-json-datasource
          - grafana-worldmap-panel
          - grafana-piechart-panel
          - digiapulssi-breadcrumb-panel
          - crate-datasource

In production I don't want people changing dashboards without going through Git ... hence this method seemed sufficient

* `grafana_dir_dashboards: /var/lib/grafana/dashboards`
* TODO move to git based population ...

#### Prometheus Integration:
* `grafana_prometehus: true`
* `grafana_prometehus_host: localhost`
* `grafana_prometehus_port: 9090`
* TODO: look at authentication

#### Grafana Database:

      grafana_database:
        type: sqlite3
        host: 127.0.0.1:3306
        name: grafana
        user: root
        password: ''
        path: grafana.db

TODO: Check other storage options

Example Playbook
----------------

    - hosts: centos,ubuntu
      roles:
        - shelleg.grafana


License
-------

[Apache 2](https://choosealicense.com/licenses/apache-2.0/)


Author Information
------------------

[Haggai Philip Zagury](http://www.tikalk.com/devops/haggai)
