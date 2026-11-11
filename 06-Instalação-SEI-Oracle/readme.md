
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
