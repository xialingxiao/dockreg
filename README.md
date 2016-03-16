DockReg (Ansible Orchestrated Docker Registry 2.0)
================================================================================
###### Copyright (c) 2016 Lingxiao Xia
###### Creation: Lingxiao Xia
###### Creation Date: 2016-03-16

This package creates a tls enabled and password protected `Docker` registry using the image `registry:2`. 

This generates its own CA and provisions the destination hosts to trust the CA.

A few steps to take before running the playbook:
1. Please open the inventory files [staging](staging) and modify the staging destinations according to your setup.
2. Please install `ansible 2.0.0.2` and its dependencies.
3. Run `ansible-vault create vars/common_vars_vault` and add the following variables for passwords:
    * `vault_ca_pass`
    * `vault_registry_pass`
4. Please install `docker 1.10.0` and its dependencies.

To generate the CA, start the registry and login to the registry from all destination hosts:
```
ansible-playbook -i staging --ask-vault-pass -K run.yaml
```

To stop and remove the registry at staging environment:
```
ansible-playbook -i staging --ask-vault-pass stop.yaml
```

To clean up all generated contents at staging environment:
```
ansible-playbook -i staging --ask-vault-pass -K clean.yaml
```