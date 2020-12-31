Role Name
=========

A role to install `Apache Zookeeper` cluster.

Requirements
------------

`Apache Zookeeper` requires `Java`. If java is installed on the host, specify it's location with `java_home` variable. Otherwise, The `chubock.java` role which is declared as a dependency for this role will try to install `Java` on the host. for more information about `chubock.java` visit [ansible-role-java](https://github.com/chubock/ansible-role-java).

Role Variables
--------------

The variable `nodeId` should be defined at host level and indicates the zookeeper instance id:

    [zookeeper]
    zk1.local nodeId=1
    zk2.local nodeId=2
    zk3.local nodeId=3

following variables are used for installing `Apache Zookeeper` on the host:

    java_home: /opt/java/default
    zookeeper_installation_path: /var/lib/zookeeper
    zookeeper_url: https://apache.mirror.digionline.de/zookeeper/zookeeper-3.6.2/apache-zookeeper-3.6.2-bin.tar.gz
    zookeeper_config_template: zoo.cfg.j2
    zookeeper_service_template: zookeeper.service.j2
    
following variables are used to configure `Apache Zookeeper`:

    tickTime: 2500
    dataDir: /data/zookeeper
    clientPort: 2181
    maxClientCnxns: 80
    admin:
      enableServer: true
      serverPort: 8080
    initLimit: 10
    syncLimit: 5
    hosts: "{{ groups['zookeeper'] }}"

Dependencies
------------

This role depends on `chubock.java` role for installing `Java`.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: zookeeper
      roles:
         - { role: chubock.zookeeper, java_home: /opt/java/default }

License
-------

Apache-2
