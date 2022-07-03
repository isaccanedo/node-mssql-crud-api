# node-mssql-crud-api

Node.js + MS SQL Server - CRUD API Example

# Ferramentas necessárias para este tutorial
Para seguir as etapas deste tutorial, você precisará do seguinte:
```
1 - Node.js & npm - inclui o runtime do Node.js, ferramentas de linha de comando e 
gerenciador de pacotes, instale-o em https://nodejs.org/;

2 - MS SQL Server - você precisará acessar a instância do SQL Server em execução 
para a API se conectar, ela pode ser remota (por exemplo, Azure, AWS etc) ou em 
sua máquina local. A edição Express do SQL Server está disponível gratuitamente 
em https://www.microsoft.com/sql-server/sql-server-downloads. Você também pode 
executá-lo em um contêiner do Docker, as imagens oficiais do docker para 
SQL Server estão disponíveis em https://hub.docker.com/_/microsoft-mssql-server;

3 - Um editor de código para visualizar e editar o código da API, não 
importa qual, pessoalmente eu uso o Visual Studio Code que é um editor 
gratuito que roda em Windows, Mac e Linux, você pode baixá-lo em 
https://code. visualstudio. com/.
```

# Execute a API CRUD Node + MSSQL localmente
```
1 - Baixe ou clone o código-fonte do projeto em https://github.com/isaccanedo/node-mssql-crud-api;

2 - Instale todos os pacotes npm necessários executando npm install ou npm i na linha de comando na pasta 
raiz do projeto (onde o package.json está localizado);

3 - Atualize as credenciais do banco de dados em /config.json para se conectar à sua instância do MS SQL 
Server e verifique se o servidor MSSQL está em execução;

4 - Inicie a API executando npm start (ou npm run dev to start with nodemon) na linha de comando na pasta 
raiz do projeto, você deverá ver a mensagem Server listen on port 4000;

5 - Siga as instruções abaixo para testar com o Postman ou conecte-se com um dos exemplos de aplicativos de 
página única disponíveis (React ou Angular).
```

### Sequela a sincronização do modelo
Na inicialização, você também deve ver a saída como abaixo da sincronização do modelo Sequelize que é executada no wrapper do banco de dados MSSQL, ela mostra a criação e sincronização da tabela Users com base no modelo de usuário do Sequelize.

```
Executing (default): SELECT TABLE_NAME, TABLE_SCHEMA FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_TYPE = 'BASE TABLE' AND TABLE_NAME = N'Users' AND TABLE_SCHEMA = N'dbo'
Executing (default): SELECT c.COLUMN_NAME AS 'Name', c.DATA_TYPE AS 'Type', c.CHARACTER_MAXIMUM_LENGTH AS 'Length', c.IS_NULLABLE as 'IsNull', COLUMN_DEFAULT AS 'Default', pk.CONSTRAINT_TYPE AS 'Constraint', COLUMNPROPERTY(OBJECT_ID(c.TABLE_SCHEMA+'.'+c.TABLE_NAME), c.COLUMN_NAME, 'IsIdentity') as 'IsIdentity', CAST(prop.value AS NVARCHAR) AS 'Comment' FROM INFORMATION_SCHEMA.TABLES t INNER JOIN INFORMATION_SCHEMA.COLUMNS c ON t.TABLE_NAME = c.TABLE_NAME AND t.TABLE_SCHEMA = c.TABLE_SCHEMA LEFT JOIN (SELECT tc.table_schema, tc.table_name,  cu.column_name, tc.CONSTRAINT_TYPE  FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS tc  JOIN INFORMATION_SCHEMA.KEY_COLUMN_USAGE  cu  ON tc.table_schema=cu.table_schema and tc.table_name=cu.table_name  and tc.constraint_name=cu.constraint_name  and tc.CONSTRAINT_TYPE='PRIMARY KEY') pk  ON pk.table_schema=c.table_schema  AND pk.table_name=c.table_name  AND pk.column_name=c.column_name  INNER JOIN sys.columns AS sc ON sc.object_id = object_id(t.table_schema + '.' + t.table_name) AND sc.name = c.column_name LEFT JOIN sys.extended_properties prop ON prop.major_id = sc.object_id AND prop.minor_id = sc.column_id AND prop.name = 'MS_Description' WHERE t.TABLE_NAME = 'Users'
Executing (default): SELECT constraint_name = OBJ.NAME, constraintName = OBJ.NAME, constraintCatalog = 'node-mssql-crud-api', constraintSchema = SCHEMA_NAME(OBJ.SCHEMA_ID), tableName = TB.NAME, tableSchema = SCHEMA_NAME(TB.SCHEMA_ID), tableCatalog = 'node-mssql-crud-api', columnName = COL.NAME, referencedTableSchema = SCHEMA_NAME(RTB.SCHEMA_ID), referencedCatalog = 'node-mssql-crud-api', referencedTableName = RTB.NAME, referencedColumnName = RCOL.NAME FROM sys.foreign_key_columns FKC INNER JOIN sys.objects OBJ ON OBJ.OBJECT_ID = FKC.CONSTRAINT_OBJECT_ID INNER JOIN sys.tables TB ON TB.OBJECT_ID = FKC.PARENT_OBJECT_ID INNER JOIN sys.columns COL ON COL.COLUMN_ID = PARENT_COLUMN_ID AND COL.OBJECT_ID = TB.OBJECT_ID INNER JOIN sys.tables RTB ON RTB.OBJECT_ID = FKC.REFERENCED_OBJECT_ID INNER JOIN sys.columns RCOL ON RCOL.COLUMN_ID = REFERENCED_COLUMN_ID AND RCOL.OBJECT_ID = RTB.OBJECT_ID WHERE TB.NAME ='Users'
Executing (default): ALTER TABLE [Users] ALTER COLUMN [email] NVARCHAR(255) NOT NULL;
Executing (default): ALTER TABLE [Users] ALTER COLUMN [passwordHash] NVARCHAR(255) NOT NULL;
Executing (default): ALTER TABLE [Users] ALTER COLUMN [title] NVARCHAR(255) NOT NULL;
Executing (default): ALTER TABLE [Users] ALTER COLUMN [firstName] NVARCHAR(255) NOT NULL;
Executing (default): ALTER TABLE [Users] ALTER COLUMN [lastName] NVARCHAR(255) NOT NULL;
Executing (default): ALTER TABLE [Users] ALTER COLUMN [role] NVARCHAR(255) NOT NULL;
Executing (default): ALTER TABLE [Users] ALTER COLUMN [createdAt] DATETIMEOFFSET NOT NULL;
Executing (default): ALTER TABLE [Users] ALTER COLUMN [updatedAt] DATETIMEOFFSET NOT NULL;
Executing (default): EXEC sys.sp_helpindex @objname = N'[Users]';
```

