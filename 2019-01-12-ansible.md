---
title: Ansible
date: 2018-09-19 21:27:22
tags:
- LINUX
- COMANDOS
- SERVER
- CLOUD
---

O [Ansible] é uma aplicação que automatiza a execução de tarefas em múltiplas máquinas virtuais (VM's). Essa automatização permite configurar ambientes grandes e complexos de TI evitando possíveis falhas de execução ou digitação humana.

# Instalação
##### Host de controle
Para instalação do Ansible as seguintes configurações são necessárias no host de controle.

```sh
sudo apt-get update
sudo apt-get install software-properties-common
sudo apt-get install python-software-properties
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible
sudo apt-get install aptitude
sudo apt-get install python-apt
sudo apt-get install python3-apt
```

##### Hosts clientes
* É necessário instalar os pacotes do python em todos os hots clientes, os demais pacotes listados são adicionais aos comandos que serão utilizados.
* É necessário que o host de controle já possua acesso aos nós clientes, de preferência com troca de [chaves criptográficas SSH] entre eles.

```sh
sudo apt-get update
sudo apt-get install software-properties-common
sudo apt-get install python-software-properties
sudo apt-get install aptitude
sudo apt-get install python-apt
sudo apt-get install python3-apt
```
##### Comandos ansible

```sh
ansible -m command -a "hostname" all
ansible -m ping all
```

## Ambiente de controle

É recomendável ter um host de controle dentro do ambiente a ser monitorado. Dessa forma o acesso externo é feito a este host que controla os demais hosts "clientes" desejados.

## Playbooks

São instruções de comandos a serem executados pelo host de controle nos clientes. Essas instruções são estruturadas em um arquivo .yml.

### Módulos

São comandos pré-definidos são inseridos nos playbooks e que executam tarefas nos clientes. Tarefas comuns como envio de arquivos, atualização e instalação de pacotes podem ser feitos por módulos já existentes.

#### apt
Módulo de configuração de aplicações do Ansible.

# Comandos úteis no linux:

* Gerar chave privada e pública para o acesso SSH. _'-t rsa'_ para utilizar a versão 2 do algoritmo rsa.

``
$ ssh-keygen -t rsa
``


* Instalar chave criptográfica para acesso via SSH

``
$ ssh-copy-id user@ip_host_client
``




* Acesso SSH com transmissão de ambiente gráfico X11.

``
$ ssh -Y user@192.168.0.1
``

* O rsync permite a sincronização de arquivos e pastas de forma rápida entre uma fonte e um destino. O seguinte comando é utilizado para sincronização da pasta Blog no PC com um servidor na nuvem.

```sh
$ rsync -avz --no-perms --rsync-path='sudo rsync' /home/user/Blog/source/_posts/ server.com.br:/home/user/Blog/source/_posts/
```


* Configuração de IP estática no linux. Editar o arquivo /etc/network/interfaces

```sh
auto eth0
iface eth0 inet static
name Ethernet LAN card
address 192.168.0.1
netmask 255.255.255.0
broadcast 192.168.0.255
network 192.168.0.0
gateway 192.168.0.1
dns-nameservers 8.8.8.8 8.8.4.4
```



# References
* Ansible: <https://docs.ansible.com/>
* Chaves SSH: <https://www.vivaolinux.com.br/dica/Configurando-SSH-sem-senha-no-Ubuntu-ssh-copy-id> # <https://www.hardware.com.br/tutoriais/dominando-ssh/pagina5.hhtml>
* Markdown: <https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf>
* Rsync: <https://www.tecmint.com/rsync-local-remote-file-synchronization-commands/> # <http://www.f15ijp.com/2010/09/executing-rsync-as-sudo/>



[Ansible]: <https://docs.ansible.com/>
[chaves criptográficas SSH]: <https://www.vivaolinux.com.br/dica/Configurando-SSH-sem-senha-no-Ubuntu-ssh-copy-id>
