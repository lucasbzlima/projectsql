# projectsql

USE exer01 -- Selecionar o banco que deseja trabalhar 

SELECT * FROM SYS.DATABASES --Selecionar todos os bancos de dados existentes

SELECT * FROM SYS.TABLES --Selecionar todas as tabelas existentes


/*-------------------------------------------------------------------------*/


/* Modelagem Básica */

/*CRIAR BANCO DE DADOS */
CREATE DATABASE exer01

/*CADASTRDO DE CLIENTE (NOME, CPF, EMAIL, TELEFONE, ENDEREÇO, SEXO)*/

CREATE TABLE CLIENTE(
    ID_CLIENTE INT PRIMARY KEY,
    NOME VARCHAR(30),
    SEXO CHAR(1),
    EMAIL VARCHAR(30),
    CPF CHAR(11) UNIQUE,
    TELEFONE VARCHAR(30),
    ENDERECO VARCHAR(100)
);


CREATE TABLE FUNCIONARIO (
    ID_FUNCIONARIO INT IDENTITY(1,1) PRIMARY KEY,
    NOME VARCHAR (100),
    SEXO VARCHAR (10),
    EMAIL VARCHAR (100),
    DEPARTAMENTO INT (100),
    ADMISSAO DATE,
    SALARIO INTEGER,
    CARGO VARCHAR(100),
    ID_REGIAO INT,
    FOREIGN KEY (ID_REGIAO) REFERENCES REGIAO(ID_REGIAO)
);


CREATE TABLE CARGO (
    ID_CARGO INT IDENTITY(1,1) PRIMARY KEY,
    NOME VARCHAR(100)

);

CREATE TABLE LIVRO (
    ID INT IDENTITY(1,1) PRIMARY KEY,
    LIVRO VARCHAR (100),
    AUTOR VARCHAR (100),
    SEXO CHAR (1),
    PAGINAS INT,
    EDITORA VARCHAR (30),
    VALOR DECIMAL(10,2),
    UF CHAR (2),
    ANO DATE
);


CREATE TABLE REGIAO (
    ID_REGIAO INT IDENTITY(1,1) PRIMARY KEY,
    ESTADO_EXT VARCHAR (100),
    ESTADO CHAR(2)
);

CREATE TABLE DEPARTAMENTO (
    ID_DEPARTAMENTO INT IDENTITY(1,1) PRIMARY KEY,
    NOME VARCHAR(100),
    SALA VARCHAR(100)
);


CREATE TABLE VENDEDOR(
    ID_VENDEDOR INT IDENTITY(1,1) PRIMARY KEY,
    NOME VARCHAR (100),
    SEXO CHAR (1),
    ENDERECO VARCHAR (100),
    CEP CHAR(8),
    TELEFONE1 VARCHAR(30),
    TELEFONE2 VARCHAR(30),
    EMAIL VARCHAR (100),
    ID_REGIAO INT,
    FOREIGN KEY (ID_REGIAO) REFERENCES REGIAO(ID_REGIAO)
)


/*-------------------------------------------------------------------------*/

/*INSERIR DADOS NA TABELA DE CLIENTE*/

INSERT INTO CLIENTE (ID, NOME, SEXO, EMAIL, CPF, TELEFONE, ENDERECO)
VALUES 
(2,'Amanda', 'F', 'mand_09@hotmail.com', 85746327943, 85977746533, 'Av: Joaquim Tavora'),
(3,'Fernando', 'M', 'ferd-87@gmail.com', 32516743298, 85987546322, 'Rua: 658'),
(4,'João', 'M', 'jovini_22@hotmail.com', 12658436798, 85977643412, 'Rua: Tenente Almeida'),
(5,'Ana', 'F', 'anaselve@gmail.com',     96323567843, 85986945732, 'Rua: 834');

/*INSERIR DADOS NA TABELA DE LIVRO*/

INSERT INTO LIVRO(LIVRO,AUTOR,SEXO,PAGINAS,EDITORA,VALOR,UF,ANO)
VALUES ('O poder da Mente', 'Clara Mafra', 'F', 120, 'Continental', 56, 'SP', '2017/02/04');

/*INSERIR DADOS NA TABELA DE FUNCIONARIO*/