# Teste a API CRUD do Node + SQL Server com o Postman
O Postman é uma ótima ferramenta para testar APIs, você pode baixá-lo em https://www.postman.com/downloads.

Abaixo estão as instruções sobre como usar o Postman para realizar as seguintes ações:
```
- Criar um novo usuário;
- Recuperar uma lista de todos os usuários;
- Recuperar um usuário por id;
- Atualizar um usuário;
- Excluir um usuário.
```

# Como criar um novo usuário com o Postman
Para criar um novo usuário com a API CRUD, siga estas etapas:

```
1 - Abra uma nova guia de solicitação clicando no botão de adição (+) no final das guias;
2 - Altere o método HTTP para POST com o seletor suspenso à esquerda do campo de entrada de URL;
3 - No campo URL insira o endereço para a rota de usuários de sua API local - http://localhost:4000/users;
4 - Selecione a guia Corpo abaixo do campo URL, altere o botão de opção do tipo de corpo para bruto e altere o seletor suspenso de formato para JSON;
5 - Insira um objeto JSON contendo as propriedades de usuário necessárias na área de texto do corpo, por exemplo:
```

```
{
    "title": "Mr",
    "firstName": "George",
    "lastName": "Costanza",
    "role": "User",
    "email": "george@costanza.com",
    "password": "george-likes-spicy-chicken",
    "confirmPassword": "george-likes-spicy-chicken"
}
```
Clique no botão Enviar, você deverá receber uma resposta "200 OK" com a mensagem "Usuário criado" no corpo da resposta.

# Como recuperar uma lista de todos os usuários com o Postman

### Para obter uma lista de todos os usuários da API Node + MSSQL CRUD, siga estas etapas:

```
1 - Abra uma nova guia de solicitação clicando no botão de adição (+) no final das guias;
2 - Altere o método HTTP para GET com o seletor suspenso à esquerda do campo de entrada de URL;
3 - No campo URL insira o endereço para a rota de usuários de sua API local - http://localhost:4000/users;
4 - Clique no botão Enviar, você deverá receber uma resposta "200 OK" contendo uma matriz JSON com todos os registros de usuário no sistema;
```

# Como recuperar um usuário por id com o Postman

### Para obter um usuário específico por id da API Node + MSSQL CRUD siga estas etapas:
```
1 - Abra uma nova guia de solicitação clicando no botão de adição (+) no final das guias;
2 - Altere o método HTTP para GET com o seletor suspenso à esquerda do campo de entrada de URL;
3 - No campo URL digite o endereço para a rota /users/{id} com o id do usuário que você deseja recuperar, por exemplo - http://localhost:4000/users/1;
4 - Clique no botão Enviar, você deverá receber uma resposta "200 OK" contendo um objeto JSON com os detalhes do usuário especificados.
```

# Como atualizar um usuário com o Postman
### Para atualizar um usuário com a API CRUD, siga estas etapas:

```
1 - Abra uma nova guia de solicitação clicando no botão de adição (+) no final das guias;
2 - Altere o método HTTP para PUT com o seletor suspenso à esquerda do campo de entrada de URL;
3 - No campo URL digite o endereço para a rota /users/{id} com o id do usuário que você deseja atualizar, por exemplo - http://localhost:4000/users/1;
4 - Selecione a guia Corpo abaixo do campo URL, altere o botão de opção do tipo de corpo para bruto e altere o seletor suspenso de formato para JSON;
5 - Insira um objeto JSON na área de texto Corpo contendo as propriedades que você deseja atualizar, por exemplo, para atualizar o nome e o sobrenome:
```

```
{
    "firstName": "Art",
    "lastName": "Vandelay"
}
```

Clique no botão Enviar, você deverá receber uma resposta "200 OK" com a mensagem "Usuário atualizado" no corpo da resposta.



