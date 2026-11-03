Relatório Técnico de Resolução de Incidente (Troubleshooting)

 A aplicação web em 3 camadas apresentou indisponibilidade total em sua interface gráfica. A investigação identificou três falhas encadeadas
  
    1 -> Camada de Aplicação : O serviço NOde.js (training-api) encontrava-se parado (inactive)
    
    2 -> Camada de Banco de Dados : O usuário training_app não possuía privilégios na tabela "ITEMS" do banco "TRAINING", gerando erro HTTP 500
    
    3 -> Camada de Web/Proxy : A diretiva "location /api/" no Ngingx impedia o roteamento de requisições, devolvendo HTML no lugar de JSON (ocorrendo o erro Unexpected token '<')


  Passo a passo técnico de Diagnóstico e Resolução

  Etapa 1 : Conexão e Investigação do Back-end
  
  -> Realizado o acesso no POWERSHELL 
  
    . Entrei na pasta Downloads para localizar a chave privada lab.pem 
  
    . Listei o arquivo lab.pem para confirmar se a chave SSH estava na pasta 
  
    . Iniciei a conexão com a SSH com o servidor Linux usando a chave la.pem

<img width="467" height="56" alt="image" src="https://github.com/user-attachments/assets/f02cf3bc-d715-499a-9228-02cfc02991eb" />

<img width="628" height="220" alt="image" src="https://github.com/user-attachments/assets/4d3acf90-84ca-47ed-9f56-55c5b0a42d2b" />

<img width="727" height="809" alt="image" src="https://github.com/user-attachments/assets/d5b98688-d20b-4759-a973-e562e0a6f86f" />

Objetivo : Localizar a chave privada e acessar a instância "trainne-02" via SSH


-> Ativação da API Node.js

    . Consultei o estado do serviço da API, mostrou que o back-end estava parado
    . Iniciei o serviço da API
    . Confirmei se a API subiu e se apropriou da porta 3000
    . Realizei a chamad apenas do HTTP para testar se o Nginx estava respondendo na porta 80
    . Chequei o histórico do serviço pelas últimas 50 linhas dos logs do serviço da API 
    
<img width="886" height="204" alt="image" src="https://github.com/user-attachments/assets/6b018a7f-1f8f-4dce-8652-28ff1047fe8d" />

<img width="569" height="28" alt="image" src="https://github.com/user-attachments/assets/10d6d7ef-8cbb-470e-ae43-27b878584a2b" />

<img width="886" height="40" alt="image" src="https://github.com/user-attachments/assets/7f539587-248e-49bc-92e7-e6d634aa3a8a" />

<img width="477" height="192" alt="image" src="https://github.com/user-attachments/assets/ae7725b6-3124-44d6-a8df-a3794f0cfa7d" />

<img width="886" height="125" alt="image" src="https://github.com/user-attachments/assets/89c73c8c-2e45-413f-b518-09ab5f00bf24" />

Objetivo : O status confirmou que o back-end estava 'inactive (dead)'. Após o 'start' o comando 'ss' confirmou o processo Node.js ativo na porta 3000



Etapa 2 : Diagnóstico e Correção no Banco de Dados

-> Identificação do Erro HTTP 500

    . Requisitei o caminho da /api diretamente na API, retornou "400 Not Found"
    . Requisitei a rota de dados para testar a consulta ao banco, retornou "500 Internal Server Error"


  <img width="886" height="205" alt="image" src="https://github.com/user-attachments/assets/5e1a256e-ca70-47b6-b891-7db7979253aa" />
  <img width="886" height="138" alt="image" src="https://github.com/user-attachments/assets/9c95005e-3110-4ff0-a988-0714303bc042" />


Diagnóstico : A API retornou "permission denied for table items"


-> Ajuste de Permissões no PostgreSQL

. Acesso direto ao console psql

<img width="570" height="97" alt="image" src="https://github.com/user-attachments/assets/a1147037-0fd6-4ac0-8f04-6fd93ad2ea90" />

