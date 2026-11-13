
ETAPA 0 - Preparação
---
- Conferir o sistema - comando: cat /etc/os-release

<img width="508" height="292" alt="image" src="https://github.com/user-attachments/assets/e87c1d23-62a3-40dc-9517-a5de9e3fe473" />

- Confere mémoria - comando: free -h  

<img width="687" height="76" alt="image" src="https://github.com/user-attachments/assets/1a46f2b5-46b1-4c54-8f81-119c945803e2" />

- Conferir o disco - comando: df -h  

<img width="538" height="203" alt="image" src="https://github.com/user-attachments/assets/255df413-1566-4fc6-92e3-f2441028115c" />

- Conferir a CPU - comando: nproc 

<img width="323" height="46" alt="image" src="https://github.com/user-attachments/assets/e1f39610-ee07-4872-9a03-0092c6616d6a" />

- Atualizar o sistema operacional - comando: sudo dnf update -y

<img width="644" height="57" alt="image" src="https://github.com/user-attachments/assets/7bb2d861-8e79-4221-90b0-7ebda05791c7" />
<img width="362" height="65" alt="image" src="https://github.com/user-attachments/assets/b420188c-7ec6-4553-bbc8-599f4d99ec0e" />

- Instalar utilitários essenciais do sistema - comando: sudo dnf install -y unzip tar vim-enhanced curl wget tree nmap-ncat

<img width="721" height="205" alt="image" src="https://github.com/user-attachments/assets/0ace2835-6d12-4d69-97aa-337e5907e6b6" />

- Verificar a instalação - comando: which unzip vim tree nc wget

<img width="424" height="113" alt="image" src="https://github.com/user-attachments/assets/b7f1781f-aaa6-476d-90d4-64dbff43f1da" />

SElinux
---
- verificar o estado atual de funcionamento do SELinux - comando: getenforce

<img width="268" height="55" alt="image" src="https://github.com/user-attachments/assets/f5af212e-08ef-4977-91cb-b0e8cc706649" />

- verificar o estado atual - comando: getsebool httpd_can_network_connect httpd_can_network_memcache httpd_execmem httpd_can_connect_ldap httpd_use_nfs httpd_can_network_connect_db

<img width="1312" height="116" alt="image" src="https://github.com/user-attachments/assets/db964b96-1a1d-4176-8af4-b84ba98c0b95" />

Como estava tudo off, realizado a ativação de cada um com o comando: sudo setsebool -P httpd
<img width="586" height="100" alt="image" src="https://github.com/user-attachments/assets/b5c5b30a-3e25-4d5d-8fc6-7b4cd5e82681" />

- verificar o estado atual - comando: getsebool httpd_can_network_connect httpd_can_network_memcache httpd_execmem httpd_can_connect_ldap httpd_use_nfs httpd_can_network_connect_db

Agora todos ativos: <img width="1306" height="113" alt="image" src="https://github.com/user-attachments/assets/5465bb4f-ee70-4e6b-a791-50ed40b40980" />

---

Manual

- Entrar no manual - comando: cd /opt/sei-lab
- Verificar o manual - comando: grep -n '^#' "INSTALACAO 4.0.12.15.md"
<img width="1010" height="864" alt="image" src="https://github.com/user-attachments/assets/562bc6f1-20ef-43b5-a492-a8f6b213083a" />

- Ler o manual - comando: less "INSTALACAO 4.0.12.15.md"
<img width="1670" height="857" alt="image" src="https://github.com/user-attachments/assets/9e46f024-842c-4366-a6df-33e01dafcb57" />


---
ETAPA 1 - SEI
---

- Ver o conteudo do pacote sem extrair - comando: unzip -l /opt/sei-lab/sei-4.0.12.15.zip

  <img width="558" height="188" alt="image" src="https://github.com/user-attachments/assets/2682fb4f-7e74-4a05-9705-c8de40025c43" />

- Criar diretorio - comando: mkdir -p ~/sei-pacote
  
  <img width="392" height="22" alt="image" src="https://github.com/user-attachments/assets/c15e88d5-4f90-44a4-9ad7-7fa264b5d082" />
  
- Extrair o documento para o diretorio - comando: unzip -q /opt/sei-lab/sei-4.0.12.15.zip -d ~/sei-pacote
  
<img width="683" height="30" alt="image" src="https://github.com/user-attachments/assets/82432f40-053b-417b-964c-4f013a77934f" />

- Listar os arquivos no diretorio - comando: ls ~/sei-pacote
  <img width="1052" height="41" alt="image" src="https://github.com/user-attachments/assets/71bd5777-b39a-4226-8380-e0db9d8b49cb" />

- Extraindo as fontes - comando: unzip -q ~/sei-pacote/sei-Fontes-4.0.12.15.zip -d ~/sei-pacote/fontes
- Extraindo o banco de dados - comando: unzip -q ~/sei-pacote/sei-Fontes-4.0.12.15.zip -d ~/sei-pacote/fontes

<img width="820" height="37" alt="image" src="https://github.com/user-attachments/assets/2ba653e1-29c1-40b8-a17c-3af8dc3aa4c3" />

- Listar os arquivos - comando: ls ~/sei-pacote/fontes ~/sei-pacote/bd

<img width="519" height="105" alt="image" src="https://github.com/user-attachments/assets/b52ef5b3-d7e7-4541-9820-809fbdfb5165" />

- Copiar para o /opt - comando: sudo cp -r ~/sei-pacote/fontes/sei ~/sei-pacote/fontes/sip ~/sei-pacote/fontes/infra /opt/

<img width="948" height="21" alt="image" src="https://github.com/user-attachments/assets/a820fa18-6b7d-4c05-93b8-66c6ee7ba2c5" />

- Criar diretorio sip/bin - comando: sudo mkdir -p /opt/sip/bin
- Listar os arquivos no diretorio - comando: ls /opt/sei /opt/sip /opt/infra

<img width="474" height="170" alt="image" src="https://github.com/user-attachments/assets/0124e5f5-c543-4037-bdcb-632a0d194394" />

---

---

ETAPA 2 - Apache
---

- Instalar o Apache - comando: sudo dnf install -y httpd

<img width="544" height="27" alt="image" src="https://github.com/user-attachments/assets/e845a2ae-9c2a-4c7f-be25-2ea724e5ec73" />