INSERT INTO FUNCIONARIO (NOME, SEXO, EMAIL,  ADMISSAO, SALARIO, ID_CARGO, ID_REGIAO, ID_DEPARTAMENTO)
VALUES ('Ana Leticia Maia', 'Feminino', 'anelet@hotmail.com', '2023/02/01', 5700.00, 2, 11, 3)


/*INSERIR DADOS NA TABELA DE DEPARTAMENTO*/

INSERT INTO DEPARTAMENTO (NOME, SALA) VALUES ('Financeiro','6'), ('Tesouraria','2'), ('Recepção','null'), ('Direção','1');


/*INSERIR DADOS NA TABELA VENDEDOR*/


INSERT INTO VENDEDOR (NOME, SEXO, ENDERECO, NUMERO, CEP, BAIRRO, TEL1, TEL2, EMAIL, ID_REGIAO)
VALUES ('Alfredo Tavares','M', 'Rua 432', 200, 60122233, 'Conjunto-Ceará', 85988557633, null, 'alftv@hotmail.com',5);
INSERT INTO VENDEDOR (NOME, SEXO, ENDERECO, NUMERO, CEP, BAIRRO, TEL1, TEL2, EMAIL, ID_REGIAO)
VALUES ('João Abides','M', 'Av. Dom Luis', 3000, 60555677, 'Aldeota', 85999976543, null, 'joab@gmail.com',5);
INSERT INTO VENDEDOR (NOME, SEXO, ENDERECO, NUMERO, CEP, BAIRRO, TEL1, TEL2, EMAIL, ID_REGIAO)
VALUES ('Kaio Manfra','M', 'Av. Dom Quitino', 345, 597643154, 'Sapiranga', 85988764533, null, 'kkoit@gmail.com',5);

INSERT INTO CARGO VALUES ('Júnior')

/*-------------------------------------------------------------------------*/

ALTER TABLE FUNCIONARIO
DROP COLUMN DEPARTAMENTO;


/*INCLUIR COLUNA NA TABELA CLIENTE*/


/*ATUALIZANDO A LINHA E COLUNA DA TABELA*/

ALTER TABLE CLIENTE
ADD NUMERO VARCHAR(8), BAIRRO VARCHAR(15), CEP VARCHAR(8);UPDATE CLIENTE 
SET NUMERO = '436', 
    BAIRRO='Conjunto Ceará', 
    CEP= 60544237
WHERE ID =5

ALTER TABLE CLIENTE
ALTER COLUMN VALORES DECIMAL(10,2);

/*Comando para alterar a coluna da tabela LIVRO*/
ALTER TABLE CLIENTE
ALTER COLUMN VALORES DECIMAL(10,2);

ALTER TABLE FUNCIONARIO
ADD CONSTRAINT ID_DEPARTAMENTO FOREIGN KEY (ID_DEPARTAMENTO) REFERENCES DEPARTAMENTO(ID_DEPARTAMENTO); 

ALTER TABLE CLIENTE
ADD CONSTRAINT ID_REGIAO FOREIGN KEY (ID_REGIAO) REFERENCES REGIAO(ID_REGIAO);

/*-------------------------------------------------------------------------*/


UPDATE CLIENTE 
SET EMAIL='luka@hotmail.com' WHERE ID=1

UPDATE FUNCIONARIO
SET ID_CARGO = '2'
WHERE ID_FUNCIONARIO =4

UPDATE CLIENTE
SET ID_REGIAO = '9'
WHERE ID = 6

/*-------------------------------------------------------------------------*/

SELECT * FROM VENDEDOR;


/*Alias Colunas*/
SELECT ENDERECO AS LOGRADOURO, CPF, EMAIL FROM CLIENTE;

/*CARACTER CORINGA % -> QUALQUER COISA*/
SELECT BAIRRO FROM CLIENTE
WHERE BAIRRO LIKE '%a'

/*Alias Colunas*/
SELECT ENDERECO AS LOGRADOURO, CPF, EMAIL FROM CLIENTE;

