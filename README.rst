========
devnodes
========

Define libvirt vm's to satisfy an ansible inventory.

What does it do?
================

The site.yaml play creates a diskimage using diskimage-builder. Then, for each
node in the inventory, a vm is defined with a disk copy of that image. The
properties of each vm are specified using ``devnodes`` vars from each host
(see vars for more info). 


Example
=======

.. code-block:: bash

  cd devnodes
  ansible-playbook -K -i hosts site.yaml

This will define a devnodes-test instance due to a node named test in the
inventory and with the networking properties defined in host_vars/test.

vars
====

The following vars can be specified in the ``devnodes`` dict.

cpus
----

The number of CPUs to make available to the vm.

links
-----

A list of link dictionaries which are passed directly to the config-drive
network_data.json.

memory
------

The amount of ram (in MB) to make available to the vm.

networks
--------

A list of network dictionaries which are passed directly to the config-drive
network_data.json.

public_keys
-----------

A dict of name to public ssh keys which are specified in the vm config-drive.
Glean is added to the vm's causing these keys to be added to the root user
on boot.

Typical Usage
=============

A typical usage pattern defines a user's ssh key in a separate vars file
(ssh-key.yaml):

.. code-block:: yaml

  devnodes:
    public_keys:
      greghaynes: <ssh-key>

The properties for a node are defined in the node's host_vars (host_vars/test):

.. code-block:: yaml

  devnodes:
    cpus: 1
    memory: 512
    links:
      - id: eth0
        ethernet_mac_address: 52:54:00:8e:d3:dc
        mtu: 1500
        type: phy
      - id: eth1
        ethernet_mac_address: 52:54:00:f8:a8:81
        mtu: 1500
        type: phy
    networks:
      - id: network0
        type: ipv4
        netmask: 255.255.255.0
        link: eth0
        routes:
           - netmask: 0.0.0.0
             network: 0.0.0.0
             gateway: 10.10.0.1
        ip_address: 10.10.0.101

Then to delete any existing devnode vm's and create new ones run site.yaml
with the inventory, host_vars, and ssh key vars file included:

.. code-block:: bash

  ansible-playbook -K -i hosts -e@ssh-key.yaml site.yaml