- Ligar o Apache  e garantir que ele continuará ligando sozinho - comando: sudo systemctl enable --now httpd

<img width="936" height="41" alt="image" src="https://github.com/user-attachments/assets/5d3e1b29-9900-4d9f-8eea-51e522f26482" />

- Verificar o status do Apache - comando: systemctl status httpd

<img width="860" height="295" alt="image" src="https://github.com/user-attachments/assets/2e825926-5eb4-49c5-a946-fd33b1ab6ee5" />

- Testar http padrão - comando: curl -I http://localhost

<img width="490" height="145" alt="image" src="https://github.com/user-attachments/assets/0a6b0711-93d9-40b8-95ea-12c31366d02b" />

---

ETAPA 3 - Php 

---

- Instalar php 7.3 - comando: dnf module list php

<img width="383" height="28" alt="image" src="https://github.com/user-attachments/assets/5f3ce6b1-c59b-4c31-bbcf-4e48da6c212a" />

- Habilitar o modulo do php - comando: sudo dnf module enable php:7.3 -y

<img width="1676" height="213" alt="image" src="https://github.com/user-attachments/assets/12bab2c6-03f5-423d-8b74-f3ec84649786" />

- Instalar pacotes do php - comando: sudo dnf install -y php-cli php-fpm

<img width="1674" height="753" alt="image" src="https://github.com/user-attachments/assets/febc12bd-2d86-442c-91cb-067c752097b6" />

- Verificar a versão do php - comando: php -v

<img width="522" height="67" alt="image" src="https://github.com/user-attachments/assets/27580d57-2e9c-4985-b927-326271ccbe37" />

- Verificar o que está carregado no php - comando: php -m

<img width="391" height="458" alt="image" src="https://github.com/user-attachments/assets/30c84407-9589-42e6-ad4d-c3bd1d330698" />

- Verificar quais existem no repositorio - comando: dnf list available "php-*"

<img width="1673" height="510" alt="image" src="https://github.com/user-attachments/assets/e7f0bd40-61e3-478f-ad9c-46f54bd8189a" />

- Instalar extensões que faltam - comando: sudo dnf install -y php-mysqlnd php-json php-xml php-soap php-mbstring php-intl php-gd php-pecl-zip php-bcmath php-ldap

<img width="1183" height="39" alt="image" src="https://github.com/user-attachments/assets/c824d080-7dbc-43ee-aa1f-a1099c5c871d" />

- Verificar o que está carregado no php - comando: php -m

<img width="349" height="774" alt="image" src="https://github.com/user-attachments/assets/aa5d2f1f-04ad-443a-8242-a0f69eb18b97" />

- Verificar pacotes de desenvolvimento e compilação do PHP - comando: sudo dnf install -y php-devel php-pear gcc make zlib-devel

<img width="682" height="34" alt="image" src="https://github.com/user-attachments/assets/1c2f26e3-9ec0-41c2-aa5b-1b6360d010df" />


- Verificar a versão atual do gerenciador de pacotes - comando: pecl version

<img width="975" height="88" alt="image" src="https://github.com/user-attachments/assets/e49e96c5-2d83-4d05-a082-d1b34dc7147f" />

- Compilar o memcache - comando: sudo pecl install memcache-4.0.5.2

<img width="478" height="24" alt="image" src="https://github.com/user-attachments/assets/ef9cab80-3a7c-49a1-a914-f95b80b7afcb" />

- Compilar o igbinary - comando: sudo pecl install igbinary

<img width="390" height="30" alt="image" src="https://github.com/user-attachments/assets/913243e6-74f1-462c-8a4d-ea18102e80d0" />

- Ativar o igbinary e o memcache - comandos: echo "extension=igbinary.so" | sudo tee /etc/php.d/30-igbinary.ini ; echo "extension=memcache.so" | sudo tee /etc/php.d/40-memcache.ini

<img width="699" height="67" alt="image" src="https://github.com/user-attachments/assets/9e0fa7e3-6274-429a-aeba-ebf602e117d8" />

Ajuste no Php 
-> Criar um arquivo próprio com os valores da seção 2 do manual - comando: sudo vim /etc/php.d/99-sei.ini

<img width="615" height="205" alt="image" src="https://github.com/user-attachments/assets/98d700cb-396f-42ce-bb19-c839ca026362" />

O Apache executa o PHP pelo php-fpm 

- Habilitar no boot - comando: sudo systemctl enable php-fpm
- Iniciar - comando: sudo systemctl restart php-fpm
- Verificar status - comando: systemctl status php-fpm

<img width="959" height="323" alt="image" src="https://github.com/user-attachments/assets/a650ee08-9a1a-4208-9134-4f0c1cd3f688" />

Como o php-fpm foi instalado depois que o Apache já estava rodando, precisa reiniciar o Apache e testar o PHP

- Reiniciar o apache - comando: sudo systemctl restart httpd

<img width="393" height="21" alt="image" src="https://github.com/user-attachments/assets/03895e37-f361-4990-98b8-0d14f023f606" />

- Criar arquivo de teste do PHP - comando: echo "<?php phpinfo();" | sudo tee /var/www/html/teste.php 

<img width="634" height="37" alt="image" src="https://github.com/user-attachments/assets/b26984bd-d618-4983-978c-d025f073a3da" />

- Verificar configuração específica no arquivo de teste - comando: curl -s http://localhost/teste.php | grep short_open_tag
- Verificar suporte a uma extensão específica - comando: curl -s http://localhost/teste.php | grep "memcache support"
- Remover o arquivo de teste do servidor  - comando: sudo rm /var/www/html/teste.php
- Verificar os cabeçalhos HTTP da página  - comando: curl -I http://localhost/teste.php

<img width="688" height="204" alt="image" src="https://github.com/user-attachments/assets/234d2433-e61f-49a1-9c6a-d288dbc3bcbd" />

---

ETAPA 4 - Memcached 

---
- Instalar o serviço Memcached - comando: sudo dnf install -y memcached
  
<img width="502" height="34" alt="image" src="https://github.com/user-attachments/assets/ba3b2715-281d-4fde-baaf-3b8887a371c9" />

- Exibir o arquivo de configuração do Memcached - comando: cat /etc/sysconfig/memcached

