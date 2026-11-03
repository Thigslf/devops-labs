INSTALAÇÃO DO SEI

ETAPA 1 – Extração dos arquivos 
	Descompactando o pacote de Fontes:
     
     sudo unzip -o /opt/sei-lab/sei-Fontes-4.0.12.15.zip -d /opt/
     
  Verificar se foi :
  
      ls -d /opt/sei /opt/sip /opt/infra
      
ETAPA 2 - Instalar e configura o Apache, Memcached e o PHP7.4
  Instalar o PHP 7.4:

    sudo amazon-linux-extras enable php7.4
Instalar o apache, memcached e as ferramentas :
      
      sudo yum install -y httpd httpd-tools memcached
      
Instalar as extensões do sei:
    
    sudo yum install -y php php-common php-cli php-fpm php-json php-mysqlnd php-gd php-mbstring php-xml php-intl php-pecl-memcache php-soap php-bcmath

Ativar e iniciar os serviços: 

    sudo systemctl enable --now httpd
    sudo systemctl enable --now memcached
    sudo systemctl enable --now php-fpm


Criação do backup do ini
  
    sudo cp /etc/php.ini /etc/php.ini.backup

Editar o php.ini:
    
    sudo vim /etc/php.ini
    
    O que trocar:
    short_open_tag = On
    default_charset = "ISO-8859-1"
    include_path = ".:/opt/infra/infra_php"
    session.gc_maxlifetime = 28800
    session.cookie_secure = 0
    default_socket_timeout = 60
    max_input_vars = 1000
    html_errors = Off
    post_max_size = 201M
    upload_max_filesize = 200M
  
  Reiniciar o php
  
    sudo systemctl restart php-fpm
    
    
  Configurar o virtualhost do apache

    sudo vim /etc/httpd/conf.d/sei.conf

    Copiar:
    Alias "/sei" "/opt/sei/web"
    Alias "/sip" "/opt/sip/web"
    Alias "/infra_css" "/opt/infra/infra_css"
    Alias "/infra_js" "/opt/infra/infra_js"
    
    <Directory />
      AllowOverride None
      Require all denied
    </Directory>
    
    <Directory ~ "(/opt/sei/web|/opt/sip/web|/opt/infra/infra_css|/opt/infra/infra_js)">
      AllowOverride None
    Options None
    Require all granted
    </Directory>
  Testar a sintaxe 
  
    sudo apachectl configtest
    
  Recarregar o apche

    sudo systemctl reload httpd

ETAPA 3 - Permissões das pastas
 Permissão nas pastas
 
    sudo chown -R root:apache /opt/sei
    sudo chown -R root:apache /opt/sip
    sudo chown -R root:apache /opt/infra

Ajustar as permissões das pastas 2750 e arquivos 0640
    
    sudo find /opt/sei /opt/sip /opt/infra -type d -exec chmod 2750 {} +
    sudo find /opt/sei /opt/sip /opt/infra -type f -exec chmod 0640 {} +

Liberar permissão especial de escrita nas pastas temp

    sudo chmod -R 2570 /opt/sei/temp
    sudo chmod -R 2570 /opt/sip/temp

ETAPA 4 - Banco de dados MYSQL 5.7

instalar repositório:

    sudo yum install -y https://dev.mysql.com/get/mysql57-community-release-el7.noarch.rpm
    sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
    sudo yum install -y mysql-community-server
    sudo systemctl enable --now mysqld
    mysqld --version

Configurar o mysql:
      
      sudo vim /etc/my.cnf

    Adicionar:
    character-set-server=latin1
    collation-server=latin1_swedish_ci
    default_authentication_plugin=mysql_native_password
    max_allowed_packet=128M
    18.	Iniciar o serviço:
    sudo systemctl enable --now mysqld
  
  Acessar o console:
        
        sudo mysql
    
    Copiar:
    CREATE DATABASE IF NOT EXISTS sip CHARACTER SET latin1 COLLATE latin1_swedish_ci;
    CREATE DATABASE IF NOT EXISTS sei CHARACTER SET latin1 COLLATE latin1_swedish_ci;
    
    CREATE USER IF NOT EXISTS 'sei_user'@'localhost' IDENTIFIED WITH mysql_native_password BY 'teste';
    CREATE USER IF NOT EXISTS 'sei_user'@'127.0.0.1' IDENTIFIED WITH mysql_native_password BY 'teste';
    GRANT ALL PRIVILEGES ON sei.* TO 'sei_user'@'localhost', 'sei_user'@'127.0.0.1';
    GRANT ALL PRIVILEGES ON sip.* TO 'sei_user'@'localhost', 'sei_user'@'127.0.0.1';
    FLUSH PRIVILEGES;
    EXIT;

  Descompactar o sql :
    
    sudo unzip -o /opt/sei-lab/sei-bd-mysql-4.0.12.15.zip -d /opt/sei-lab/

