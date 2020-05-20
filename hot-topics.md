Implementações
- NMAP que varre a rede para verificar conectividade, escaneia alguns hosts ou redes, retorna relatórios de sucesso/falha


Uso simplificado do GIT
- https://www.youtube.com/watch?v=2alg7MQ6_sI
- https://www.youtube.com/watch?v=UbJLOn1PAKw
- https://medium.com/@tordable/github-pages-as-blogging-platform-320524b1fffa

Uso do cron
- https://crontab.guru/#*_*_*_*_*
- https://opensource.com/article/17/11/how-use-cron-linux

Shell script
- https://www.cyberciti.biz/faq/unix-linux-iterate-over-a-variable-range-of-numbers-in-bash/
- http://faculty.salina.k-state.edu/tim/unix_sg/shell/variables.html

Funcionalidades do Latex

Usos do Google Cloud (wordpress e templates)

Orientações básicas sobre cabeamento estruturado (normas para ambientes acadêmicos)

IFMG4.0

Como funciona um serviço de DNS

Programas iniciais para uma instalação linux
- Alterar visudo user ALL=(ALL) NOPASSWD:ALL
- Nmap
- Iperf3
- git
- htop
- aptitude
- screen
- dnsutils
- ethtool
- registar data e hora no histórico do terminar: echo 'export HISTTIMEFORMAT="%d/%m/%y %T "' >> ~/.bash_profile
- ansible
- speedtest-cli
- software-properties-common
- curl
- rename
- crontab
- prips
- 7zip
- unattended-upgrades apt-listchanges: https://wiki.debian.org/UnattendedUpgrades
- zabbix (config:  vim /etc/zabbix/zabbix_agentd.conf (Server=IP address of Zabbix Server)  (Hostname=Hostname of client PC) (systemctl restart zabbix-agent) (systemctl enable zabbix-agent) (systemctl status zabbix-agent)
- vnstat: vnstat -l -i eth0
- bash-completion: https://www.howtoforge.com/how-to-add-bash-completion-in-debian
- docker : https://docs.docker.com/engine/install/debian/#installation-methods (debian)
- 
- ~~parallel (descrever funcionalidade)~~ - criar um scaner baseado em parallel

Conversões de vídeo, qual codec e resoluçes usar, bem como programas e comandos.

Tratar imagens RAW minimamente com soluções open source

sudo timedatectl set-timezone 'America/Sao_Paulo'


Funcionamento traccar

Falar sobre programação de shell script e argoritmos com ele

Algum banco de dados

Wordpress como blog/página web/CMS


Comandos


sudo aptitude install nmap iperf3 git htop screen dnsutils ethtool ansible speedtest-cli prips vnstat speedometer bash-completion software-properties-common curl bash-completion aptitude wget

sudo apt-get install     apt-transport-https     ca-certificates     curl     gnupg-agent     software-properties-common
sudo timedatectl set-timezone 'America/Sao_Paulo'

sudo nano /etc/rsyslog.d/90-google.conf 
  148  17/05/20 22:13:38 sudo nano /etc/rsyslog.conf 
  149  17/05/20 22:14:05 sudo service rsyslog restart


sudo apt-get install unattended-upgrades apt-listchanges

sudo nano /etc/apt/apt.conf.d/20auto-upgrades 


echo 'export HISTTIMEFORMAT="%d/%m/%y %T "' >> ~/.bashrc



References

https://www.cyberciti.biz/faq/howto-set-date-time-from-linux-command-prompt/

https://www.networkinghowtos.com/howto/adding-persistent-static-routes-on-ubuntu-18-04-and-higher-using-netplan/

https://cloudcone.com/docs/how-to-install-zabbix-agent-on-centos-7-and-ubuntu-18-04/

https://www.binarytides.com/linux-commands-monitor-network/

https://blog.stackpath.com/glossary-cwnd-and-rwnd/

http://blog.evaldojunior.com.br/aulas/blog/shell%20script/2011/05/08/shell-script-parte-2-controle-de-fluxo.html

~~https://www.gnu.org/software/parallel/parallel_tutorial.html#Controlling-the-output~~

~~https://www.gnu.org/software/bash/manual/html_node/GNU-Parallel.html~~

~~https://www.msi.umn.edu/support/faq/how-can-i-use-gnu-parallel-run-lot-commands-parallel~~

https://www.shellhacks.com/tune-command-line-history-bash/










-------


# Instalação jitsi
 PARA SER OPEN TEM QUE SER ACESSÍVEL.

URL: https://jitsi.github.io/handbook/docs/devops-guide/devops-guide-quickstart

Hardware: google cloud

setar dns registro.br 

meet.vhtel.eng.br - 34.66.27.251)

sudo hostnamectl set-hostname meet.vhtel.eng.br


sudo apt-get install ufw

Regras


80 TCP - for SSL certificate verification / renewal with Let's Encrypt
443 TCP - for general access to Jitsi Meet
4443 TCP - for fallback network video/audio communications (when UDP is blocked for example)
10000 UDP - for general network video/audio communications
22 TCP - if you access you server using SSH (change the port accordingly if it's not 22)



sudo ufw status verbose


Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
80/tcp                     ALLOW IN    Anywhere                  
443/tcp                    ALLOW IN    Anywhere                  
4443/tcp                   ALLOW IN    Anywhere                  
10000/udp                  ALLOW IN    Anywhere                  
22/tcp                     ALLOW IN    Anywhere                  
80/tcp (v6)                ALLOW IN    Anywhere (v6)             
443/tcp (v6)               ALLOW IN    Anywhere (v6)             
4443/tcp (v6)              ALLOW IN    Anywhere (v6)             
10000/udp (v6)             ALLOW IN    Anywhere (v6)             
22/tcp (v6)                ALLOW IN    Anywhere (v6)       



configurar rotas de nat no google cloud: atenção para as tags que devem ser adicionadas à vm e à regras para devida efetivação


Instalar jitsi

sudo apt install jitsi-meet

Instalar certificados ssl

sudo /usr/share/jitsi-meet/scripts/install-letsencrypt-cert.sh


configurar logs e alertas da vm no gcloud


manter arquivo de configuração das instância do google cloud - git privado ?


Alerta de cpu

stress para stressar a máquina
https://superuser.com/questions/443406/how-can-i-produce-high-cpu-load-on-a-linux-server




---------












