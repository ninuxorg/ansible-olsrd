Ansible compile OLSR v.1 for Debian Jessie
=================================

Clonare con::

    git clone git@github.com:ninuxorg/ansible-olsrd.git
    git clone https://github.com:ninuxorg/ansible-olsrd.git


Roles Variables
```yaml
# interfaces OLSRd will bind to
olsrd_interfaces:
    - eth0

olsrd_build_dependencies:
    - subversion-tools
    - subversion
    - debhelper
    - bison
    - flex
    - pkg-config
    - libgtk2.0-dev
    - python-gtk2-dev
    - liblua50-dev
    - cmake
    - libgps-dev
    - build-essential
    - libnl-3-dev
    - git
    - libnl-genl-3-dev
    - libnl-utils
    - pkg-config
    - doxygen
    - devscripts
    - dh-systemd

olsrd_dir: "/opt/olsrd"
olsrd_source_repo: https://github.com/OLSR/olsrd.git
olsrd_source_dir: "{{ olsrd_dir }}/source"
olsrd_source_version: HEAD  # master
olsrd_git_email: "git@{{ ansible_domain }}"
olsrd_git_name: "{{ ansible_user }}"
svn_debian_repo: svn://svn.debian.org/svn/collab-maint/deb-maint/olsrd/trunk/debian
```


Esempio Playbook
---------------------
```yaml
- hosts: myserver
  roles:
    - ninux.olsrd
  vars:
    olsrd2_interfaces:
      - eth0
```