<img width="405" height="100" alt="image" src="https://github.com/user-attachments/assets/c15a7928-f80e-47a0-aa30-76eb4dbd52a7" />

- Habilitar e iniciar o serviço Memcached - comando: sudo systemctl enable --now memcached

<img width="981" height="49" alt="image" src="https://github.com/user-attachments/assets/9a9fae22-dce8-43bd-afce-9bbbeaab0f2a" />

- Consultar estatísticas do Memcached - comando: printf "stats\nquit\n" | nc 127.0.0.1 11211 | head -5

<img width="622" height="108" alt="image" src="https://github.com/user-attachments/assets/10296525-5a15-4331-bdcd-dda4a6e83009" />


---

ETAPA 5 - Banco de dados - MySQL 8.0

---

- Listar módulos disponíveis para o MySQL - comando: dnf module list mysql

<img width="1357" height="133" alt="image" src="https://github.com/user-attachments/assets/b225ccf0-5cc8-446e-969c-3baee827030a" />

- Habilitar a versão 8.0 do MySQL - comando: sudo dnf module enable mysql:8.0 -y

<img width="1669" height="201" alt="image" src="https://github.com/user-attachments/assets/88c56b1d-87da-4b34-9847-4e6ab756aea3" />

- Instalar o  MySQL - comando: sudo dnf install -y mysql-server

<img width="635" height="32" alt="image" src="https://github.com/user-attachments/assets/da3a7b54-bf8b-4839-89b2-1a81738fb259" />

- Verificar a versão do MySQL - comando: mysql --version

<img width="478" height="35" alt="image" src="https://github.com/user-attachments/assets/1d4834bd-cb1e-4c85-a7ac-f9474d958abd" />

- Habilitar e iniciar o serviço MySQL - comando: sudo systemctl enable --now mysqld

<img width="936" height="43" alt="image" src="https://github.com/user-attachments/assets/13b3a729-4967-4904-a02e-5b5450d8bbf6" />

- Verificar o status do MySQL - comando: systemctl status mysqld

<img width="912" height="262" alt="image" src="https://github.com/user-attachments/assets/d380a390-a9eb-4033-9fcd-55c0c015161e" />

- Executar o script de segurança do MySQL - comando: sudo mysql_secure_installation

<img width="455" height="86" alt="image" src="https://github.com/user-attachments/assets/a7356c24-6293-4784-9532-f5e266f55143" />

-> Conjunto de caracteres latin1

- Exibir o arquivo principal de configuração do MySQL - comando: cat /etc/my.cnf

<img width="485" height="179" alt="image" src="https://github.com/user-attachments/assets/6a3a3e4f-b6ca-40d7-b096-42dd516f3e93" />

- Listar o diretório de configurações adicionais do MySQL - comando: ls /etc/my.cnf.d

<img width="578" height="49" alt="image" src="https://github.com/user-attachments/assets/2bd5520e-ccb9-4191-a409-c02844020fdd" />

- Exibir o arquivo de configuração do plugin de autenticação padrão - comando: cat /etc/my.cnf.d/mysql-default-authentication-plugin.cnf

<img width="931" height="205" alt="image" src="https://github.com/user-attachments/assets/e5748808-ae95-429c-abb6-355dbb113430" />

- Criar o arquivo de configuração do MySQL - comando: sudo vim /etc/my.cnf.d/99-sei.cnf

<img width="477" height="140" alt="image" src="https://github.com/user-attachments/assets/1c6c72d3-21ef-40d1-94ab-38eeae36ebff" />

- Reiniciar o  MySQL - comando: sudo systemctl restart mysqld

<img width="407" height="27" alt="image" src="https://github.com/user-attachments/assets/4e6d4470-2086-4ff1-a77e-db8e064379d7" />

- Consultar as variáveis de codificação de caracteres do MySQL - comando: mysql -u root -p -e "SHOW VARIABLES LIKE 'character_set%';"

<img width="652" height="230" alt="image" src="https://github.com/user-attachments/assets/75fd0dca-64ac-4ef2-a9ad-b502eeef0e44" />

- Entrar no banco - comando: mysql -u root -p

<img width="303" height="36" alt="image" src="https://github.com/user-attachments/assets/27e20ba5-2d6c-47c1-976c-8f6abe016b67" />

- Criar os bancos de dados sei e sip: comando: CREATE DATABASE sei CHARACTER SET latin1 COLLATE latin1_swedish_ci;    ; CREATE DATABASE sip CHARACTER SET latin1 COLLATE latin1_swedish_ci;
<img width="629" height="97" alt="image" src="https://github.com/user-attachments/assets/634c7357-bc38-4f44-8260-f9156dbd62c2" />

- Criar o usuário - comando: CREATE USER 'sei_user'@'localhost' IDENTIFIED BY 'senha';

<img width="603" height="41" alt="image" src="https://github.com/user-attachments/assets/05c819a3-9457-45d7-893b-663f3b6228e4" />

- Conceder as permissões pro sei - comando: GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER, LOCK TABLES, REFERENCES ON sei.* TO 'sei_user'@'localhost';
- Conceder as permissões pro sip - comando: GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER, LOCK TABLES, REFERENCES ON sip.* TO 'sei_user'@'localhost';

<img width="1063" height="94" alt="image" src="https://github.com/user-attachments/assets/730e88e5-5af6-4249-ad2b-3dd502439e52" />

- Importar o arquivo de referência do sip e sei para o banco de dados - comando: mysql -u root -p sip < ~/sei-pacote/bd/sip_4.0.x.1_BD_Ref_Exec.sql ;  mysql -u root -p sei < ~/sei-pacote/bd/sei_4.0.x.1_BD_Ref_Exec.sql
<img width="707" height="65" alt="image" src="https://github.com/user-attachments/assets/df49736e-3d75-4169-b8c2-1def8305ea02" />

- Consultar a quantidade de tabelas no banco de dados Sip e sei- comando: mysql -u root -p -e "SELECT COUNT(*) FROM information_schema.tables WHERE table_schema='sip';"  ;  mysql -u root -p -e "SELECT COUNT(*) FROM information_schema.tables WHERE table_schema='sei';"

<img width="960" height="223" alt="image" src="https://github.com/user-attachments/assets/9f0ced4a-df24-44b5-97cc-50df3c09a79c" />

-> Base SIP

