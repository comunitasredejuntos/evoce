# evoce

Para a instalação da aplicação campinasevoce.campinas.sp.gov.br é necessário ter os seguintes requisitos:
-> Servidor Apache + PHP
-> Servidor MySQL

Versões das aplicações instaladas atualmente no ambiente de produção: Apache/2.2.16, PHP 5.3.3-7 e MySQL 5.1.72-2.

O arquivo compactado campinasevoce-FULL2.zip contém: pasta "html" com os fontes do ambiente de produção e a pasta "Copia do BD" com o dump completo do banco de dados de produção, todos extraídos do ambiente de produção do dia 11/03/2014. OBS: os nomes de usuários de conexão e senha de banco de dados foram omitidos, assim como o conteúdo da tabela de usuarios do sistema em produção.



############## Passos para colocar a aplicação em funcionamento ##############

1. Descompacte o arquivo enviado, copie a pasta "html" para o "DocumentROOT" do apache;

2. Configure o virtualhost da seguinte forma:

NameVirtualHost seuservidorapache.com.br:80
<VirtualHost seuservidorapache.com.br:80>
  ServerName    publico.evoce.com.br
  ServerAlias   publico

  DocumentRoot  /CAMINHO_DESEJADO/html/publico
  ErrorLog      /CAMINHO_DESEJADO/logs/error.log
  Customlog     /CAMINHO_DESEJADO/logs/access.log combined

  php_value register_globals Off

  <Directory /CAMINHO_DESEJADO/html/publico>
        Options None
        AllowOverride None
        order allow,deny
        Allow from all
  </Directory>

</VirtualHost>


<VirtualHost seuservidorapache.com.br:80>
  ServerName    adm.evoce.com.br
  ServerAlias   adm

  DocumentRoot  /CAMINHO_DESEJADO/html
  ErrorLog      /CAMINHO_DESEJADO/logs/error.log
  Customlog     /CAMINHO_DESEJADO/logs/access.log combined

  php_value register_globals Off

  <Directory /CAMINHO_DESEJADO/html>
        Options None
        AllowOverride None
        order allow,deny
        Allow from all
  </Directory>

</VirtualHost>



3. Crie uma nova base no MySQL para restaurar o dump campinasevoce.sql que está dentro da pasta "Copia do BD";

4. Configure o arquivo dentro do caminho "/CAMINHO_DESEJADO/html/publico/php/connections/connections.php" com o nome da base de dados, o usuario de acesso a base de dados e senha;

5. Se desejar, configurar o usuário do apache nas pastas "download" e "images" para ter acesso de escrita e leitura, para que funcionalidades como upload de imagens funcione.
