Development environment
-----------------------

This environment has been designed to help you to modify IRMA's components and
redeploy and test them. In this setup, everything is installed in a single
virtual machine with sources rsync-ed between the host and the guest.

Requirements
````````````

- `Vagrant <http://www.vagrantup.com/>`_ 1.8 or higher has to be installed
- As the installation work only for `Virtualbox <https://www.virtualbox.org/>`_,
  you will need to install it
- `Rsync <https://rsync.samba.org/>`_ to synchronize directories from host to VMs
- Read the `Ansible introduction <http://docs.ansible.com/intro.html>`_


Run Vagrant and create your VMs
```````````````````````````````

To initialize and provision the Virtualbox VM.

.. code-block:: bash

    $ cd <IRMA_SRC_DIR>/ansible
    $ VM_ENV=your_environment_name vagrant up

The template will be downloaded automatically and configured using ``environments/dev.yml`` file.


.. NOTE::

    Optionally, if you want to use your own environment, create it in
    ``environments`` directory and run:

    .. code-block:: bash

        $ VM_ENV=your_environment_name vagrant up

Configure your .ini files
`````````````````````````

.. NOTE::

    You can bypass this step, as this provisioning is sync with default username
    and password used in (frontend|brain|probe) config files.

As your ``config/*.ini`` file are transferred from host to VMs, you will need
to modify them individually in the ``frontend``, ``probe`` and
``brain`` directories to match the user and password defined in
``playbooks/group_vars/*``.


Modify your host and open IRMA frontend
```````````````````````````````````````

Then, for proper use, update your `/etc/hosts` file and add:

.. code-block:: bash

	172.16.1.30    www.frontend.irma

Then, with your web browser, IRMA allinone is available at
`www.frontend.irma <http://www.frontend.irma>`_.

Sync files between host and guest
`````````````````````````````````

Once rsync is installed inside your virtual machine and your environment is correctly set. You could easily sync your code with:

.. code-block:: bash

    $ vagrant rsync # or vagrant rsync-auto to automatically initiates an rsync
                    # transfer when changes are detected

Then, reload the modified application.

