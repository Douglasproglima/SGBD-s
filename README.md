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

###Dicas 01 - Restaurar Backup no Windows
1 - Acessar o cmd como admistrardor;


2 - Acessar o diretório onde está instalado o MySQL, exemplo cd "C:\Arquivos de Programas\MySQL\MySQL Server 5.6\bin\";


3 - Digite o comando mysql –h + o host do servidor Mysql (exemplo : mysql5.inetweb.com.br) –u + conta de usuário -p –D + nome do banco de dados < caminho 


(exemplo : c:\backup.sql) aonde está o arquivo de Backup e pressione a tecla ENTER . (exemplo : mysql –h mysql5.inetweb.com.br –u inetweb –p -D base_de_dados < c:\backup )



###Dicas 02
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

###Macros que podem ser adicionados ao PgaAdmin

--LOCALIZAR FUNCTION

SELECT 
 pc.oid AS prooid,
 proname,
 lanname as prolanguage,
 pg_catalog.format_type(prorettype, NULL) as proresult,
 prosrc,
 probin,
 proretset,
 proisstrict,
 provolatile,
 prosecdef,
 pg_catalog.oidvectortypes(pc.proargtypes) AS proarguments,
 proargnames AS proargnames,
 pg_catalog.obj_description(pc.oid, 'pg_proc') AS procomment
FROM pg_catalog.pg_proc pc, pg_catalog.pg_language pl
WHERE (TRIM(LOWER(a.attname ))= '$SELECTION$'
    OR TRIM(UPPER(a.attname ))= '$SELECTION$')
 AND 
pc.prolang = pl.oid


--DESCOBRE DESCRICAO LABEL DO CAMPO

select db_syscampo.codcam,db_syscampo.nomecam,
       db_syscampo.conteudo,
       db_syscampo.descricao,db_syscampo.rotulo,
       db_sysarquivo.nomearq,
       db_sysarquivo.descricao,
       db_sysarquivo.rotulo,
       db_sysmodulo.nomemod as modulo,
       db_sysmodulo.descricao
from db_syscampo
inner join db_sysarqcamp on db_syscampo.codcam = db_sysarqcamp.codcam
inner join db_sysarquivo on db_sysarqcamp.codarq = db_sysarquivo.codarq
inner join db_sysarqmod on db_sysarqmod.codarq = db_sysarquivo.codarq
inner join db_sysmodulo on db_sysmodulo.codmod = db_sysarqmod.codmod
where db_syscampo.nomecam = 'e60_numerol';


--DESCOBRE DE QUAL TABELA A CONSTRAINT PERTENCE

SELECT n.nspname as sckema,
r.relname as tabela_pai,
conname, conrelid::pg_catalog.regclass as tabela_filha,
  pg_catalog.pg_get_constraintdef(c.oid, true) as condef
FROM pg_catalog.pg_constraint c
  JOIN pg_catalog.pg_class r ON r.oid = c.confrelid
  JOIN pg_catalog.pg_namespace n ON n.oid = r.relnamespace
where c.conname='orcreserva_ae_coddot_fk'


--LIMIT 10

select * from $SELECTION$ LIMIT 10

--SEQUENCIA

SELECT * FROM information_schema.sequences
 WHERE upper(sequence_name) like '%$SELECTION$%';


--LISTA CAMPOS DE UMA TABELA SEM TIPO

SELECT a.relname AS Tabela, b.attname AS Campo
FROM pg_class a
JOIN pg_attribute b ON (b.attrelid = a.relfilenode)
WHERE  b.attstattarget = -1 AND
	(TRIM(LOWER(a.relname))= '$SELECTION$'
       OR TRIM(UPPER(a.relname))= '$SELECTION$');

--LOCALIZA CAMPO NA TABELA

SELECT a.relname AS Tabela, b.attname AS Campo
FROM pg_class a
JOIN pg_attribute b ON (b.attrelid = a.relfilenode)
WHERE  b.attstattarget = -1 AND  
    (TRIM(LOWER(b.attname))= '$SELECTION$'
    OR TRIM(UPPER(b.attname))= '$SELECTION$');


--ESTRUTURA TABELA

SELECT table_catalog as banco,table_schema as schema,table_name as tabela,
       ordinal_position as posicao,
       column_name as campo,is_nullable,data_type as tipo,
       character_maximum_length as tamanho
 FROM information_schema.columns
 WHERE TRIM(LOWER(table_name))= '$SELECTION$'
    OR TRIM(UPPER(table_name))= '$SELECTION$'


