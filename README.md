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
Baixe ou clone o código-fonte do projeto em https://github.com/isaccanedo/node-mssql-crud-api
Instale todos os pacotes npm necessários executando npm install ou npm i na linha de comando na pasta raiz do projeto (onde o package.json está localizado).
Atualize as credenciais do banco de dados em /config.json para se conectar à sua instância do MS SQL Server e verifique se o servidor MSSQL está em execução.
Inicie a API executando npm start (ou npm run dev to start with nodemon) na linha de comando na pasta raiz do projeto, você deverá ver a mensagem Server listen on port 4000.
Siga as instruções abaixo para testar com o Postman ou conecte-se com um dos exemplos de aplicativos de página única disponíveis (React ou Angular).
```
