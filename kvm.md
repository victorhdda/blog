---
title: KVM
date: 2018-09-24 18:45:20
tags:
- KVM
- VIRTUALIZAÇÃO
- CLOUD
- SERVER
- LINUX
---

O KVM é um hypervisor que possibilita a criação de VM's de uma forma eficiente quanto a utilização do hardware.

---
### Instalação
1. Pacotes necessários para instalação do KVM e suas dependências:
```sh
$ sudo apt-get install qemu-kvm libvirt-bin ubuntu-vm-builder bridge-utils
```
2. Adicionando usuários aos grupos:
```sh
$ sudo adduser `id -un` libvirtd
```
* `id -un` representa o nome do usuário. Efetue um relogin para validar a alteração.

### Verificar a instalação:
```sh
$ virsh list --all
 Id    Name          State
---------------------------
```

### References

- KVM: <https://help.ubuntu.com/community/KVM/Installation> #
- MACVTAP: <https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/virtualization_administration_guide/sect-attch-nic-physdev> # <https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/virtualization_deployment_and_administration_guide/sect-virtual_networking-directly_attaching_to_physical_interface> # <https://seravo.fi/2012/virtualized-bridged-networking-with-macvtap> # <https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/virtualization_host_configuration_and_guest_installation_guide/app_macvtap>
