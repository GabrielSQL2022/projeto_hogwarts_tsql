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

![diagrama](https://i.ibb.co/kKFqpRk/Diagrama-Modelo-F-sico.jpg)

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
    HABILIDADES VARCHAR (200),
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
    TIPO VARCHAR (20),
    ID_ALUNO_ARMDUM INT,
	CONSTRAINT FK_ALUNO_ARM_DUMBLE FOREIGN KEY (ID_ALUNO_ARMDUM)
	REFERENCES ALUNO (ID_ALUNO)
)
```


- ### Inserindo dados nas tabelas;

Para a inserção dos dados optei por seguir a sintaxe mais simples e minimalista, sem destacar as colunas que os dados pertencem, porém seguindo a ordem correta:

```
INSERT INTO CASAS 
VALUES
(1,'Grifinória','Godrico Gryffindo','Escarlate e ouro','Leão','Fogo','Coragem, Bravura, Determinação, Ousadia, Nobreza e Cavalherismo','Nick Quase Sem Cabeça'),
(2,'Lufa-Lufa','Helga Hufflepuf','Amarelo e preto','Texugo','Terra','Trabalho árduo, Justiça, Lealdade, Paciência,Sinceridade e Modéstia','Frei Gorducho'),
(3,'Corvinal','Rowena Ravenclaw','Azul e bronze','Águia','Ar','Sagacidade, Aprendizagem, Sabedoria, Aceitação, Inteligência e Criatividade','Dama Cinzenta'),
(4,'Sonserina','Salazar Slytherin','Verde e prata','Serpente','Água','Despreço pelas regras, Determinação, Criatividade, Orgulho, Astúcia, Ambição, Autopreservação','Barão Sangrento');
```

```
INSERT INTO PROFESSOR
VALUES
(50,'Quirino Quirrell','Defesa Contra as Artes das Trevas','23/01/1960','Professor',3),
(60,'Gilderoy Lockhart','Defesa Contra as Artes das Trevas','26/01/1964','Professor, Escritor e Fundador e líder do Clube de Duelos',3),
(70,'Remo João Lupin','Defesa Contra as Artes das Trevas','10/03/1960','Professor e Monitor',1),
(80,'Alastor Moody','Defesa Contra as Artes das Trevas','08/03/1911','Auror e Professor',2),
(90,'Dolores Umbridge','Defesa Contra as Artes das Trevas','26/03/1961','Subsecretária Sênior do Ministro da Magia, Diretora de Hogwarts e Professora',4),
(100,'Minerva McGonagall','Transfiguração','04/10/1935','Monitora-Chefe, Diretora da Casa de Grifinória, Vice-Diretora de Hogwarts, Professora, Diretora de Hogwarts',1),
(110,'Alvo Percival Wulfrico Brian Dumbledore','Defesa Contra as Artes das Trevas','01/08/1881','Diretor do Departamento de Transfiguração, Cacique Supremo da Confederação Internacional dos Bruxos, Colunista do Transfiguração Hoje e Professor',1),
(120,'Pomona Sprout','Herbologia','15/05/1931','Diretora do Depertamento de Herbologia, Diretora da Casa de Lufa-Lufa, Professora',2);
```

```
INSERT INTO ALUNO
VALUES
(101,'Angelina Johnson','1977/10/30','Irlandesa','Feminino',1),
(102,'Harry Tiago Potter','1980/07/31','Inglês','Masculino',1),
(103,'Luna Lovegood','1981/02/13','Britânica','Feminino',3),
(104,'Cho Chang','1980/07/29','Britânica','Feminino',3),
(105,'Padma Patil','1979/09/02','Irlandesa','Feminino',3),
(106,'Terêncio Boot','1980/04/21','Inglês','Masculino',3),
(107,'Rogério Davies','1978/08/31','Britânico','Masculino',3),
(108,'Marcos Flint','1975/09/01','Irlandês','Masculino',4),
(109,'Pansy Parkinson','1979/09/01','Irlandesa','Feminino',4),
(110,'Emília Bulstrode','1980/10/31','Irlandesa','Feminino',4),
(111,'Vicente Crabbe','1980/10/16','Britânico','Masculino',4),
(112,'Gregório Goyle','1979/09/04','Britânico','Masculino',4),
(113,'Draco Malfoy','1980/06/05','Britânico','Masculino',4),
(114,'Percy Weasley','1976/10/22','Inglês','Masculino',1),
(115,'Fred Weasley','1978/04/01','Inglês','Masculino',1),
(116,'Jorge Weasley','1978/04/01','Inglês','Masculino',1),
(117,'Ronald Weasley','1980/03/01','Inglês','Masculino',1),
(118,'Gina Weasley','1981/10/11','Inglesa','Feminino',1),
(119,'Colin Creevey','1981/05/03','Britânico','Masculino',1),
(120,'Dino Thomas','1979/12/08','Inglês','Masculino',1),
(121,'Hermione Granger','1979/09/19','Inglesa','Feminina',1),
(122,'Lilá Brown','1980/02/04','Inglesa','Feminina',1),
(123,'Lino Jordan','1978/07/22','Britânico','Masculino',1),
(124,'Neville Longbottom','1980/07/30','Britânico','Masculino',1),
(125,'Olívio Wood','1975/10/30','Irlandês','Masculino',1),
(126,'Parvati Patil','1980/04/21','Irlandesa','Feminino',1),
(127,'Simas Finnigan','1980/05/29','Irlandês','Masculino',1),
(128,'Cedrico Diggory','1977/10/16','Britânico','Masculino',2),
(129,'Ernesto Macmillan','1980/04/22','Britânico','Masculino',2),
(130,'Ana Abbott','1979/10/22','Irlandesa','Feminino',2),
(131,'Susana Bones','1980/09/29','Britânica','Feminino',2),
(132,'Zacarias Smith','1979/11/14','Irlandês','Femino',2);
```

```
INSERT INTO FUNDADOR
VALUES
(10,'Salazar Slytherin','Ofidioglossia, Legilimência, Artes das Trevas, Fabricante de varinhas, Feitiços e Criador de basilisco',4),
(11,'Rowena Ravenclaw','Feitiços, Adivinhação, História da Magia, Arquitetura mágica e Invenção',3),
(12,'Godrico Gryffindor','Duelo e Feitiços',1),
(13,'Helga Hufflepuff','Feitiços e Invenção',2);
```

```
INSERT INTO ARMADA_DUMBLEDORE
VALUES
(200,'Harry Tiago Potter','Líder',102),
(201,'Hermione Granger','Líder',121),
(203,'Ronald Weasley','Líder',117),
(204,'Neville Longbottom','Lider',124),
(205,'Gina Weasley','Líder',118),
(206,'Luna Lovegood','Líder',103),
(207,'Angelina Johnson','Membro',101),
(208,'Dino Thomas','Membro',120),
(209,'Colin Creevey','Membro',119),
(210,'Fred Weasley','Membro',115),
(211,'Jorge Weasley','Membro',116),
(222,'Lilá Brown','Membro',122),
(223,'Lino Jordan','Membro',123),
(224,'Parvati Patil','Membro',126),
(225,'Simas Finnigan','Membro',127),
(226,'Cho Chang','Membro',104),
(227,'Padma Patil','Membro',105),
(228,'Ana Abbott','Membro',130),
(229,'Zacarias Smith','Membro',132);
```

**_atualizado em 20/11/2023_**
