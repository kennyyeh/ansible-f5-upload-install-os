# ansible-f5-upload-install-os

I was asked to upgarde 40+ f5 devices in AWS, so i thought it would be best to automate the entire procoess using a simple ansible playbook. 

* Inventory list of all the f5s i needed to upgrade (active and standby) .. because we need the code on all the versions.

to execute install
```
ansible-playbook -i inventory/hosts install-os.yaml
```

to verify
```
nsible-playbook -i inventory/hosts verify-install.yaml
```

The playbook perfoms the following actions
* saves the existing configurations
* uploads the latest OS
* installs it on a new partition
* prints out an output of when its complete

## install-os.yaml
* uploads, installs and verifies the install

## install-os-boot.yaml
* uploads, installs, verifies the install and copies the configuration from boot location HD1.1 (BIG-IP 15.1.0) to boot location HD1.3 (BIG-IP 16.0.0) and immediately reboot the system to the HD1.3 boot location:

cpcfg --source=HD1.1 --reboot HD1.3

On a VIPRION system, ensure each blade receives the updated configuration by running the cpcfg command with the clsh utility on the primary blade.

For example:

clsh cpcfg --source=HD1.1 --reboot HD1.3