- Acessar banco de dados do SIP - comando: mysql -u root -p sip
<img width="376" height="30" alt="image" src="https://github.com/user-attachments/assets/068adfec-fc5d-4387-b011-0f8b619997a3" />

- Atualizar os dados do órgão - comando: UPDATE orgao SET sigla='SUA_SIGLA', descricao='SUA_DESCRICAO' WHERE id_orgao=0;

<img width="582" height="49" alt="image" src="https://github.com/user-attachments/assets/0e913b95-f356-44da-a2ef-2e579a1f7ab9" />

- Atualizar a página inicial do SIP - comando: UPDATE sistema SET pagina_inicial='http://SEU_ENDERECO/sip' WHERE sigla='SIP';

<img width="701" height="54" alt="image" src="https://github.com/user-attachments/assets/3255b298-6943-46b1-8215-2b49b75c511c" />

- Atualizar os endereços e web services do SEI - comando: UPDATE sistema SET pagina_inicial='http://SEU_ENDERECO/sei/inicializar.php', web_service='http://SEU_ENDERECO/sei/controlador_ws.php?servico=sip' WHERE sigla='SEI';

<img width="1408" height="50" alt="image" src="https://github.com/user-attachments/assets/1f14eb77-3079-4e2e-98e6-927e96892fc8" />

- Consultar as alterações na tabela de órgãos - comando: SELECT sigla, descricao FROM orgao;
- Consultar as configurações dos sistemas - comando: SELECT sigla, pagina_inicial, web_service FROM sistema;
<img width="934" height="247" alt="image" src="https://github.com/user-attachments/assets/69ebab87-e808-4bf8-9277-0d5c7b833add" />

-> Base SEI

- Acessar banco de dados do SIP - comando: mysql -u root -p sei

<img width="335" height="31" alt="image" src="https://github.com/user-attachments/assets/2e21254d-653e-4391-9c95-91cd010f3035" />

- Atualizar os dados do órgão - comando: UPDATE orgao SET sigla='SUA_SIGLA', descricao='SUA_DESCRICAO' WHERE id_orgao=0;

<img width="566" height="61" alt="image" src="https://github.com/user-attachments/assets/b1befb01-ab5d-4cd8-acd9-4952d4f02abe" />

- Consultar os dados atualizados do órgão - comando: SELECT id_orgao, sigla, descricao FROM orgao;

<img width="435" height="123" alt="image" src="https://github.com/user-attachments/assets/050b2073-967a-42c8-b9c6-aa8d82c0a856" />

- Consultar a sigla do órgão nos bancos de dados SIP e SEI - comando: mysql -u sei_user -p -e "SELECT sigla FROM sip.orgao; SELECT sigla FROM sei.orgao;"

<img width="830" height="196" alt="image" src="https://github.com/user-attachments/assets/4b51ac34-3a89-4386-adcc-c6d88067ab8a" />

---

ETAPA 6 - Permissões e publicação no Apache

---

- Ajustar as permissões de propriedade dos diretórios de instalação do SEI, SIP e Infra - comando: sudo chown -R root:apache /opt/sei /opt/sip /opt/infra

<img width="618" height="27" alt="image" src="https://github.com/user-attachments/assets/97639fec-9d57-442e-9c6e-8c98225c7976" />


-> SEI

- Ajustar as permissões de diretórios no SEI - comando: sudo find /opt/sei -type d -exec chmod 2750 {} \;

<img width="575" height="28" alt="image" src="https://github.com/user-attachments/assets/ca450dbd-42b4-46f6-8387-ae1eb9de8eee" />

- Ajustar as permissões de arquivos no SEI - comando: sudo find /opt/sei -type f -exec chmod 0640 {} \;

<img width="553" height="26" alt="image" src="https://github.com/user-attachments/assets/0b42f230-3bb2-48c0-a28b-e8561db3cdab" />

- Ajustar as permissões específicas do diretório temporário (temp) - comando: sudo find /opt/sei/temp -type d -exec chmod 2570 {} \;

<img width="595" height="24" alt="image" src="https://github.com/user-attachments/assets/91bd6e6f-49d4-48f7-8c5e-4c9ac1e6cf68" />

-> SIP

- Ajustar as permissões de diretórios no SIP - comando: sudo find /opt/sip -type d -exec chmod 2750 {} \;

<img width="570" height="21" alt="image" src="https://github.com/user-attachments/assets/d28506b5-fa77-4a49-b30b-c1f36f7ebae3" />

- Ajustar as permissões de arquivos no SIP - comando: sudo find /opt/sip -type f -exec chmod 0640 {} \;

<img width="556" height="22" alt="image" src="https://github.com/user-attachments/assets/96b9be1d-a2d5-4afb-a0d9-c305e8e4c00c" />

- Ajustar as permissões específicas do diretório temporário do SIP (temp) - comando: sudo find /opt/sip/temp -type d -exec chmod 2570 {} \;

<img width="600" height="24" alt="image" src="https://github.com/user-attachments/assets/17e15a29-bd3a-4f2f-a8af-1c23ee4dcc2e" />

-> Infra 

- Ajustar as permissões de diretórios na Infra - comando: sudo find /opt/infra -type d -exec chmod 2750 {} \;

<img width="584" height="24" alt="image" src="https://github.com/user-attachments/assets/ea207696-401e-451a-af37-bc66e26d67e9" />

- Ajustar as permissões de arquivos na Infra - comando: sudo find /opt/infra -type f -exec chmod 0640 {} \;

<img width="580" height="25" alt="image" src="https://github.com/user-attachments/assets/f543bba1-ea53-44b5-9931-
  635a2714c33d" />

- Verificar as permissões e propriedades dos diretórios principais - comando: sudo ls -ld /opt/sei /opt/sei/temp /opt/sip /opt/sip/temp /opt/infra

<img width="717" height="107" alt="image" src="https://github.com/user-attachments/assets/9ba89c34-bc8a-44aa-b31e-b4e10afac8c0" />

- Conferir os arquivos com permissões incorretas no SEI, SIP e Infra - comando: sudo find /opt/sei /opt/sip /opt/infra -type f ! -perm 0640 | wc -l

<img width="709" height="36" alt="image" src="https://github.com/user-attachments/assets/96a8e698-6910-45e1-b077-cd0acd71a45f" />

-> Publicar sei e sip