--DESCOBRE PK DE UMA TABELA

SELECT a.attname AS chave_pk
FROM pg_class c
  INNER JOIN pg_attribute a ON (c.oid = a.attrelid)
  INNER JOIN pg_index i ON (c.oid = i.indrelid)
WHERE
  i.indkey[0] = a.attnum AND
  i.indisprimary = 't' AND
  (TRIM(LOWER(c.relname))= '$SELECTION$'
    OR TRIM(UPPER(c.relname))= '$SELECTION');

--TRIGGERS NA TABELA

select trigger_schema as "Schema",event_object_table as "tabela",
      trigger_name as "trigger",event_manipulation as "evento",
      action_timing as "modificador" ,
      action_statement as "Function"
FROM information_schema.triggers
WHERE (TRIM(LOWER(event_object_table))= '$SELECTION$'
    OR TRIM(UPPER(event_object_table))= '$SELECTION$');


--DESCRIÇÃO TABELA

select trim(db_sysarquivo.nomearq) as nomearq,
       trim(db_sysarquivo.descricao) as descricao
from db_sysarquivo
where (TRIM(LOWER(nomearq))= '$SELECTION$'
    OR TRIM(UPPER(nomearq))= '$SELECTION$');


--LOCALIZA CAMPO NA TABELA

select c.schemaname||'.'||
c.relname as schema_tabela,
a.attname as "Campo",
pg_catalog.format_type(a.atttypid, a.atttypmod) as "Tipo"  
from pg_catalog.pg_attribute a
inner join pg_stat_user_tables c on a.attrelid = c.relid
WHERE (TRIM(LOWER(a.attname ))= '$SELECTION$'
    OR TRIM(UPPER(a.attname ))= '$SELECTION$')
order by c.relname, a.attname


--USUARIO CONECTADOS

select datname,
pid,
usename,
application_name,
client_addr,
client_hostname,
backend_start
from pg_stat_activity




###__________________________________________
###Firebird

###Principais Funções p/ Manipular Datas

select sysdate() as data_completa,
Current_Date as data_sem_hora,Current_Time as so_horas,
extract(day from current_date)as dia,
extract(month from current_date)as mes,
extract(year from current_date)as ano,
extract(minute from Current_Time)as minuto,
extract(second from Current_Time)as segundo,
cast((current_timestamp + (1.0/24.0)) as timestamp) soma_1_hora,
case when EXTRACT(WEEKDAY FROM current_date)=0 then 'DOMINGO'
     when EXTRACT(WEEKDAY FROM current_date)=2 then 'SEGUNDA'
     when EXTRACT(WEEKDAY FROM current_date)=2 then 'TERÇA'
     when EXTRACT(WEEKDAY FROM current_date)=3 then 'QUARTA'
     when EXTRACT(WEEKDAY FROM current_date)=4 then 'QUINTA'
     when EXTRACT(WEEKDAY FROM current_date)=5 then 'SEXTA'
     else 'SÁBADO' end semana,
current_date-EXTRACT(DAY FROM current_date) + 1 primeiro_dia_mes,
current_date - EXTRACT(DAY FROM current_date) + 32 -
EXTRACT(DAY FROM current_date - EXTRACT(DAY FROM current_date) + 32) as ultimo_dia_mes,
current_date - EXTRACT(DAY FROM current_date) + 33 -
EXTRACT(DAY FROM current_date - EXTRACT(DAY FROM current_date) + 32)as primeiro_dia_proximo_mes
from RDB$Database


###Primeiro e último dia de uma data

select cast(:DataInicial as timestamp) - EXTRACT(DAY FROM cast(:DataInicial as timestamp)) + 33 -
EXTRACT(DAY FROM cast(:DataInicial as timestamp)- EXTRACT(DAY FROM cast(:DataInicial as timestamp)) + 32),
cast(:DataInicial as timestamp) - EXTRACT(DAY FROM cast(:DataInicial as timestamp)) + 32 -
EXTRACT(DAY FROM cast(:DataInicial as timestamp) - EXTRACT(DAY FROM cast(:DataInicial as timestamp)) + 32) as ultimo dia
from TabelaMalaca
