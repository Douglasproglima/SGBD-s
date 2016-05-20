# SGBD-s
Scripts e dicas referente a Banco de Dados relacionais;

###Oracle
###Dicas 01

Criar banco de dados:
create tablespace DADOS
     datafile
      'C:\oraclexe\app\oracle\oradata\XE\DADOS.dbf' size 100m autoextend on next 50m maxsize 500m
     online
      permanent
      extent management local autoallocate
     segment space management auto;


alter tablespace INDECES offline

drop tablespace DADOS including contents 

create tablespace DADOS
     datafile
      'C:\oraclexe\oradata\XE\DADOS.dbf' size 100m autoextend on next 50m maxsize 500m
     online
      permanent
      extent management local autoallocate
     segment space management auto;



CREATE USER NOME_DO_USUARIO IDENTIFIED BY SENHA_DE_ACESSO
   default TableSpace NOME_DA_TABLESPACE
   Temporary TableSpace TEMP

###Dicas 02

/*Comandos para criar as TableSpaces*/
create TableSpace TSDNomeDoBanco 
   DataFile 'C:\oraclexe\app\oracle\oradata\XE\TSDCodil.DBF' SIZE 30M Reuse
   AutoExtend On Next 512k;

create TableSpace TSINomeDoBanco 
   DataFile 'C:\oraclexe\app\oracle\oradata\XE\TSICodil.DBF' SIZE 30M Reuse
   AutoExtend On Next 512k;


/*Comandos para criar o usuário*/
CREATE USER UsuarioNome IDENTIFIED BY USUARIO
   default TableSpace TSDNomeDoBanco
   Temporary TableSpace TEMP;
   
/*Comandos para dar acessos ao usuário e teste de conexão*/ 
GRANT CONNECT TO NomeDoBanco;
GRANT RESOURCE TO NomeDoBanco;
GRANT DBA TO NomeDoBanco;
CONNECT NomeDoBanco/USUARIO@XE;  

_________________________________________
/*CRIA DIRETORIO PARA REALIZAÇÃO DO EXPORTAR DUMP VIA EXP OU EXPDP*/
CREATE DIRECTORY DUMPS AS 'D:\Dumps\';
GRANT READ, WRITE ON DIRECTORY Dumps TO ENGEMAN;

__________________________________________
/*DELETA USUÁRIO DO ORACLE, SEGUIDO DAS TABLESPACES*/

DROP USER PORTOBELLO CASCADE;
DROP TABLESPACE TSDCODIL INCLUDING CONTENTS AND DATAFILES;
DROP TABLESPACE TSICODIL INCLUDING CONTENTS AND DATAFILES;

###Dicas 03 - SQL para listar o nomes das tablesSpaces

SELECT DISTINCT TABLESPACE_NAME NOME, 'DADOS' AS TIPO FROM USER_TABLES
UNION ALL
SELECT DISTINCT TABLESPACE_NAME NOME, 'INDICES' AS TIPO FROM USER_INDEXES

--RETORNA O NOME DAS TABLESPACES VINCULADO AO ARQUIVO .DBF
select tablespace_name,file_name from dba_data_files 



###__________________________________________
###SQL Server

Script de um cursor em SQL Server, para concatenar uma string (e-mails):
//Deleta o último ponto e vírgula do retorno do SQL

DECLARE @EMAIL VARCHAR(8000)
DECLARE @LISTEMAIL VARCHAR(8000)

SET @LISTEMAIL='';

DECLARE TESTE CURSOR FOR
  SELECT RETORNO FROM CFGUSR WHERE U_MAILSSOS = 'S'
OPEN TESTE
  FETCH NEXT FROM TESTE INTO @EMAIL
  
  WHILE @@FETCH_STATUS = 0  BEGIN 
    SET @LISTEMAIL = @LISTEMAIL+@EMAIL+';';
    FETCH NEXT FROM TESTE INTO @EMAIL
  END
CLOSE TESTE
DEALLOCATE TESTE
SELECT LEFT(@LISTEMAIL, LEN(@LISTEMAIL)-1) AS EMAILS

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




###__________________________________________
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




###__________________________________________
###Postgre





###__________________________________________
###Firebird