- Criar o arquivo de configuração do SEI no Apache - comando: sudo vim /etc/httpd/conf.d/sei.conf

<img width="450" height="23" alt="image" src="https://github.com/user-attachments/assets/eb24d417-9755-46fa-8717-ac5025cf6b40" />

<img width="706" height="264" alt="image" src="https://github.com/user-attachments/assets/778fdf0e-6ebe-4c78-b4bb-94585c3fc41f" />

- Testar a sintaxe da configuração do Apache - comando: sudo apachectl configtest

<img width="386" height="36" alt="image" src="https://github.com/user-attachments/assets/c354c0f3-e625-4d1b-af8a-9b6fbd7e8b87" />

- Reiniciar o Apache - comando: sudo systemctl restart httpd

<img width="389" height="24" alt="image" src="https://github.com/user-attachments/assets/c404641e-1cad-44ee-a73c-847d34abedea" />

- Testar o acesso HTTP ao arquivo CSS de infraestrutura - comando: curl -I http://localhost/infra_css/infra-global-esquema.css

<img width="642" height="163" alt="image" src="https://github.com/user-attachments/assets/d48e7162-bf1b-4c34-842d-2b7435fe1ab7" />

- Testar o acesso HTTP ao arquivo JavaScript de infraestrutura - comando: curl -I http://localhost/infra_js/InfraUtil.js

<img width="534" height="154" alt="image" src="https://github.com/user-attachments/assets/aceaef7d-06de-418a-8dc0-723e9afb0a27" />

---

ETAPA 7 - Configurar o SIP

---

- Criar o arquivo de configuração do SIP - comando: sudo cp -p /opt/sip/config/ConfiguracaoSip.exemplo.php /opt/sip/config/ConfiguracaoSip.php

<img width="893" height="28" alt="image" src="https://github.com/user-attachments/assets/b4d0ae08-5d4b-40ae-81ee-975712aabcf3" />

- Pesquisar chaves de configuração do SIP - comando: sudo grep -n -E "URL|Producao|SiglaOrgao|PaginaLogin|SipWsdl|https|Servidor|Porta|Banco'|Usuario|Tipo" /opt/sip/config/ConfiguracaoSip.php

<img width="1298" height="424" alt="image" src="https://github.com/user-attachments/assets/fd2ea57e-cc34-4ad5-a994-1a83b5e87617" />

- Editar o arquivo de configuração do SIP - comando: sudo vim /opt/sip/config/ConfiguracaoSip.php

<img width="513" height="21" alt="image" src="https://github.com/user-attachments/assets/de7ccda7-be90-4210-9da8-2032d1785771" />

O que foi feito na edição:
<img width="1648" height="830" alt="image" src="https://github.com/user-attachments/assets/538b98aa-2efc-4634-8288-b9f427e187c4" />

- Testar a sintaxe do arquivo PHP criado - comando: sudo php -l /opt/sip/config/ConfiguracaoSip.php

<img width="547" height="40" alt="image" src="https://github.com/user-attachments/assets/c61f6f9d-6e6f-47c2-ad5e-fa56a9fb6653" />

- Conferir os parâmetros - comando: sudo grep -n -E "URL|Producao|SiglaOrgao|PaginaLogin|SipWsdl|https|Servidor|Porta|Banco'|Usuario|Tipo" /opt/sip/config/ConfiguracaoSip.php

<img width="1283" height="426" alt="image" src="https://github.com/user-attachments/assets/410a44c9-8a86-46e2-86fb-92a0ec36a1fc" />

- Listar os arquivos da pasta de configuração do SIP - comando: sudo ls -la /opt/sip/config

<img width="604" height="97" alt="image" src="https://github.com/user-attachments/assets/23636bbf-7c3d-498d-a12e-a41d3a5a6e86" />

---

ETAPA 8 - Configurar o SEI

---

- Criar o arquivo de configuração do SEI - comando: sudo cp -p /opt/sei/config/ConfiguracaoSEI.exemplo.php /opt/sei/config/ConfiguracaoSEI.php

<img width="886" height="23" alt="image" src="https://github.com/user-attachments/assets/9a983f16-90df-4d4e-ac15-b5609a2f4a60" />

- Pesquisar as chaves de configuração do SEI - comando: sudo grep -n -E "URL|Producao|Repositorio|SiglaOrgao|PaginaLogin|SipWsdl|https|Servidor|Porta|Banco'|Usuario|Tipo|JODConverter|CoreProtocolos" /opt/sei/config/ConfiguracaoSEI.php

<img width="1587" height="517" alt="image" src="https://github.com/user-attachments/assets/8853673c-fb68-4eb7-b0e3-f4e3bb7d958f" />

- Editar o arquivo de configuração oficial do SEI - comando: sudo vim /opt/sei/config/ConfiguracaoSEI.php

<img width="528" height="26" alt="image" src="https://github.com/user-attachments/assets/5db956c3-50dc-4aa7-987f-d9e0dc9a6cde" />

O que foi feito na edição:
<img width="1600" height="859" alt="image" src="https://github.com/user-attachments/assets/28cc1796-2fc7-4190-b72b-b9f2673e9250" />

- Testar a sintaxe do arquivo de configuração do SEI - comando: sudo php -l /opt/sei/config/ConfiguracaoSEI.php

<img width="541" height="36" alt="image" src="https://github.com/user-attachments/assets/4ed335fb-1c33-46be-9047-06562042385e" />

- Exibir um intervalo específico de linhas do arquivo - comando: sudo sed -n '81,87p' /opt/sei/config/ConfiguracaoSEI.php

<img width="663" height="130" alt="image" src="https://github.com/user-attachments/assets/8b4101c2-7da2-43b3-9eca-221b0c468027" />

- Conferir os parâmetros - comando: sudo grep -n -E "URL|Producao|Repositorio|SiglaOrgao|PaginaLogin|SipWsdl|https|Servidor|Porta|Banco'|Usuario|Tipo" /opt/sei/config/ConfiguracaoSEI.php

<img width="1381" height="483" alt="image" src="https://github.com/user-attachments/assets/5cf914e9-2de4-4b34-b5e0-2b0ec4729471" />

- Listar os arquivos da pasta de configuração do SEI - comando: sudo ls -la /opt/sei/config

