# ProjetoMediPre-o-
-Projeto processo seletivo para a empresa MediPreço;
-Programas necessários:
        - Vscode;
        - Mysql;
-VERSIONAMENTO
    -git add .
    -git status 
    -git checkout origem master
    -git commit -m "segundo commit"
    -git push  

-Passo a passo para realização do projeto MediPreço:

1. - Instalação do Git;
	
	https://git-scm.com/download/win
	     

2. -Iniciar projeto 
    
    -git clone https://github.com/-bibiperigosa28/ProjetoMediPre-o-.git
    

3. - Criar tabela de medicamentos no Mysql;
    
    -CREATE DATABASE DADOS;
    USE DADOS;
    CREATE TABLE MEDICAMENTO(
    ID INT(11) NOT NULL AUTO_INCREMENT,
    CODBARRA CHAR (13) NOT NULL,
    PRODUTO VARCHAR (100) NOT NULL,
    PRECO DECIMAL (15,2) NOT NULL,
    CATEGORIA VARCHAR(100) NOT NULL,
    PRIMARY KEY (ID)
    )ENGINE=INNODB DEFAULT CHARSET=UTF8;
    

4. - Importar CSV da tabela "Medicamento" para o Mysql,logo após clicar com o botão direito sobre a tabela "medicamento" abrir a opção "Table Date Import Wizard" e selecione o arquivo para exportação;

5. 
#### TABELA PRODUTO
CREATE TABLE PRODUTO (
    ID INT(11) NOT NULL AUTO_INCREMENT,
    IDCATEGORIA INT NOT NULL,
    NOME VARCHAR(150) NOT NULL,
    CODBARRA CHAR(13) NOT NULL,
    PRIMARY KEY (ID),
    FOREIGN KEY (IDCATEGORIA) REFERENCES CATEGORIA(ID)
)  ENGINE=INNODB DEFAULT CHARSET=UTF8;


#### CARGA 
INSERT INTO produto
(NOME,CODBARRAS,IDCATEGORIA)
SELECT M.PRODUTO AS NOME, M.CODBARRA, C.ID AS IDCATEGORIA FROM MEDICAMENTO AS M
INNER JOIN CATEGORIA AS C ON M.CATEGORIA = C.NOME;



### TABELA CATEGORIA
CREATE TABLE CATEGORIA(
    ID INT(11) NOT NULL AUTO_INCREMENT,
    NOME VARCHAR(150) NOT NULL,
    PRIMARY KEY (ID)
)  ENGINE=INNODB DEFAULT CHARSET=UTF8;

### UPDATE categoria SET NOME = 'SEM CATEGORIA' WHERE ID= 6;

### CARGA
INSERT INTO CATEGORIA
(NOME)
SELECT CATEGORIA FROM MEDICAMENTO  GROUP BY CATEGORIA;


### TABELA COMPRA
CREATE TABLE COMPRA (
    ID INT(11) NOT NULL AUTO_INCREMENT,
    IDCLIENTE INT NOT NULL,
    IDCOMPRA INT NOT NULL,
    DATA DATE NOT NULL,
    PRODUTO VARCHAR (150) DEFAULT 0,
    QUANTIDADE INT NOT NULL,
    PRIMARY KEY (ID),
    FOREIGN KEY (IDCLIENTE) REFERENCES CLIENTE(ID)
)  ENGINE=INNODB DEFAULT CHARSET=UTF8;


### TABELA COMPRAPRODUTO
CREATE TABLE COMPRAPRODUTO(
    ID INT(11) NOT NULL AUTO_INCREMENT,
    IDPRODUTO INT NOT NULL,
    IDCOMPRA INT NOT NULL,
    QUANTIDADE INT NOT NULL,
    PRECO DECIMAL(15,2),
    PRIMARY KEY (ID),
	FOREIGN KEY (IDPRODUTO) REFERENCES PRODUTO(ID),
	FOREIGN KEY (IDCOMPRA) REFERENCES COMPRA(ID)
)  ENGINE=INNODB DEFAULT CHARSET=UTF8;


### TABELA CLIENTE
CREATE TABLE CLIENTE (
    ID INT(11) NOT NULL AUTO_INCREMENT,
    NOME VARCHAR(150) NOT NULL,
    PRIMARY KEY (ID)
)  ENGINE=INNODB DEFAULT CHARSET=UTF8;


### CARGA CLIENTE 
INSERT INTO dados.cliente
(NOME)
VALUES
('GABRIELLY SOARES CALDEIRA');

### VIEW
Total de produtos daquela categoria;
CREATE VIEW  VW_TOTALPRODUTOCATEGORIA AS 
SELECT C.NOME, count(*) AS QTDPRODUTO FROM CATEGORIA AS C 
INNER JOIN PRODUTO AS P ON P.IDCATEGORIA = C.ID
GROUP BY C.ID;
 
CREATE VIEW  VW_PRODUTOMENORPRECO AS 
SELECT C.NOME, MIN(P.PRECO) AS MENORPRECO FROM CATEGORIA AS C 
INNER JOIN PRODUTO AS P ON P.IDCATEGORIA = C.ID
GROUP BY C.ID;

CREATE VIEW VW_MEDIAPRECO AS 
SELECT C.NOME, TRUNCATE(AVG(P.PRECO),2)AS MEDIAPRECO FROM CATEGORIA AS C 
INNER JOIN PRODUTO AS P ON P.IDCATEGORIA = C.ID
GROUP BY C.ID;

CREATE VIEW  VW_PRODUTOMAIORPRECO AS 
SELECT C.NOME, MAX(P.PRECO) AS MAIORPRECO FROM CATEGORIA AS C 
INNER JOIN PRODUTO AS P ON P.IDCATEGORIA = C.ID
GROUP BY C.ID;

<!DOCTYPE html>
<html>
    <head>
        <mate charest="utf-8" />
    </head>
    <body>
       <img src=”https://raw.githubusercontent.com/bibiperigosa28/ProjetoMediPre-o-/main/imagem/powerbi.jpeg” alt=”Grafico” width="300" height="200"/>
    </body>
</html>
```

      
![](https://raw.githubusercontent.com/bibiperigosa28/ProjetoMediPre-o-/main/imagem/powerbi.jpeg)