SELECT * FROM CLIENTE WHERE SEXO='F'
/* 1 - Trazer todos os dados*/
SELECT * FROM LIVRO
/* 2 - Trazer o nome do livro e o nome da editora*/
SELECT LIVRO, EDITORA FROM LIVRO
/* 3 - Trazer o nome do livro e a UF dos livros publicados por autores do sexo masculino */
SELECT LIVRO, UF, SEXO FROM LIVRO WHERE SEXO='M'
/* 4 - Trazer o nome do livro e o número de páginas dos livros publicados por autores do sexo femino*/
SELECT LIVRO, PAGINAS, AUTOR, SEXO FROM LIVRO WHERE SEXO='F'
/* 5 - Trazer os valores dos livros das editiras de São Paulo*/
SELECT LIVRO, VALOR FROM LIVRO
/* 6 - Trazer os dados dos autores do sexo masculino que tiveram livros publicados por São Paulo
ou Rio de Janeiro (Questão Desafio)*/
SELECT AUTOR, SEXO FROM LIVRO --OR -> Para que a saida da query seja verdadeira, basta que apenas uma condicção seja verdadeira
WHERE SEXO='M' AND (UF='SP' OR UF='RJ'); --AND -> Para que a saída seja verdadeira todas as condições precisam ser verdadeiras.


/* OR - OU */
SELECT * FROM CLIENTE

SELECT NOME, SEXO, ENDERECO FROM CLIENTE
WHERE SEXO = 'M' OR ENDERECO LIKE '%RJ';

/* AND - E */
SELECT NOME, SEXO, ENDERECO FROM CLIENTE
WHERE SEXO = 'M' AND ENDERECO LIKE 'RJ';



-- OR traz todo mundo com pelo menos uma das duas condições
-- AND Traz apenas o rREGIAO


/*Junção de tabelas CLIENTE E REGIAO*/
SELECT C.ID_CLIENTE, C.NOME, C.SEXO, R.ESTADO
FROM CLIENTE C 
INNER JOIN REGIAO R  
ON C.ID_REGIAO = R.ID_REGIAO
WHERE C.SEXO = 'F' AND R.ESTADO LIKE 'M%';


/*Comandos COMMIT E ROLLBACK*/
SELECT * FROM CLIENTE
WHERE NOME = 'LIVIA'
AND sexo = 'F'



/*WHERE = SELEÇÃO*/


/*Criando POROCEDURE para inserir dados na tabela departamento*/
SELECT * FROM DEPARTAMENTO;

SELECT * FROM CLIENTE
WHERE ID_CLIENTE IN (3,5,6,7);

/*-------------------------------------------------------------------------*/

create procedure insere_departamento ( @dep_nome VARCHAR(100), @dep_sala VARCHAR(100)))
AS
BEGIN
    insert into departamento(nome,sala)
    values (@dep_nome, @dep_sala);

    select nome, sala from departamento;
end;


EXEC insere_departamento 'Caixa', '5';


/*-------------------------------------------------------------------------*/


INSERT INTO VENDEDOR (NULL, 'Carlos Alberto', 'M','Av. Padre Valdevino')


/*-------------------------------------------------------------------------*/

/*Aqui foi um desafio que fiz no dia a dia de um Analista de dados*/

/* Adicionei uma FOREIGN KEY para fazer referencia a tabela REGIAO */
ALTER TABLE LIVRO
ADD CONSTRAINT FK_LIVRO_REGIAO FOREIGN KEY (ID_REGIAO) REFERENCES REGIAO(ID_REGIAO); 

ALTER TABLE LIVRO
ADD ID_REGIAO INT;

/*Como já tinha um campo (UF) criando na tabela livro com dados antigos... Eu fiz
a atualização com a tabela REGIAO*/


UPDATE LIVRO SET ID_REGIAO = 18 WHERE UF='RJ';
UPDATE LIVRO SET ID_REGIAO = 24 WHERE UF='SP';
UPDATE LIVRO SET ID_REGIAO = 7  WHERE UF='ES';

/*-------------------------------------------------------------------------*/

SELECT * FROM LIVRO

CREATE TABLE AUTOR(
    ID_AUTOR INT IDENTITY (1,1) PRIMARY KEY,
    AUTOR VARCHAR(100),
    SEXO CHAR(1),
    FORMACAO VARCHAR(100),
    NASCIMENTO DATE,   
)


CREATE TABLE EDITORA (
    ID_EDITORA INT IDENTITY (1,1) PRIMARY KEY,
    EDITORA VARCHAR(100),
    ENDERECO VARCHAR(100),
    NUMERO VARCHAR (30),
    BAIRRO VARCHAR(100),
    CEP CHAR(8),
    TEL1 VARCHAR(30),
    TEL2 VARCHAR(30),
    EMAIL VARCHAR (100),
    ID_REGIAO INT,
    FOREIGN KEY (ID_REGIAO) REFERENCES REGIAO(ID_REGIAO) 
)


