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
