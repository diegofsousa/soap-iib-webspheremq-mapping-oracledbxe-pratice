# soap-iib-webspheremq-mapping-oracledbxe-pratice

> Laboratório de SOA com IBM Integration BUS, WebSphereMQ e Oracle XE

## Configurando o Oracle XE com o IBB

Oracle XE é um sistema de banco de dados gratuito para desenvolvimento, distribuição e uso comercial.

Depois de instalado, deve-se criar um usuário:

```sql
alter session set "_ORACLE_SCRIPT"=true;

CREATE USER usuario
IDENTIFIED BY senha;
  
GRANT create session TO usuario;
GRANT create table TO usuario;
GRANT create view TO usuario;
GRANT create any trigger TO usuario;
GRANT create any procedure TO usuario;
GRANT create sequence TO usuario;
GRANT create synonym TO usuario;

ALTER USER usuario quota unlimited on SYSTEM;
ALTER USER usuario quota unlimited on USERS;
```

Logo em seguida, criar uma conexão para este usuário recém-criado. (pode ser pela interface gráfica do Oracle SQL Developer)

Pelo IBM Integration Console a conexão com o banco faz link com o IBB através dos seguintes comandos:

```
mqsicreateconfigurableservice <Nome do Nó> -c JDBCProviders -o xe -n connectionUrlFormat,connectionUrlFormatAttr1,description,jarsURL,portNumber,
securityIdentity,serverName,type4DatasourceClassName,type4DriverClassName -v "jdbc:oracle:thin:[user]/[password]@[serverName]:[portNumber]:[connectionUrlFormatAttr1]
,"XE","default_none","<Caminho do driver ODBC fornecido pelo Oracle XE>",1521,"XE_SecurityId","localhost","oracle.jdbc.xa.client.OracleXADataSource",
"oracle.jdbc.OracleDriver" 
```

```
mqsisetdbparms <Nome do Nó> -n jdbc::XE_SecurityId -u <Usuário do banco> -p <Senha do usuário>
```

```
mqsistop <Nome do Nó>
mqsistart <Nome do Nó>
```

Substituir:

- Nome do Nó
- Usuário do banco
- Senha do usuário
- Caminho do driver ODBC fornecido pelo Oracle XE

## Exemplo de tabela usada no laboratório

```sql
CREATE SCHEMA AUTHORIZATION usuario
     CREATE TABLE pessoa
        ( nome varchar2(50) not null,
          sobrenome varchar2(50) not null,
          estadoCivil char(1) not null,
          sexo char(1) not null,
          email varchar2(50) not null
         );
```