ALTER TABLE LIVRO
ADD CONSTRAINT FK_LIVRO_REGIAO FOREIGN KEY (ID_REGIAO) REFERENCES REGIAO(ID_REGIAO); 

ALTER TABLE LIVRO DROP CONSTRAINT FK_LIVRO_EDITORA
ALTER TABLE LIVRO DROP COLUMN SEXO, ID_AUTOR;



ALTER TABLE LIVRO ADD ID_EDITORA INT, ID_AUTOR INT;

ALTER TABLE LIVRO
ADD CONSTRAINT FK_LIVRO_EDITORA FOREIGN KEY (ID_EDITORA) REFERENCES EDITORA(ID_EDITORA);

ALTER TABLE LIVRO
ADD CONSTRAINT FK_LIVRO_AUTOR FOREIGN KEY (ID_AUTOR) REFERENCES AUTOR(ID_AUTOR);


INSERT INTO EDITORA VALUES ('Palmar', 'Rua Valim', 500, 'Pampulhar', 80756299, 12, 81988763566, null, 'palm_edit@gmail.com');
INSERT INTO EDITORA VALUES ('Companhia das Letras', 'Avelin', 'S/N', 'Joaquim Tavares', 65738100, 7, 88988353536, null, 'compdasletras@outlook.com');
INSERT INTO EDITORA VALUES ('Record', 'Av. Paulista',3478, 'Bela Vista', 345000188, 24, 11989563586, null, 'record@gmail.com');
INSERT INTO EDITORA VALUES ('Addis', 'Av. Santos Dumont',7000, 'Aldeota', 60744900, 5, 85999983212, null, 'addis@hotmail.com');
INSERT INTO EDITORA VALUES ('Continental', 'Av. Alvrinho',500, 'Espirito Santo', 23981258, 20, 2177984655, null, 'cont@gmail.com');



UPDATE LIVRO SET ID_EDITORA = 1 WHERE EDITORA='Palmar';
UPDATE LIVRO SET ID_EDITORA = 2 WHERE EDITORA='Companhia das Letras';
UPDATE LIVRO SET ID_EDITORA = 3 WHERE EDITORA='Record';
UPDATE LIVRO SET ID_EDITORA = 4  WHERE EDITORA='Addis';
UPDATE LIVRO SET ID_EDITORA = 5  WHERE EDITORA='Continental';


UPDATE LIVRO SET ID = ID_CLIENTE;


INSERT INTO AUTOR VALUES ('Kelly Vircson', 'F', 'Filosofo', '01/02/1963')

INSERT INTO AUTOR VALUES ('Miguel de Cervantes', 'M', 'Teologo', '10/05/1957')
INSERT INTO AUTOR VALUES ('Gabriel Garcái Marques', 'M', 'Sociologo', '07/28/1972');
INSERT INTO AUTOR VALUES ('João River Nunes', 'M', 'Cientista de Dados', '09/08/1980');
INSERT INTO AUTOR VALUES ('Clara Mafra', 'F', 'Psicologa', '12/15/1982');


UPDATE LIVRO SET ID_AUTOR = 1 WHERE AUTOR='Kelly Vircson';
UPDATE LIVRO SET ID_AUTOR = 2 WHERE AUTOR='Miguel de Cervantes';
UPDATE LIVRO SET ID_AUTOR = 8 WHERE AUTOR='João River Nunes';
UPDATE LIVRO SET ID_AUTOR = 12 WHERE AUTOR='Clara Mafra';
UPDATE LIVRO SET ID_AUTOR = 13 WHERE AUTOR='Gabriel García Marques';


SELECT L.LIVRO, R.AUTOR, L.VALOR
FROM LIVRO L 
INNER JOIN AUTOR R  
ON L.ID_AUTOR = R.ID_AUTOR


SELECT L.LIVRO, R.AUTOR, E.EDITORA, L.VALOR
FROM LIVRO L
INNER JOIN AUTOR R
ON L.ID_AUTOR = R.ID_AUTOR 
INNER JOIN EDITORA E
ON L.ID_EDITORA = E.ID_EDITORA;


SELECT * FROM LIVRO