<img width="637" height="132" alt="image" src="https://github.com/user-attachments/assets/0f2fe8b1-a727-450a-bb1f-f5250179e6b5" />

-> Repositório de arquivos

- Criar o diretório de repositório de arquivos do SEI - comando: sudo mkdir -p /var/sei/arquivos

<img width="432" height="28" alt="image" src="https://github.com/user-attachments/assets/fa57d96d-66f8-4722-9e9d-04e41806f85a" />

- Definir o proprietário e grupo do diretório - comando: sudo chown apache:apache /var/sei/arquivos

<img width="504" height="27" alt="image" src="https://github.com/user-attachments/assets/9f681cd7-0530-45ac-b998-3433e3a5f50a" />

- Ajustar as permissões de segurança - comando: sudo chmod 750 /var/sei/arquivos

<img width="443" height="24" alt="image" src="https://github.com/user-attachments/assets/052a23b6-367f-431e-8d94-a0f98f4061ba" />

- Validar a criação e as permissões - comando: sudo ls -ld /var/sei/arquivos

<img width="486" height="36" alt="image" src="https://github.com/user-attachments/assets/ddcb29d8-d60a-40b0-984a-e18b04ea59bb" />

-> Gravação SElinux

- Verificar os contextos de segurança SELinux e permissões de diretórios críticos - comando: sudo ls -ldZ /var/sei/arquivos /opt/sei/temp /opt/sip/temp

<img width="760" height="73" alt="image" src="https://github.com/user-attachments/assets/0d8be991-781a-4e68-a41d-b4fb75149250" />

- Instalar gerenciamento do SELinux - comando: sudo dnf install -y policycoreutils-python-utils

<img width="668" height="96" alt="image" src="https://github.com/user-attachments/assets/38c8f471-2db7-443a-9963-73acdf6f9d2e" />

- Adicionar regra de contexto SELinux para o repositório de arquivos do SEI - comando: sudo semanage fcontext -a -t httpd_sys_rw_content_t "/var/sei/arquivos(/.*)?"

<img width="785" height="27" alt="image" src="https://github.com/user-attachments/assets/68c5e246-fb5a-41a4-acb3-ad268024e60d" />

- Adicionar regra de contexto SELinux para a pasta temporária do SEI - comando: sudo semanage fcontext -a -t httpd_sys_rw_content_t "/opt/sei/temp(/.*)?"

<img width="758" height="27" alt="image" src="https://github.com/user-attachments/assets/a6fe3f48-2843-4796-9b84-f4b94a08845c" />

- Adicionar regra de contexto SELinux para a pasta temporária do SIP - comando: sudo semanage fcontext -a -t httpd_sys_rw_content_t "/opt/sip/temp(/.*)?"

<img width="751" height="22" alt="image" src="https://github.com/user-attachments/assets/9fa3ec61-708e-4535-89a4-091266baa723" />

- Aplicar os contextos de segurança SELinux recursivamente - comando: sudo restorecon -Rv /var/sei/arquivos /opt/sei/temp /opt/sip/temp

<img width="966" height="102" alt="image" src="https://github.com/user-attachments/assets/1f64a4fe-107a-49af-875f-2ff09f4b297e" />

- Validar os contextos aplicados - comando: sudo ls -ldZ /var/sei/arquivos /opt/sei/temp /opt/sip/temp

<img width="884" height="76" alt="image" src="https://github.com/user-attachments/assets/5094b19f-317a-4abb-8d8f-ef9c3a88afbd" />

- Listar as regras customizadas do SELinux - comando: sudo semanage fcontext -l -C

<img width="915" height="186" alt="image" src="https://github.com/user-attachments/assets/58e08c92-5e8c-4664-8a62-8e96f06bf84c" />


---

ETAPA 9 - Acesso pelo navegador e login

---

- Testar a resposta HTTP do SIP via linha de comando - comando: curl -I http://localhost/sip/

<img width="881" height="190" alt="image" src="https://github.com/user-attachments/assets/19a206cb-3b66-4d61-81ff-e8975e28f162" />

---

ETAPA 10 - Solr

---

-> Java

- Instalar o pacote Java OpenJDK 8 Headless - comando: sudo dnf install -y java-1.8.0-openjdk-headless

<img width="698" height="34" alt="image" src="https://github.com/user-attachments/assets/9138e330-129e-4138-be9f-514de5807f06" />


- Verificar versão do java -m comando: java -version

<img width="450" height="77" alt="image" src="https://github.com/user-attachments/assets/1d92ad66-62e4-428a-a513-10b68435c9a7" />

- Criar o usuário do sistema para o Solr/Serviços - comando: sudo useradd solr

<img width="322" height="23" alt="image" src="https://github.com/user-attachments/assets/e2cd4190-7ed3-470c-bd17-8726c8fc88f6" />

- Verificar a existência e o ID do usuário criado - comando: id solr

<img width="400" height="38" alt="image" src="https://github.com/user-attachments/assets/17079c24-3a1f-45cb-adc0-25cbdbbc2aa1" />

-> Donwload

- Verificar espaço em disco e mudar para o diretório temporário - comando: df -h /tmp && cd /tmp

<img width="489" height="53" alt="image" src="https://github.com/user-attachments/assets/6d0f0520-a79a-4141-807d-44d537635981" />

- Baixar o pacote compactado do Apache Solr 8.2.0 - comando: wget https://archive.apache.org/dist/lucene/solr/8.2.0/solr-8.2.0.tgz

<img width="746" height="35" alt="image" src="https://github.com/user-attachments/assets/576ae9e7-f99e-448d-9c07-9246fe92b34e" />

- Baixar o arquivo de validação de integridade (SHA-512) - comando: wget https://archive.apache.org/dist/lucene/solr/8.2.0/solr-8.2.0.tgz.sha512

<img width="772" height="34" alt="image" src="https://github.com/user-attachments/assets/d9f3c3b1-0feb-4aa7-aa1b-722946d231dc" />

- Validar a integridade do pacote do Solr - comando: sha512sum -c solr-8.2.0.tgz.sha512

<img width="459" height="38" alt="image" src="https://github.com/user-attachments/assets/7f7105c1-c3a3-43a5-9c9b-a97492839003" />

-> Arquivos do SEI para o Solr

- Copiar os arquivos de configuração do Solr para o diretório temporário - comando: sudo cp -r /opt/sei/config/solr/. /tmp/

