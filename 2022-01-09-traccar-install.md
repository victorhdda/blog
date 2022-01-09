---
title: Instalação Traccar na AWS
date: 2022-01-09 20:00:00
tags:
- TRACCAR
- AWS
- LINUX
- SERVER
- CLOUD
---

# Instalação Traccar na AWS

O Traccar pode ser instalado com um banco interno, H2 de "baixo desempenho", com um banco de dados na mesma instância (MySQL) ou utilizando um banco externo.

Para a primeira etapa desta instalação será utilizado o banco interno, dando preferência para conectar a um banco externo (AWS RDS) quando a instância estiver em produção.

1. Criar a instância na AWS em um subnet pública, 8 GB de HD são suficientes. Adicionar regras de Security Groups para as portas 22, 80, 443, 8082 (porta de acesso inicial do servidor java) e para as portas de recebimento dos dados de telemetria 5000 à 5150 (TCP e UDP).

2. Baixar e descompactar os arquivos de instalação do sistema:
```
sudo yum update -y
sudo yum install htop
wget https://www.traccar.org/download/traccar-linux-64-latest.zip
unzip traccar-linux-*.zip
```

3. Executar o arquivo de instalação como sudo: `sudo ./traccar.run`

<details>
<summary markdown="span">4. Configuração do banco de dados: </summary>

1. Caso deixe a configuração padrão, para uso do banco de dados imbutido (H2), a seguinte configuração será mantida no arquivo de configuração: /opt/traccar/conf/traccar.xml
  ```
  <entry key='database.driver'>com.mysql.jdbc.Driver</entry>
  <entry key='database.url'>jdbc:mysql://localhost/traccardb?serverTimezone=UTC&amp;useSSL=false&amp;allowMultiQueries=true&amp;autoReconnect=true&amp;useUnicode=yes&amp;characterEncoding=UTF-8&amp;sessionVariables=sql_mode=''</entry>
  <entry key='database.user'>root</entry>
  <entry key='database.password'>root</entry>
  ```

2.  Caso altere a opção padrão de banco de dados e crie um banco de dados MySQL, o arquivo /opt/traccar/conf/traccar.xml deve ser alterado, seguindo o modelo:

  ```
  cat > /opt/traccar/conf/traccar.xml << EOF
  <?xml version='1.0' encoding='UTF-8'?>

  <!DOCTYPE properties SYSTEM 'http://java.sun.com/dtd/properties.dtd'>

  <properties>

      <entry key="config.default">./conf/default.xml</entry>

      <entry key='database.driver'>com.mysql.jdbc.Driver</entry>
      <entry key='database.url'>jdbc:mysql://localhost/traccardb?serverTimezone=UTC&amp;useSSL=false&amp;allowMultiQueries=true&amp;autoReconnect=true&amp;useUnicode=yes&amp;characterEncoding=UTF-8&amp;sessionVariables=sql_mode=''</entry>
      <entry key='database.user'>root</entry>
      <entry key='database.password'>root</entry>

  </properties>
  EOF

  ```

</details>



5. Iniciar o serviço Traccar: `sudo service traccar start`

6. Testar acesso web pela porta 8082: http://ip-do-servidor:8082

7. Realizar login com a credencial padrão (admin/admin), desativar o auto-registro de usuários e alterar a senha padrão.


Na segunda estapa desta instalação será configurado o acesso ao site pelo nome de domínio, através da porta 443 (ssl/tls) e instalação de um certificado.











<details>
<summary markdown="span">8. Configurações do Apache e do certificado SSL</summary>

Traccar serves web interface and API using regular HTTP protocol which does not use any encryption. This guide provides instructions on how to configure Traccar to use secure HTTPS protocol with SSL/TLS encryption of all traffic [Traccar Secure Connection]. Examples are for Ubuntu and other Debian-based systems only, but the general idea can be applied to all platforms. For Windows system you can follow this blog post from Freek.

Traccar does not support secure connection out of the box, but a proxy server can be used to tunnel all data through secure protocol. In this guide we will use Apache server with proxy module.


<details>
<summary markdown="span">1. First step is to install Apache server and enable required modules:</summary>



```
sudo apt-get install ssl-cert apache2
sudo a2enmod ssl
sudo a2enmod proxy_http
sudo a2enmod proxy_wstunnel
sudo service apache2 restart
```
</details>


