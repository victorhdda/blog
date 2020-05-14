---
title: Hexo e ferramentas de texto
date: 2018-09-19 19:07:40
tags:
- HEXO
- BLOG
- LINUX
- SERVER
- DOCKER
- CLOUD
- GOOGLE
---

## Hexo - Blog
O [Hexo](http://hexo.io) é uma plataforma de blog pessoal open source que utiliza textos em [markdown](https://daringfireball.net/projects/markdown/>) para gerar páginas HTML. Ele mostra ser uma plataforma leve e prática de ser utilizada, principalmente se for associada a [contêineres Docker](https://github.com/davyyy/docker-hexo). Aproveitando essa  facilidade foi criado um contêiner para hospedar o conteúdo que se deseja publicar em uma VM no [Google Cloud](https://cloud.google.com).

## Docker
O Docker foi utilizado nesse projeto para subir e manter o contêiner operacional na VM. O contêiner foi configurado para iniciar junto com a inicialização da VM. O redirecionamento de porta foi feito para a porta 4000, ou seja, toda comunicação que chegar na porta 4000 da VM será direcionada para o contêiner. Foi estudado também a execução de comandos do Docker utilizando o Pipe "|". O mesmo se mostrou poderoso para associar a execução de comandos bash a uma lista de elementos que são exibidos no terminal. O [vídeo](https://www.youtube.com/watch?v=EuzOw7M15vg) demonstrou a execução de Streams, Redirects e Piping.

{% youtube EuzOw7M15vg %}


#### Criar um contêiner com hexo-server instalado
```sh
$ sudo docker run --restart=always --name=hexo-server -d -p 4000:4000 -v /home/username/Blog:/blog  davyyy/hexo server
```
### Criação de novos posts no hexo-server
```sh
$ sudo docker run --rm --volumes-from hexo-server davyyy/hexo new nome_do_post
```

### Outros comandos Docker
```sh
$ sudo docker ps -aq # Listar contêineres  abertos
$ sudo docker ps -aq | sudo xargs docker rm # Excluir todos contêineres
$ sudo docker images # Listar images disponíveis
$ sudo docker images -aq | sudo xargs docker rmi # Excluir todas images não associadas a contêineres
```

## Google Cloud
Na plataforma do GCloud foi necessário criar uma regra para abertura da porta 4000 e direcionamento dela para VM. O tutorial a seguir foi utilizado: <https://www.youtube.com/watch?v=JmjqPpQdtW8>

{% youtube JmjqPpQdtW8 %}

## Atividades a desenvolver
* Rodar webserver via docker
* Substituir página principal por Hexo estático ?
* Implementar compilador latex no hexo

# References
* [Hexo] <https://hexo.io/>
* [Hexo - contêiner] <https://github.com/davyyy/docker-hexo>
* [Markdown] <https://dillinger.io/> <https://stackedit.io/> # <https://daringfireball.net/projects/markdown/>
* [Diagramas] <https://mermaidjs.github.io/>
* [Docker] <https://docs.docker.com/install/linux/docker-ce/ubuntu/#upgrade-docker-ce> # <https://zaiste.net/removing_docker_containers/> # <https://serverfault.com/questions/633067/how-do-i-auto-start-docker-containers-at-system-boot> # <https://docs.docker.com/engine/reference/commandline/container_ls/>
* [Bash pipe, stream, redirect: xargs] - <https://www.youtube.com/watch?v=EuzOw7M15vg>
* [GCLOUD] <https://www.youtube.com/watch?v=JmjqPpQdtW8> # <https://cloud.google.com/load-balancing/docs/forwarding-rules>