. Comandos executados dentro do psql: 
  
    . Listei o banco de dados, revelando o banco 'training'
    . Listei os roles, confirmou o usuário 'training_app'
    . Conectei ao banco de dados training 
    . Concedi o acesso às tabelas
    . Concedi acesso às sequencias 
    . Sai do PostgreSQL

<img width="886" height="260" alt="image" src="https://github.com/user-attachments/assets/ba0d9e98-b00b-418b-96d0-af5d4547a83d" />


<img width="670" height="45" alt="image" src="https://github.com/user-attachments/assets/7ee35691-a1fe-4211-a480-352646189bf7" />

<img width="795" height="45" alt="image" src="https://github.com/user-attachments/assets/c80ba18b-ee5f-43cf-9580-f22e48b9f182" />

<img width="816" height="47" alt="image" src="https://github.com/user-attachments/assets/0606a30b-93b3-4223-baed-ec61fb3ff0ec" />

<img width="247" height="34" alt="image" src="https://github.com/user-attachments/assets/4d0d954a-75d3-4215-b7b8-28fffda1d6ec" />

. Validação Interna da API 
      
    . Reexecutei o teste da consulta de itens na API 

<img width="645" height="152" alt="image" src="https://github.com/user-attachments/assets/b78fbc3d-d801-4b6d-9696-7a5d38b20953" />

Resultado : Retornou "HTTP/1.1 200 OK", validando a comunicação entre API e PostreSQL


Etapa 3 : Estado da Interface e Correção do Proxy Reverso (Nginx)

-> Ao abrir o navegador, a página exibiu a tag "Falha ao consultar a aplicação" com a mensagem " Unexpected token '<' "

<img width="886" height="395" alt="image" src="https://github.com/user-attachments/assets/6e836040-2d5e-4235-9ab6-591484375109" />


-> Investigação do Nginx
      
    . Identifiquei o link 'training'
    . Exibiu a regra incorreta: location /api/
    . Verifiquei os erros de requisição 404/304


<img width="877" height="69" alt="image" src="https://github.com/user-attachments/assets/15ecd3a4-0396-41bf-82f0-6502e8e35e9d" />

<img width="886" height="387" alt="image" src="https://github.com/user-attachments/assets/e051fd89-371c-46bd-8562-bdfaf76362fb" />

<img width="886" height="208" alt="image" src="https://github.com/user-attachments/assets/38b5870c-1621-4a27-9177-184373c8de9b" />

Causa : O Nginx ainda tentava responder pela rota location /api/ , devolvendo a página HTML padrão (index.html) em vez de repassar para o Node.js


-> Correção no arquivo de Configuração
<img width="886" height="23" alt="image" src="https://github.com/user-attachments/assets/737cf90f-8431-4191-84e0-0d59153ec338" />

<img width="886" height="460" alt="image" src="https://github.com/user-attachments/assets/81397780-40fe-4e80-aaa8-206ccaa14b8d" />

-> Ajuste realizado : Alterado de location /api/ para location /api
<img width="886" height="616" alt="image" src="https://github.com/user-attachments/assets/bae2a68b-4d8d-4dd1-ac1b-f0d7a1e5978d" />


    . Validei a sintaxe do arquivo 
    . Reiniciei o Nginx 

<img width="886" height="84" alt="image" src="https://github.com/user-attachments/assets/7c1807c1-0659-43b7-a7d1-e3e2a3596c8f" />

<img width="886" height="36" alt="image" src="https://github.com/user-attachments/assets/bd041063-7536-4692-8046-7c5c53d964f8" />


-> Conclusão e Resultado Final 

<img width="886" height="426" alt="image" src="https://github.com/user-attachments/assets/a8b41c25-b13b-4cf2-99cb-93ecbcdccb1e" />

  -> Após a reinicialização do Nginx, a requisição /api/items feita pelo navegador foi repassada com sucesso para a API Node.js (porta 3000), que por sua vez consultou a tabela no PostreSQL. A interface web atualizou automaticamente, exibindo a tag "Front, back e banco OK", o nome da instância (trainne-02) e os itens cadastrados no banco (Linux, Redes, DevOps)