<details>
<summary markdown="span">2. As a next step we need to add new site configuration:</summary>


`sudo nano /etc/apache2/sites-available/traccar.conf`
Content for the site configuration (replace "demo.traccar.org" with your domain):

```
<IfModule mod_ssl.c>
        <VirtualHost _default_:443>

                ServerName demo.traccar.org
                ServerAdmin webmaster@localhost

                DocumentRoot /var/www/html

                ProxyPass /api/socket ws://localhost:8082/api/socket
                ProxyPassReverse /api/socket ws://localhost:8082/api/socket

                ProxyPass / http://localhost:8082/
                ProxyPassReverse / http://localhost:8082/

                SSLEngine on
                SSLCertificateFile /etc/ssl/certs/ssl-cert-snakeoil.pem
                SSLCertificateKeyFile /etc/ssl/private/ssl-cert-snakeoil.key

        </VirtualHost>
</IfModule>
```

</details>

<details>
<summary markdown="span">3. Enable site and restart Apache service:</summary>

```
sudo a2ensite traccar
sudo service apache2 restart
```

</details>

<details>
<summary markdown="span">4. Domain Name:</summary>
You need to have a domain name. Check our documentation on how register and to configure a custom domain name with Traccar.
</details>


<details>
<summary markdown="span">5. Generate an SSL certificate for your server using Let’s Encrypt service :</summary>

[Lets encrypt certbot]: Install certbot:
```
sudo snap install --classic certbot
```
Execute Certbot:
```
sudo certbot --apache
```
</details>

<details>
<summary markdown="span">6. Traccar in subdirectory (non root path) - OPTIONAL:</summary>

If you want Traccar to be in a subdirectory, you also need to adjust cookies path. Here is a proxy configuration example:

```
ProxyRequests off

ProxyPass /gps/api/socket ws://localhost:8082/api/socket
ProxyPassReverse /gps/api/socket ws://localhost:8082/api/socket

ProxyPass /gps/ http://localhost:8082/
ProxyPassReverse /gps/ http://localhost:8082/
ProxyPassReverseCookiePath / /gps/

Redirect permanent /gps /gps/
```
</details>

<details>
<summary markdown="span">7. Redirect unsecure connections HTTP to HTTPS:</summary>

```
sudo a2enmod rewrite
sudo a2dissite 000-default
sudo nano /etc/apache2/sites-available/traccar.conf
```

Add following lines to the configuration:

```
<VirtualHost *:80>
  ServerName demo.traccar.org
  Redirect / https://demo.traccar.org/
</VirtualHost>
```

Restart Apache server:

```
sudo service apache2 restart
```


</details>
</details>








9. Configurar no Registrar o encaminhamento do nome de subdomínio desejado para o IP/CNAME da instância EC2. Caso seja utilizado um Elastic IP, este deve receber o apontamento do subdomínio desejado.



<details>
<summary markdown="span">10. Configurações adicionais:</summary>


 Podem ser feitos mais alguns ajustes, a fim de garantir mais algumas restrições de segurança e funcionalidades para o serviço:
* Firewall UFW: Instalar, habilitar e liberar as portas de acesso ao servidor: 5000-5150 (UDP/TCP), 80+443 (TCP), 22 (TCP) caso o servidor ainda precise ser configurado remotamente.
* No momento em que o servidor já esteja em produção não é necessário mais manter liberação de acesso à porta 22, com isso evita-se alguns escaneamentos de bots.
* Caso a porta 22 deva ser mantida aberta, utilize a aplicação fail2ban como método adicional de segurança.

</details>

# Referências
* Traccar Instalation Guide: https://www.traccar.org/install-digitalocean/

* Traccar Secure Connection: https://www.traccar.org/secure-connection/

* SSL on AWS: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/SSL-on-amazon-linux-2.html

* Let's Encrypt Certbot: https://certbot.eff.org/instructions?ws=apache&os=ubuntufocal



<!--- Identifiers -->

[Traccar Secure Connection]: https://www.traccar.org/secure-connection/
[Lets encrypt certbot]: https://certbot.eff.org/instructions?ws=apache&os=ubuntufocal












<!--

Hardening?? fechar porta do AIM com firewall?? iptalbles?

-->
