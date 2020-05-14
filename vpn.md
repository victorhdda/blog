---
title: VPN
date: 2018-09-23 23:27:00
tags:
- VPN
- NETWORK
- FIREWALL
- SECURITY
- PRIVACY
---

Uma [VPN] (Virtual Private Network) é uma forma de acessar com segurança uma rede local, outro gateway de internet, servidores na intranet ou navegar de forma segura na internet.

### Acessando redes locais
Uma VPN permite acessar uma rede corporativa como se estivesse conectado localmente. Esse tipo de configuração é útil para situações em que um colaborador opera viajando muito e precisa acessar recursos da rede local de qualquer lugar. O que difere de uma VPN-Proxy é apenas a rede em que o usuário é alocado pelo servidor VPN. No primeiro caso, para permitir acesso aos serviços locais, o tunelamento realizado permite acesso a todas as rodas e serviços locais. No caso de uma VPN-Proxy o tunelamento é feito de forma a alocar o usuário em uma rede fechada e que possui acesso apenas para a internet.

### Navegando com segurança em redes públicas (VPN-Proxy)
Vários provedores de serviços oferecem conexões VPN com o objetivo de permitir ao usuário uma forma de burlar eventuais controles de conteúdos impostos em uma rede. Essas redes podem ser de um campus universitário, ambientes de trabalho ou hotspots públicos. ___A utilização dessas ferramentas para acessar conteúdos proibidos pelas políticas desses ambientes não é recomendada.___

Uma utilização coerente dessa ferramenta seria para a __navegação segura em ambientes públicos:__ Wi-Fi abertos, aeroportos, rodoviárias e outros mais. Esses ambientes são potenciais alvos de ataques virtuais, roubos de informações sensíveis e monitoramento de usuários.

Nesse caso, a utilização de uma VPN, que seja confiável, cria um canal de comunicação seguro através da internet. Esse canal é estabelecido entre o dispositivo e o servidor VPN. A comunicação que será enviada a um web site deixa de ser entregue pelo gateway local e passa a ser entregue pelo gateway da VPN. Esse processo faz com que o dispositivo esteja virtualmente na rede do servidor da VPN.

O caminho da comunicação:
O celular irá se comunicar com o web site. Após estabelecer uma conexão VPN com o gateway 2, os dados que ele envia irão sempre passar pelo gateway 1, criptografados, e chegarão ao gateway 2. O gateway 2, por sua vez, irá encaminhar os dados do celular para o web site. O gateway 2 também será responsável por receber as respostas do web site e encaminhá-las, criptografadas, para o gateway 1. O gateway 1 receberá esses dados e encaminhará de volta para o celular. Como os dados estão criptografados, o gateway 1, não terá como inspecionar ou analisá-los.

Esse tipo de comunicação aumenta a troca de mensagens e o delay de comunicação entre o celular e o site desejado. Isso se deve ao fato de que a informação transitará por uma terceira rede. Apesar do aumento do delay e redução do throughput, a utilização de uma VPN __impede que terceiros acessem os dados e até os metadados__ de uma comunicação, pois todo o tráfego é encapsulado e criptografado entre o cliente e o servidor VPN.

![Figura 1: Exemplo de comunicação de um celular para um web site através de uma VPN.](/images/01-vpn.png)


### Protocolos
Existem vários protocolos que realizam essa comunicação fim a fim. Cada um possui suas especificidades. Os mais utilizados são:
- [OpenVPN] Protocolo open source que é mais utilizado para prover conexões VPN a clientes, seja para acessar a rede local de uma organização ou para proteger uma conexão, quando em redes públicas.

- [IPsec]: Mais utilizado para conexões entre firewalls para prover uma conexão segura site to site.

### Instalação no linux
Um serviço de VPN como o OpenVPN exporta um pacote de certificados e configurações que pode ser importado de forma simplificada pelo usuário em seus dispositivos. Isso economiza tempo ao evitar uma configuração passo a passo de todos os itens de segurança.
Para estações que estejam rodando o Gnome o seguinte pacote pode ser instalado:
```sh
$ sudo apt-get install network-manager-openvpn-gnome
```
Após instalado basta acessar o gerenciado de conexões e importar o arquivo de configuração fornecido pelo servidor OpenVPN.


### Instalação no android
No android o processo é parecido, porém o aplicativo que importa as configurações e as aplica é o OpenVPN Connect – Fast & Safe SSL VPN Client. Após instalá-lo é só importar o arquivo de configuração e inserir as informações de usuário e senha.

### Bloqueios
Alguns tipos de bloqueios podem impedir que a conexão com o servidor VPN seja estabelecida. O que mais impacta é quando existe uma restrição de comunicação pela __porta 1194__. Quando uma rede local impede que seus clientes efetuem comunicações para esta porta(porta padrão na maioria dos servidores OpenVPN), o tunelamento não é estabelecido e a comunicação não flui. Uma alternativa para contornar essa situação é ter servidores que permitam configurar outras portas de conexão.

Outro tipo de bloqueio que ocorre é quando uma rede bloqueia acesso web (portas 80/443) a serviços de VPN ou direcionamento de tráfego. Nesse caso o bloqueio é por inspeção de pacotes e ele ocorre antes que o tunelamento seja estabelecido. O objetivo desse bloqueio é não permitir que os usuário pesquisem formas de burlar as regras do firewall.

### Serviços de VPN
Exemplo de serviços de VPN-Proxy:
- [ProtonVPN]
- [SuperFreeVPN]
- [BetterNet]

### References
- VPN: <https://9to5mac.com/guides/vpn/> # https://www.vpnmentor.com/blog/top-really-free-vpn-services/
- OpenVPN: <https://openvpn.net/index.php/open-source/333-what-is-openvpn.html>
- IPsec:<https://en.wikipedia.org/wiki/IPsec> #  <https://www.netgate.com/docs/pfsense/vpn/ipsec/configuring-a-site-to-site-ipsec-vpn.html>
- ProtonVPN: <https://protonvpn.com/>
- SuperFreeVPN: <http://superfreevpn.com/>
- BetterNet: <https://www.betternet.co>
- Tunneling: <https://wiki.linuxfoundation.org/networking/tunneling>

[//]: # (--- Hiperlinks)
[VPN]: <https://9to5mac.com/guides/vpn/>
[OpenVPN]: <https://openvpn.net/index.php/open-source/333-what-is-openvpn.html>
[IPsec]: <https://www.netgate.com/docs/pfsense/vpn/ipsec/configuring-a-site-to-site-ipsec-vpn.html>
[ProtonVPN]: <https://protonvpn.com/>
[SuperFreeVPN]: <http://superfreevpn.com/>
[BetterNet]: <https://www.betternet.co>
