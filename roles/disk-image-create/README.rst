==============================
ansible-role-disk-image-create
==============================

Create a disk image using diskimage-builder's disk-image-create command.

Requirements
------------

The disk-image-create command must be in ansible's PATH. This can be done by
installing diskimage-builder via pip / git
(https://http://git.openstack.org/openstack/diskimage-builder) / package.


Role Variables
--------------

The available role variables and default values are:

.. code-block:: yaml

  dibcreate_destination: undefined
  dibcreate_elements: undefined
  dibcreate_env_vars: []
  dibcreate_extra_packages: []
  dibcreate_log_dest: /dev/null
  dibcreate_output_types: [ qcow2 ]
  dibcreate_overwrite_dest: False

The variables `dibcreate_destination` and `dibcreate_elements` are required.
