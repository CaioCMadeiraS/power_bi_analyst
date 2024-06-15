Descrição do desafio módulo 3 – Processamento de Dados Simplificado com Power BI

1. Criação de uma instância na Azure para MySQL

2. Criar o Banco de dados com base disponível no github

3. Integração do Power BI com MySQL no Azure

4. Verificar problemas na base a fim de realizar a transformação dos dados

---------------------------------------------------------------------------------------------------------------------------------
Criação de banco de dados MySQL usando como base "script_bd_company.sql".

Mudei o nome da tabela departament para department, respeitando a nomenclatura correta em inglês.

Os comandos de "drop" como "alter table dept_locations drop fk_dept_locations;" já haviam sido aplicados às tabelas e, portanto, retornaram erro.

A constraint "fk_dept_locations" é adicionada duas vezes no script e também retorna erro.

No script também se encontra "drop table dependent;" antes de "create table dependent", o que não segui, porque não faria sentido. 

Inseri os dados a partir de "inserção_de_dados_e_queries_sql.sql".

O uso de "select Ssn, count(Essn) from employee e, dependent d where (e.Ssn = d.Essn);" exigiu um "group by", de forma que podem ser usados "group by e.Ssn;" ou "group by d.Essn;". Nesse caso específico, retornam o mesmo resultado.

Os seguintes erros são apresentados quando, após inserir "Values" no banco de dados, tenta-se atualizar todos os dados das tabelas de uma vez no power BI a partir da página inicial (opção "atualizar").
   
     azure_company department
Um erro ao carregar uma tabela anterior cancelou o carregamento.

     azure_company dependent
A coluna "Essn" na tabela "azure_company dependent" contém um valor "123456789" duplicado e isso não é permitido para colunas de um lado do relacionamento muitos para um ou para colunas que estão sendo usadas como a chave primária de uma tabela.

     azure_company dept_locations
Erro do OLE DB ou do ODBC : Exceção de HRESULT: 0x80040E4E.

     azure_company employee
Erro do OLE DB ou do ODBC : Exceção de HRESULT: 0x80040E4E.

     azure_company project
A coluna "Dnum" na tabela "azure_company project" contém um valor "5" duplicado e isso não é permitido para colunas de um lado do relacionamento muitos para um ou para colunas que estão sendo usadas como a chave primária de uma tabela.

     azure_company works_on
Erro do OLE DB ou do ODBC : Exceção de HRESULT: 0x80040E4E.

Para lidar com isto, é preciso usar a opção transformar dados, portanto seguindo um passoa a passo Extract-Transform-Load. Utilizando esta opção, os dados podem ser atualizados de acordo com o banco de dados usando power query.
