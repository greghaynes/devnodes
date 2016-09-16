========
devnodes
========

Define libvirt vm's to satisfy an ansible inventory.

Example
=======

.. code-block:: bash

  cd devnodes
  ansible-playbook -K -i hosts site.yaml

This will define a devnodes-test instance due to a node named test in the
inventory and with the networking properties defined in host_vars/test.
