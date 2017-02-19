Ansible compile OLSR v.1 for Debian Jessie
=================================

Clonare con::

    git clone git@github.com:ninuxorg/ansible-olsrd.git
    git clone https://github.com:ninuxorg/ansible-olsrd.git


Roles
-----

Il Playbook contiene le seguenti roles:

- common
  This role contain all the common package/ configuration and utils needed by ANY system (by nemesisdesign)

- olsrd-v1
  Compilazione e installazione di OLSR v1



Inventory
---------

::

	# file: hosts

	[name/group servers]
	olsr.basilicata.nnxx	ansible_user=michele	ansible_port:2400
	10.27.0.120             ansible_user=michele	ansible_port:2400



Defining playbooks
------------------


::

    # file: test.yml

    - hosts: olsr-role
      become: "{{ sudo | default('yes') }}"
      roles:
        - common
        - olsrd-v1
      vars:
        # common
        common_ipv4_forward: 1
        common_ssh_port: 2400
        # variabili per ruolo common
      users:
        - name: michele
          authorized:
            - ./keys/michele.pub
        # oslr
        olsrd_interfaces:
          - eth0




Every role has a directory where tasks, templates, handlers and variables are defined. For more informations see https://docs.ansible.com/index.html

Gotta deploy 'em all!
---------------------

Install ansible on Debian Jessie:

::

  $ sudo apt-get install software-properties-common
  $ sudo echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" >> /etc/apt/sources.list
  $ sudo apt-get update
  $ sudo apt-get install ansible

Deploy of a new server:

::

  ansible-playbook -i hosts test.yml -ku <user> -e "sudo=no" -l <server-host-name>
