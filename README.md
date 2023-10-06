# Desafio 2 Power BI - Dio: Processando e Transformando Dados com Power BI.

## Algumas correções que precisaram ser realizadas para resolver e evitar erros:

Na linha 63 do arquivo 'script_bd_company.sql' foi necessario alterar o comando. Adicionando foreign key para realizar o drop, ficando:

  'alter table dept_locations drop foreign key fk_dept_locations;'.

No arquivo 'insercao_de_dados_e_queries_sql.sql' o comando na primeira linha foi atualizado para 'use azure_company;';

no comando de inserção de valores na tabela 'employee', foi necessario modificar para 'NULL' todos os campos relativos a 'Super_ssn' para evitar o erro 'ERROR 1452 (23000)';

em alguns comandos de consulta o caracter U+2019 foi substituido por aspas simples.

## Transformação de dados:

Remoção de colunas adicionadas pelo Power BI;

todas as ocorrencias da coluna 'Dnumber', que se refere ao numero do departamento, foram modificados para 'texto', para tornar possivel a correlação da informação nos gráficos;

'Salary' na tabela 'employee' foi modificado para o tipo 'decimal fixo';

Os valores na coluna 'Super_ssn', que ficaram em 'null', foram preenchidos utilizando MySQL Workbench, baseando-se nos dados previamente fornecidos e por abstração;

a coluna 'Address' foi dividida primeiro em 'digito e não digito', para separar numero do resto do endereço, gerando a nova coluna renomeada para 'Anumber'; após a nova coluna 'Address' foi dividida duas vezes por 'delimitador na extremidade direita', separando em novas colunas e renomendo-as para 'City' e 'State'; por fim, o delimitador '-' foi removido da coluna 'Address' e o valor 'FireOak' foi mudado para 'Fire Oak'.

Na tabela 'project', a coluna 'Pnumber' foi alterada para o tipo 'texto';

na tabela 'works_on', a coluna 'Pno' foi alterada para o tipo 'texto', e a coluna 'Hours' alterada para 'numero decimal'.

Ao juntar as informações Employee X Departament, deve-se mesclar a consulta, gerando uma nova tabela, assim será possivel limitar quais informações correlacionar, tornando mais simples a limpeza de dados da nova relação, para permanecer apenas as informações desejadas. Com a combinação de consultas, todas as informações contidas nas tabelas selecionadas seriam combinadas em uma nova tabela, podendo resultar em vários ocorrencias indesejadas por haver discrepancia nas informações combinadas.

### O mesmo tipo de mescla foi aplicado para correlacionar as seguintes informações:
Employee X Manager, agrupando Managers por numero de employees; 
Departament X Location, que neste caso faz-se necessario por haver o mesmo tipo de departamento para localizações diferentes;
Departament X project;
Projects X employee, agrupando numero de employee por projeto;
Hours X project, agrupando a quantidade de horas gastas em cada projeto.

