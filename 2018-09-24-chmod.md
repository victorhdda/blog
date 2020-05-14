---
title: CHMOD
date: 2018-09-24 19:14:27
tags:
- LINUX
- COMANDOS
- ARQUIVOS
- PERMISSÕES
---

A alteração de permissões de arquivos no linux pode ser efetuada de forma rápida com o comando `chmod`.

##### Sintaxe

`chmod [option] path/to/file `  
`chmod -R go-w path/to/folder`

#### Tipos de permissões
Um arquivo ou pasta podem receber permissões de leitura (read), escrita (write) ou execução (execute).

#### Grupos
Ao aplicar uma permisão é necessário especificar os grupos aos quais ela se aplica. Os possíveis grupos são: usuário (user), grupo (group) e outro (other).

Informações dos grupos e das permissões são exibidas ao executar o comando `ls -l`.
```sh
-rw-r--r--  1 user user    0 Sep 24 16:38 readme.txt
file -
user rw-
group r--
other r--
```
O primeiro campo diferencia ou não um diretório (d). Os próximos três campos determinam as permissões do usuário (user). Os três campos seguintes exibem as permissões do grupo do usuário (group) e os últimos campus as permissões do outros grupos (other). O grupo other se refere a qualquer outro usuário existente, inclusive acessos públicos.

#### Exemplos
1. Excluir permissão de escrita de um arquivo para " group" e "others":
```sh
$ chmod go-w readme.txt
```
2. Adicionar todas as permissões para um arquivo:
```sh
$ chmod ugo+rwx readme.txt
-rwxrwxrwx  1 user user    0 Sep 24 16:38 readme.txt
file -
user rwx
group rwx
other rwx
```
3. Adicionar todas as permissões para um diretório e seus arquivos:
```sh
$ chmod -R test ugo+rwx
drwxrwxrwx  2 user user 4096 Sep 24 16:53 test
directory d
user rwx
group rwx
other rwx
```


### References
- chmod: <https://www.linux.com/learn/how-manage-file-and-folder-permissions-linux> # <https://kb.iu.edu/d/abdb>
