# SGBD-s
Scripts e dicas referente a Banco de Dados relacionais;

###Oracle



###SQL Server

Cursos OnLine Free:
Este curso vai deste a linguagem até as abordagens de gerenciamento de um banco de dados (DBA): http://juliobattisti.com.br/artigos/sqlserver2005/principal.asp
Este curso vai deste a linguagem até as abordagens de gerenciamento de um banco de dados (DBA): https://www.microsoft.com/learning/en-us/course.aspx?translate=pt&ID=40364A

Para quem tem uma grana extra e internet boa, essa é a melhor escola do Brasil para cursos em nossa Área: http://www.impactaonline.com.br/curso/SQL-2012-Modulo-I-online.php

Tutoriais Sobre Select
Create database e principais nomenclaturas técnicas do banco de dados: https://programandodotnet.wordpress.com/2011/07/20/sql-server-conceitos-gerais/

Neste site explica os comandos create table, chaves, alteração de tabelas, tipos de dados, insert, update, delete e select: https://andrielleazevedo.wordpress.com/category/sql-server/

Neste explica as principais funções para manipular o tipo de dados String (char, varchar etc...): http://www.linhadecodigo.com.br/artigo/3070/manipulacao-de-strings-com-sql-server-2008-r2.aspx

Exemplo de como utilizar o CASE WHEN CAMPO OPERADOR THEN RESULTADO 1 ELSE RESULTADO 2 END : https://www.portaleducacao.com.br/informatica/artigos/6356/utilizando-a-clausula-case-em-um-select-sql-server

Consultas SQL Avançadas: https://books.google.com.br/books?id=oRmZrDph5WMC&pg=RA1-PT67&lpg=RA1-PT67&dq=select+sql+server&source=bl&ots=oc5DW4e-DK&sig=K1-ULhxN4sGD4T7RyEohcuCxtVk&hl=pt-BR&sa=X&ei=sGgqVbXdK8HZgwS-m4SwDA&ved=0CDQQ6AEwAzgo#v=onepage&q=select%20sql%20server&f=false

Principais Funções SQL Server: https://programandodotnet.wordpress.com/2011/12/12/funcoes-sql-server/

Views: https://programandodotnet.wordpress.com/2011/09/26/sql-server-views/


###MySQl
Dicas para utilizar o mysqldump para fazer o backup corretamente e isolado do seu banco de dados mysql, seja por algum crash, alguma atualização ou modificação mal feita no servidor, você pode em ultimo caso recorrer ao backup manual dos arquivos, podendo assim você logo apos restaurar os arquivo em uma nova configuração de mysql:

1- Faça backup dos bancos de dados:
cp -rf /var/lib/mysql/ ~/backup_mysql

2 – Reconfigure seu novo servidor

3 – Pare o servidor
service mysql stop

4 – Copie de volta os bancos de dados que deseja, normalmente estes sao separados por pastas
cp -rf ~/mysql_backup/meu_db /var/lib/mysql/

5 – Caso voce possua algum banco de dados InnoDB, voce tambem tera que copiar a pasta ibdata1.
cp -rf ~/mysql_backup/ibdata1 /var/lib/mysql/

6 – Restaure as permissoes dos arquivos
chown mysql:mysql /var/lib/mysql/* -R

7 – Reinicie o servidor, e provavelmente estará tudo funcionando
service mysql start


###Postgre



###Firebird