Importar os bancos de referencia

    do sip: sudo mysql sip < /opt/sei-lab/sip_4.0.x.1_BD_Ref_Exec.sql
    do sei: sudo mysql sei < /opt/sei-lab/sei_4.0.x.1_BD_Ref_Exec.sql


  Sincronizar o Órgão lab e as urls

    copiar:
    
    UPDATE sip.orgao SET sigla='LAB', descricao='Laboratorio SEI' WHERE id_orgao=0;
    UPDATE sei.orgao SET sigla='LAB', descricao='Laboratorio SEI' WHERE id_orgao=0;
    
    UPDATE sip.sistema SET pagina_inicial='http:// <ENDERECO_DA_EC2>/sip' WHERE sigla='SIP';
    UPDATE sip.sistema SET pagina_inicial='http:// <ENDERECO_DA_EC2>/sei/inicializar.php', web_service='http:// <ENDERECO_DA_EC2>/sei/controlador_ws.php?servico=sip' WHERE sigla='SEI';
    
    EXIT;

ETAPA 5 - Arquivos de Configuração do SIP e do SEI

Configuração do sip

    sudo cp /opt/sip/config/ConfiguracaoSip.exemplo.php /opt/sip/config/ConfiguracaoSip.php

Editar o sip:
    
    sudo vim /opt/sip/config/ConfiguracaoSip.php
    Copiar:
    
    'URL' => 'http:// <ENDERECO_DA_EC2>/sip',
    'SiglaOrgaoSistema' => 'LAB',
    'PaginaLogin' => 'http:// <ENDERECO_DA_EC2>/sip/login.php',
    'SipWsdl' => 'http:// <ENDERECO_DA_EC2>/sip/controlador_ws.php?servico=sip',
    'https' => false,
    
     BancoSip:
    'Servidor' => '127.0.0.1',
    'Porta' => '3306',
    'Banco' => 'sip',
    'Usuario' => 'sei_user',
    'Senha' => '<SENHA_DO_BANCO>',
    'Tipo' => 'MySql',
    CacheSip:
    'Servidor' => '127.0.0.1',
    'Porta' => '11211'


 Configuração do sei :

    sudo cp /opt/sei/config/ConfiguracaoSEI.exemplo.php /opt/sei/config/ConfiguracaoSEI.php

Editar o sei:

      sudo vim /opt/sei/config/ConfiguracaoSEI.php
          
    'URL' => 'http:// <ENDERECO_DA_EC2>/sei',
    'RepositorioArquivos' => '/opt/sei/dados',
    'SiglaOrgaoSistema' => 'LAB',
    'PaginaLogin' => 'http:// <ENDERECO_DA_EC2>/sip/login.php',
    'SipWsdl' => 'http:// <ENDERECO_DA_EC2>/sip/controlador_ws.php?servico=sip',
    'https' => false,
    
     BancoSEI:
    'Servidor' => '127.0.0.1',
    'Porta' => '3306',
    'Banco' => 'sei',
    'Usuario' => 'teste',
    'Senha' => 'teste',
    'Tipo' => 'MySql',
    
    No bloco CacheSEI:
    'Servidor' => '127.0.0.1',
    'Porta' => '11211',
    
    No bloco Solr:
    'Servidor' => 'http://127.0.0.1:8983/solr',

Ajustar as permissão de segurança dos arquivos:

    sudo chown root:apache /opt/sip/config/ConfiguracaoSip.php /opt/sei/config/ConfiguracaoSEI.php
    sudo chmod 0640 /opt/sip/config/ConfiguracaoSip.php /opt/sei/config/ConfiguracaoSEI.php