<img width="491" height="24" alt="image" src="https://github.com/user-attachments/assets/9b18bcd6-1e8c-4fe7-b757-fcf4e7dfe7dd" />

- Listar o conteúdo do diretório temporário - comando: ls -l /tmp

<img width="1091" height="279" alt="image" src="https://github.com/user-attachments/assets/033e34f0-6129-43e5-a2aa-3b248ff8f76b" />


-> Conversor de arquivos para o formato Linux

- Instalar a ferramenta dos2unix - comando: sudo dnf install -y dos2unix

<img width="656" height="92" alt="image" src="https://github.com/user-attachments/assets/01e8d613-e026-4ded-815f-fc072bfdee32" />

- Converter arquivos do formato DOS para Unix - comando: sudo dos2unix /tmp/sei-solr-8.2.0.sh /tmp/solr.service

<img width="619" height="53" alt="image" src="https://github.com/user-attachments/assets/da7992ca-94db-4c3b-b8cb-496b3d63df0e" />

- Verificar o tipo de codificação dos arquivos - comando: sudo file /tmp/sei-solr-8.2.0.sh /tmp/solr.service

<img width="578" height="50" alt="image" src="https://github.com/user-attachments/assets/37e4861a-d6af-430e-949b-76c7232593d2" />

-> Instalar

- Exibir o conteúdo do script de instalação do Solr - comando: sudo cat /tmp/sei-solr-8.2.0.sh

<img width="760" height="742" alt="image" src="https://github.com/user-attachments/assets/138432d9-b159-4614-85f0-998a4ad15b08" />

- Executar o script de instalação do Solr - comando: sudo bash /tmp/sei-solr-8.2.0.sh

<img width="579" height="122" alt="image" src="https://github.com/user-attachments/assets/55729407-61a1-4092-a6c7-7078ce5e0ef3" />

- Exibir a árvore de diretórios a partir de /dados - comando: sudo tree -d /dados

<img width="376" height="387" alt="image" src="https://github.com/user-attachments/assets/c44c257a-e2e4-4360-839c-c49c544fe380" />

- Verificar permissões e detalhes dos diretórios de dados e do Solr - comando: sudo ls -ld /dados /opt/solr

<img width="419" height="54" alt="image" src="https://github.com/user-attachments/assets/54c32bc5-e9ea-47b6-bd32-71be4d12cb8b" />


-> Memória

- Localizar a configuração de memória do Solr - comando: grep -n "SOLR_JAVA_MEM" /opt/solr/bin/solr.in.sh

<img width="568" height="37" alt="image" src="https://github.com/user-attachments/assets/097e4edf-c483-416f-93d4-7ef06136c550" />

- Editar o arquivo de configuração do Solr - comando: sudo vim +NUMERO_DA_LINHA /opt/solr/bin/solr.in.sh

<img width="584" height="31" alt="image" src="https://github.com/user-attachments/assets/dda10135-119d-4060-b077-ee8bd2b709c9" />

O que foi editado:
<img width="431" height="52" alt="image" src="https://github.com/user-attachments/assets/aea6e485-0da5-4f77-875d-167b01056506" />

-> Ligar o serviço

- Recarregar as unidades do Systemd - comando: sudo systemctl daemon-reload
- Habilitar e iniciar o serviço do Solr - comando: sudo systemctl enable --now solr
- Verificar o status atual do serviço do Solr - comando: systemctl status solr

<img width="705" height="96" alt="image" src="https://github.com/user-attachments/assets/913b4d8e-2c75-4d65-ba9e-ef10ede892c5" />

- Consultar os índices - comando: curl -s "http://localhost:8983/solr/admin/cores?action=STATUS" | grep '"name"'

<img width="819" height="73" alt="image" src="https://github.com/user-attachments/assets/4da6c2b1-f5bc-4069-abf4-cc8068e49de0" />

-> Restringir o acesso ao Solr

- Fazer o backup do arquivo de configuração do Jetty - comando: sudo cp -p /opt/solr/server/etc/jetty.xml /opt/solr/server/etc/jetty.xml.original

<img width="845" height="31" alt="image" src="https://github.com/user-attachments/assets/62b98bbc-54b5-4e8a-a22e-89abcbaca5f1" />

- Localizar a tag de contextos no arquivo jetty.xml - comando: sudo grep -n "Contexts" /opt/solr/server/etc/jetty.xml

<img width="862" height="51" alt="image" src="https://github.com/user-attachments/assets/f20213ca-e053-476c-b8ca-89ec87430043" />

- Exibir um intervalo específico de linhas do arquivo jetty.xml - comando: sudo sed -n '118,124p' /opt/solr/server/etc/jetty.xml

<img width="847" height="137" alt="image" src="https://github.com/user-attachments/assets/a8ee5657-5bca-441c-bfb7-640d5f5ffa51" />

- Validar a sintaxe XML do arquivo de configuração do Jetty - comando: xmllint --noout /opt/solr/server/etc/jetty.xml
- Reiniciar o serviço do Apache Solr - comando: sudo systemctl restart solr

<img width="550" height="34" alt="image" src="https://github.com/user-attachments/assets/9e8783df-a1d7-4bb0-9069-a531dc9b4901" />

