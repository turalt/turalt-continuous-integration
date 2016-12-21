## Turalt continuous integration platform

This is a public mirror of the Turalt continuous integration platform. We
actually run this on a Raspberry Pi 3 in the office.

### Before you deploy:

Set up your Raspberry Pi using Raspbian, and make sure you can ssh to it over
the network. We use ssh keys for logging in, so use a `.ssh/config` file entry
to enable ssh to the device as root. Our `.ssh/config` file contains this, for
example:

    Host raspberry
      RSAAuthentication yes
      Hostname 10.0.1.203
      IdentityFile /Users/stuart/raspberry_rsa
      User root

There are also a bunch of settings under `vars/secure_vars` which specify
the server address and so on. We usually keep these encrypted using
Ansible Vault, with the password in a `.vault-password` file blocked from
version control.

### To deploy:

    ansible-playbook -v -i inventory.ini deploy.yml

Then you can connect to the server at:

    http://10.0.1.203:3000

### Adding projects

You can add projects to the list in the variable `project_list`, and for
each one, under `roles/projects/files` create a named YAML file. We've
included one example (which is private, so it won't work as it stands).
This file tells NCI what to do with that project,
in terms of how to manage the build, where to get the code from, how often
to check for updates, and so on.