ETAPA 6 - Atualização das versões do banco 

    sip: sudo php /opt/sip/scripts/sip_atualizar_versao.php
    sei: sudo php /opt/sei/scripts/sei_atualizar_versao.php
ETAPA 7 - Apache Solr 8.2
Instalar java 8 (amazon corretto):

      sudo amazon-linux-extras enable corretto8
      sudo yum install -y java-1.8.0-amazon-corretto
Instalar o apache solr 8.2

      cd /tmp 
      wget https://archive.apache.org/dist/lucene/solr/8.2.0/solr-8.2.0.tgz
      tar xzf solr-8.2.0.tgz solr-8.2.0/bin/install_solr_service.sh --strip-components=2
      sudo bash ./install_solr_service.sh solr-8.2.0.tgz -u solr -i /opt -d /dados/solr -p 8983

Copiar os núcleos do sei para o solr:

    sudo cp -r /opt/sei/config/solr/sei-cores-8.2.0/* /dados/solr/data/
Criar as pastas  para os 3 :

      sudo mkdir -p /dados/sei-protocolos/conteudo
      sudo mkdir -p /dados/sei-bases-conhecimento/conteudo
      sudo mkdir -p /dados/sei-publicacoes/conteúdo
      
Copiar dicionários auxiliares de sinônimos e stopwords:

    sudo cp -rn /opt/solr/server/solr/configsets/sample_techproducts_configs/conf/* /dados/solr/data/sei-protocolos/conf/
    sudo cp -rn /opt/solr/server/solr/configsets/sample_techproducts_configs/conf/* /dados/solr/data/sei-bases-conhecimento/conf/
    sudo cp -rn /opt/solr/server/solr/configsets/sample_techproducts_configs/conf/* /dados/solr/data/sei-publicacoes/conf/

Ajustar dono das pastas e reiniciar o serviço:

      sudo chown -R solr:solr /dados
      sudo systemctl enable --now solr
      sudo systemctl restart solr

ETAPA 8 - Gerador de Documentos em PDF
Acessar a pasta temporária e baixar o pacote

    cd /tmp
    wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6-1/wkhtmltox-0.12.6-1.centos7.x86_64.rpm
Instalar o pacote:

    sudo yum localinstall -y wkhtmltox-0.12.6-1.centos7.x86_64.rpm
Validar a versão: 

    wkhtmltopdf --version

ETAPA 9 - Serviços complementares

Criar repositório de documentos anexos do SEI

    sudo mkdir -p /opt/sei/dados
    sudo chown -R apache:apache /opt/sei/dados
    sudo chmod 770 /opt/sei/dados

Instalar e iniciar o serviço de e-mail

    sudo yum install -y postfix
    sudo systemctl enable --now postfix

Cadastrar e-mail de adm no sip

    sudo mysql -e "INSERT INTO sip.infra_parametro (nome, valor) VALUES ('SIP_EMAIL_ADMINISTRADOR', 'teste@dominio.gov.br') ON DUPLICATE KEY UPDATE valor='teste@dominio.gov.br';"

Configurar os agendamentos CRON

    sudo vim /etc/cron.d/sei
    
    * * * * * root /usr/bin/php -c /etc/php.ini /opt/sei/scripts/AgendamentoTarefaSEI.php 2>&1 >> /root/infra_agendamento_sei.log
    * * * * * root /usr/bin/php -c /etc/php.ini /opt/sip/scripts/AgendamentoTarefaSip.php 2>&1 >> /root/infra_agendamento_sip.log
    00 01 * * * root rm -rf /opt/sei/temp/*
    00 01 * * * root rm -rf /opt/sip/temp/*
Criar arquivo robots.txt

    sudo vim /var/www/html/robots.txt
    cole: User-agent: *
            Disallow: /

Reiniciar os serviços: 

    sudo systemctl restart php-fpm
    sudo systemctl restart httpd

Etapa 10: Validação

  Abrir o navegador e acessar as URLs:
    SIP: http:// <ENDERECO_DA_EC2>/sip
    SEI: http:// <ENDERECO_DA_EC2>/sei

Faça o login com os dados padrão:
  Usuário: teste
  Senha: teste
  Órgão: LAB
