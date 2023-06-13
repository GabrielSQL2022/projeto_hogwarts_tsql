## INTRODUÇÃO

Esse projeto tem a finalidade de mostrar um pouco dos conceitos da linguagem T-SQL para manipulação de banco de dados relacional em SQL Server.

Sempre que me perguntam sobre criação de projeto de portfólio, recomendo a todos aqueles que estudam T-SQL, PL/SQL (Oracle) ou qualquer linguagem que façam um projeto e documentem aqui no Github. No entanto, busquem algo que gostem de verdade e, independente do assunto, que seja algo com que se identifiquem.
Nem todos gostam de escrever ou estudar, mas, mesclar estudo com algum assunto que dê prazer é sempre muito bom e ajuda muito no aprendizado.

Seguindo esse conceito, optei por criar este projeto no universo literário de Harry Potter, escrito por J. K Rowling, mais especificamente envolvendo a escola de magia e bruxaria de Hogwarts.
Então, para quem conhece este mundo mágico, será de mais fácil compreensão a criação das tabelas, colunas, constraints, relações e tudo que documentarei sobre Hogwarts no SQL Server.

Mas, para quem não conhece, é a oportunidade perfeita para se aventurar e aprender um pouco sobre T-SQL e o universo de Harry Potter. :magic_wand:

<hr size="100"> <!-- LINHA HORIZONTAL -->

## ANÁLISE DE REQUISITOS

A análise de requisitos consiste no aprofundamento e conhecimento sobre a regra de negócio da empresa, ou seja, nesta etapa são realizadas entrevistas e imersões acerca da empresa para compreender o que ela faz, os tipos de clientes que ela possui, o ramo que atua, sua história, características e tudo que for importante para a criação de um banco de dados consistente.

Pelo fato deste projeto não ser baseado em nenhuma empresa, e sim no universo de Harry Potter, não será necessário um aprofundamento sobre o assunto, porém é importante destacar os conceitos por trás das tabelas e colunas deste mundo mágico.

Para quem conhece o universo de Harry Potter sabe que ele envolve a escola de Hogwarts e outras pouco exploradas, como Durmstrang e Beauxbatons, o vilarejo de Hogsmeade, o Beco Diagonal, localizado em Londres, o Ministério da Magia e o mundo dos bruxos como um todo além do mundo dos trouxas (humanos não-bruxos).
Porém, para este projeto focarei apenas em Hogwarts e criarei uma base de dados simples que possa servir de base para outros projetos.

As tabelas criadas serão estas;

- **Casas**, **Professor**, **Aluno**, **Fundador**, **Armada de Dumbledore** e **Brigada Inquisitorial**.

<hr size="100"> <!-- LINHA HORIZONTAL -->

## MODELO FÍSICO

O Modelo Físico consiste no design do banco de dados com base nos requisitos apurados. Nesta etapa são representadas as tabelas, colunas, tipos de dados, visualizações, restrições, índices e outros procedimentos estruturais do banco de dados.

Também é definido o SGBD (Sistema de Gerenciamento de Banco de Dados) que será utilizado, neste projeto utilizarei o Microsoft SQL Server Management Studio.

Em projetos reais ou mais complexos são criados outros modelos antes do físico, como o conceitual e o lógico. Caso queria conhecer um pouco mais sobre estes outros modelos veja-os em outro projeto que fiz sobre uma livraria clicando **[aqui](https://github.com/GabrielSQL2022/projeto-livraria)**.

O SQL Server dispõe de uma funcionalidade nativa que cria um Diagrama de Banco de Dados simples de acordo com as tabelas, colunas e chaves criadas, conforme imagem abaixo:

![diagrama](https://i.imgur.com/NQ8N9rv.jpeg)

- ### Criação da Banco de Dados;

A instrução para criação de banco de dados mais simples no SQL Server é esta:

```
CREATE DATABASE HOGWARTS
```

- ### Criação das Tabelas;

Com o banco de dados criado as tabelas podem ser criadas. Optei por criar as tabelas definindo as chaves primárias (primary key), chaves estrangeiras (foreign key) e as colunas que não podem receber valores nulos:

```
CREATE TABLE CASAS
(
	ID_CASA INT PRIMARY KEY NOT NULL,
	NOME_CASA VARCHAR (20) NOT NULL,
	FUNDADOR VARCHAR (40),
	CORES VARCHAR (40),
	ANIMAL VARCHAR (30),
	ELEMENTO VARCHAR (30),
	TRAÇOS VARCHAR (100),
	FANTASMA VARCHAR (40)
)
```

```
CREATE TABLE PROFESSOR
(
	ID_PROF INT PRIMARY KEY NOT NULL,
	NOME_PROFESSOR VARCHAR (100) NOT NULL,
	DISCIPLINA VARCHAR (30),
	NASCIMENTO DATE,
	TÍTULOS VARCHAR (100),
	ID_CASA_PROF INT,
	CONSTRAINT FK_CASA_PROF FOREIGN KEY (ID_CASA_PROF)
	REFERENCES CASAS (ID_CASA)
)
```

```
CREATE TABLE ALUNO
(
	ID_ALUNO INT PRIMARY KEY NOT NULL,
	NOME_ALUNO VARCHAR (100) NOT NULL,
	NASCIMENTO DATE,
	NACIONALIDADE VARCHAR (30),
	GENERO VARCHAR (30),
	ID_CASA_ALUNO INT,
	CONSTRAINT FK_CASA_ALUNO FOREIGN KEY (ID_CASA_ALUNO)
	REFERENCES CASAS (ID_CASA)
)
```

```
CREATE TABLE FUNDADOR
(
        ID_FUNDADOR INT PRIMARY KEY NOT NULL,
        NOME_FUNDADOR VARCHAR (100) NOT NULL,
        HABILIDADES VARCHAR (100),
        ID_CASA_FUND INT,
        CONSTRAINT FK_CASA_FUNDADOR FOREIGN KEY (ID_CASA_FUND)
        REFERENCES CASAS (ID_CASA)
)
```

```
CREATE TABLE ARMADA_DUMBLEDORE
(
        ID_MEMBRO INT PRIMARY KEY NOT NULL,
        NOME_MEMBRO VARCHAR (100) NOT NULL,
        OBSERVAÇÃO VARCHAR (200),
        ID_ALUNO_ARMDUM INT,
        CONSTRAINT FK_ALUNO_ARM_DUMBLE FOREIGN KEY (ID_ALUNO_ARMDUM)
        REFERENCES CASAS (ID_CASA)
)
```

```
CREATE TABLE BRIGADA_INQUISITORIAL
(
        ID_MEMBRO INT PRIMARY KEY NOT NULL,
        NOME_MEMBRO VARCHAR (100),
        ID_ALUNO_BRIGINQUI INT,
        CONSTRAINT FK_ALUNO_BRIG_INQUI FOREIGN KEY (ID_ALUNO_BRIGINQUI)
        REFERENCES CASAS (ID_CASA)
)
```

- ### Inserindo dados nas tabelas;

**_atualizado em 13/06/2023_**