- Testar a resposta HTTP do Solr via loopback IPv4 - comando: curl -I [http://127.0.0.1:8983/solr/](http://127.0.0.1:8983/solr/)

<img width="462" height="92" alt="image" src="https://github.com/user-attachments/assets/d77482a9-7670-453f-b6b5-c8201874728e" />

- Testar a resposta HTTP do Solr pelo IP privado da máquina - comando: curl -I http://IP_PRIVADO_DA_VM:8983/solr/

<img width="479" height="92" alt="image" src="https://github.com/user-attachments/assets/50241148-b8e9-4102-9930-3b25c04d4d84" />

- Testar a resposta HTTP do Solr via hostname local forçando IPv4 - comando: curl -4 -I http://localhost:8983/solr/

<img width="494" height="103" alt="image" src="https://github.com/user-attachments/assets/55c6aac8-0da9-4e85-8bbb-b672751c7a56" />

- Testar a resposta HTTP do Solr via hostname local forçando IPv6 - comando: curl -6 -I http://localhost:8983/solr/

<img width="514" height="62" alt="image" src="https://github.com/user-attachments/assets/fe7f77a7-deb7-4626-9e45-d3b66290d49e" />

- Localizar a referência do Solr no arquivo do SEI - comando: sudo grep -n "8983" /opt/sei/config/ConfiguracaoSEI.php

<img width="605" height="42" alt="image" src="https://github.com/user-attachments/assets/fcbfb4de-df06-4fa6-8942-1d0cfd394795" />

- Validar a sintaxe PHP do arquivo do SEI - comando: sudo php -l /opt/sei/config/ConfiguracaoSEI.php

<img width="556" height="41" alt="image" src="https://github.com/user-attachments/assets/ce6bf9f9-a1c6-4d59-a4a5-4b4d8c948fc0" />


-> Indexar

- Executar a indexação completa de protocolos do SEI - comando: sudo /usr/bin/php -c /etc/php.ini /opt/sei/scripts/indexacao_protocolos_completa.php

<img width="868" height="100" alt="image" src="https://github.com/user-attachments/assets/7a738c70-6227-4807-b875-8cc05b0fd645" />

- Executar a indexação de publicações do SEI - comando: sudo /usr/bin/php -c /etc/php.ini /opt/sei/scripts/indexacao_publicacoes.php

  <img width="783" height="96" alt="image" src="https://github.com/user-attachments/assets/4a58e1a9-6517-4768-be87-0ea5f15c53b4" />

- Executar a indexação das bases de conhecimento do SEI - comando: sudo /usr/bin/php -c /etc/php.ini /opt/sei/scripts/indexacao_bases_conhecimento.php

<img width="830" height="94" alt="image" src="https://github.com/user-attachments/assets/e2b695f6-5a51-4b49-9061-07ecbba31618" />

- Verificar o status e número de documentos do core de protocolos no Solr - comando: curl -s "http://127.0.0.1:8983/solr/admin/cores?action=STATUS&core=sei-protocolos" | grep numDocs

<img width="956" height="38" alt="image" src="https://github.com/user-attachments/assets/593e7594-a069-4623-87bb-869b073d0d4f" />

---

ETAPA 11 - Agendamentos

---

- Consultar os parâmetros de e-mail do SIP no banco de dados - comando: mysql -u root -p sip -e "SELECT nome, valor FROM infra_parametro WHERE nome LIKE 'SIP_EMAIL%';"

<img width="937" height="117" alt="image" src="https://github.com/user-attachments/assets/477f218c-2b21-4bd3-8dfe-9457ce5b500f" />

- Consultar os parâmetros de e-mail do SEI no banco de dados - comando: mysql -u root -p sei -e "SELECT nome, valor FROM infra_parametro WHERE nome LIKE 'SEI_EMAIL%';"

<img width="941" height="144" alt="image" src="https://github.com/user-attachments/assets/0c6a4494-d1b7-4587-bfd8-8bb223070cf4" />

-> Agendar sem cron

- Criar o arquivo de agendamentos automáticos (cron) do SEI e do SIP - comando: sudo vim /etc/cron.d/sei-agendamentos

<img width="479" height="25" alt="image" src="https://github.com/user-attachments/assets/dc47e2c3-a07f-415a-a93c-24df84959274" />
 
<img width="1038" height="115" alt="image" src="https://github.com/user-attachments/assets/64538ed1-00bf-4077-91f5-c49b843dbb39" />

- Exibir o conteúdo do arquivo de agendamentos do SEI e do SIP - comando: cat /etc/cron.d/sei-agendamentos
- Verificar as permissões e detalhes do arquivo de agendamentos do SEI e do SIP - comando: ls -l /etc/cron.d/sei-agendamentos
- Verificar se o serviço do Cron está em execução (ativo) - comando: systemctl is-active crond
- Verificar se o serviço do Cron está habilitado para iniciar com o sistema - comando: systemctl is-enabled crond

<img width="1019" height="158" alt="image" src="https://github.com/user-attachments/assets/5402f3df-a9d5-47e6-9dd9-d691e0659b76" />

- Executar script de agendamento de tarefas do SEI - comando: sudo /usr/bin/php -c /etc/php.ini /opt/sei/scripts/AgendamentoTarefaSEI.php
- Executar script de agendamento de tarefas do SIP - comando: sudo /usr/bin/php -c /etc/php.ini /opt/sip/scripts/AgendamentoTarefaSip.php

- Verificar os registros recentes de execução dos agendamentos no log do cron - comando: sudo grep AgendamentoTarefa /var/log/cron | tail -5

<img width="1340" height="109" alt="image" src="https://github.com/user-attachments/assets/b7595c8b-72dc-4e1d-a4bb-d71b2dd9d2b9" />


---

ETAPA 12 - PDF

---

- Verificar o caminho de instalação do binário wkhtmltopdf - comando: which wkhtmltopdf

<img width="1153" height="38" alt="image" src="https://github.com/user-attachments/assets/fdd37491-387d-4d61-9c06-8aaf4846620e" />

- Verificar os cabeçalhos de resposta HTTP para o download do pacote RPM do wkhtmltopdf - comando: curl -sI https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6-1/wkhtmltox-0.12.6-1.centos8.x86_64.rpm | head -n 1

<img width="1175" height="42" alt="image" src="https://github.com/user-attachments/assets/a8c4b503-8ed2-4321-970d-843742c86f8d" />

- Baixar o pacote RPM do wkhtmltopdf do GitHub - comando: wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6-1/wkhtmltox-0.12.6-1.centos8.x86_64.rpm

<img width="1040" height="36" alt="image" src="https://github.com/user-attachments/assets/5557195f-3647-44a0-83e3-8604a87e79e5" />

- Instalar o pacote RPM baixado utilizando o gerenciador DNF - comando: sudo dnf install -y ./wkhtmltox-0.12.6-1.centos8.x86_64.rpm

<img width="660" height="32" alt="image" src="https://github.com/user-attachments/assets/3753ee2c-eed8-4057-aa2f-7981424a0a4d" />

- Verificar a versão do wkhtmltopdf  - comando: wkhtmltopdf --version
- Confirmar o caminho do binário do wkhtmltopdf - comando: which wkhtmltopdf

<img width="334" height="71" alt="image" src="https://github.com/user-attachments/assets/20e87095-93cd-4b88-b161-2da99add9ba4" />

