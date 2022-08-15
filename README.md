## Sumário

- [**O que vamos aprender?**](#o-que-vamos-aprender)
  - [Você será capaz de:](#você-será-capaz-de)
- [**Porque isso é importante?**](#porque-isso-é-importante)
- [**Conteúdos**](#conteúdos)
  - [O que é JOIN?](#o-que-é-join)
  - [Como utilizar o INNER JOIN](#como-utilizar-o-inner-join)
  - [Como utilizar o LEFT JOIN e o RIGHT JOIN](#como-utilizar-o-left-join-e-o-right-join)
  - [O que é SELF JOIN e quando utilizar](#o-que-é-self-join-e-quando-utilizar)
- [**Vamos praticar!**](#vamos-praticar)
- [**Exercicios**](#exercicios)
  - [Agora na prática](#agora-na-prática)
  - [Bônus](#bônus)
- [**Recursos Adicionais**](#recursos-adicionais)

## **O que vamos aprender?**

Hoje você vai aprender sobre o **JOIN**, alguns dos seus tipos, e como podemos utilizá-lo para juntar dados relacionados. 😉

![Bem vindo](https://thumbs.gfycat.com/HatefulAllFlycatcher-max-1mb.gif)

### Você será capaz de:

- Combinar dados de duas tabelas utilizando **INNER JOIN**;
- Combinar dados de duas tabelas, preservando de uma, utilizando **LEFT JOIN** e **RIGHT JOIN**;
- Utilizar dados de uma mesma tabela utilizando **SELF JOIN**;

## **Porque isso é importante?**

Em nossa vida de pessoa desenvolvedora podemos nos deparar com um banco de dado relacional, e eles são conhecidos, muitas vezes, por manter dados espalhados por diversas tabelas,
e para obter um conjunto de informações podemos fazer uso do **JOIN**.

## **Conteúdos**

### O que é JOIN?

Nesse universo de ferramentas do **SQL** que já vimos ao longo do curso, hoje vamos adicionar mais uma a nossa lista o **JOIN**, mas afinal o que ele faz?
Sabe quando alguns dados estão em uma tabela e outros em outra? Com esta nova ferramenta nós podemos uni-los em um só resultado! 🤩

Ou seja, basicamente o **JOIN** é a junção de duas ou mais colunas de tabelas diferentes, exibindo apenas as informações que queremos.

[![JOIN MEME](https://i.postimg.cc/j5XW0WGf/1-2cl-2q-W1-Az-Vzca-Vx-k0r-Kg.png)](https://postimg.cc/CBRMbKMM)

### Como utilizar o INNER JOIN

O **INNER JOIN** exibe as informações que são **comuns** entre as tabelas. Observe a imagem:

[![inner-join.jpg](https://i.postimg.cc/nLn71jzg/inner-join.jpg)](https://postimg.cc/0zHbkN70)

Como é visível na imagem, temos um campo de dados comuns, para obtermos essas informações é necessário fazer uso de uma condição chamada **ON**, com ela podemos especificar qual é a coluna comum entre as tabelas. Vamos ver um pouco como é essa sintaxe na prática:

```
SELECT tabela1.coluna1, tabela2.coluna2
FROM tabela1
INNER JOIN tabela2
ON tabela1.coluna_em_comum1 = tabela2.coluna_em_comum2;
```

*A tradução desse comando ficaria: Selecione a coluna1 da tabela1, a coluna2 da tabela2 vindo da tabela1 juntando com a tabela2
onde a coluna_em_comum1 da tabela1 é igual a coluna_em_comum2 da tabela2*

Você consegue perceber quantas vezes precisamos dizer tabela1 e tabela2? Não é uma boa prática fazermos isso, para isso temos um aliado, ou melhor, **alias**. Mas afinal, o que é um *alias*? Um alias é um apelido que podemos dar a uma tabela, é como chamar uma pessoa de nome José de Zé. Veja o exemplo usando o **AS**:

```
SELECT t1.coluna, t2.coluna
FROM tabela1 AS t1
INNER JOIN tabela2 AS t2
ON t1.coluna_em_comum = t2.coluna_em_comum;
```

Também é possível omitir o **AS**:

```
SELECT t1.coluna, t2.coluna
FROM tabela1 t1
INNER JOIN tabela2 t2
ON t1.coluna_em_comum = t2.coluna_em_comum;
```

#### Na prática:

⚠️ Atencão! Para acompanhar os comandos e fazer o exercicio de fixação será necessário a utilização do banco de dados **Trybe ~~is cool~~ School**:

```
DROP SCHEMA IF EXISTS school;
CREATE SCHEMA school;
USE school;

CREATE TABLE countries (
id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
country VARCHAR(45) NOT NULL,
country_code VARCHAR(5) NOT NULL
);

CREATE TABLE states (
id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
state VARCHAR(45) NOT NULL,
state_code VARCHAR(5) NOT NULL,
country_id INT NOT NULL,
FOREIGN KEY (country_id) REFERENCES countries(id)
);

CREATE TABLE cities (
id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
city VARCHAR(45) NOT NULL,
state_id INT NOT NULL,
FOREIGN KEY (state_id) REFERENCES states(id)
);

CREATE TABLE adresses (
id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
cep VARCHAR(45) NOT NULL,
street VARCHAR(45) NOT NULL,
number INT NOT NULL,
city_id INT NOT NULL,
FOREIGN KEY (city_id) REFERENCES cities(id)
);

CREATE TABLE phones (
id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
phone VARCHAR(16) NOT NULL
);

CREATE TABLE teachers (
id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
first_name VARCHAR(45) NOT NULL,
last_name VARCHAR(45) NOT NULL,
phone_id INT NULL,
address_id INT NOT NULL,
FOREIGN KEY (phone_id) REFERENCES phones(id),
FOREIGN KEY (address_id) REFERENCES adresses(id)
);

CREATE TABLE subjects (
id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
name VARCHAR(45) NOT NULL,
teacher_id INT NOT NULL,
FOREIGN KEY (teacher_id) REFERENCES teachers(id)
);

CREATE TABLE tribes (
id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
name VARCHAR(45) NOT NULL,
teacher_id INT NOT NULL,
FOREIGN KEY (teacher_id) REFERENCES teachers(id)
);

CREATE TABLE studants (
id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
first_name VARCHAR(45) NOT NULL,
last_name VARCHAR(45) NOT NULL,
buddie_id INT NULL,
tribe_id INT NOT NULL,
phone_id INT NULL,
address_id INT NULL,
FOREIGN KEY (tribe_id) REFERENCES tribes(id),
FOREIGN KEY (phone_id) REFERENCES phones(id),
FOREIGN KEY (address_id) REFERENCES adresses(id)
);

INSERT INTO countries (country, country_code)
VALUES ('Brasil', 'BR');

INSERT INTO states (id, state, state_code, country_id)
VALUES (1, 'Acre','AC', 1),
(2, 'Alagoas','AL', 1),
(3, 'Amapá','AP', 1),
(4, 'Amazonas','AM', 1),
(5, 'Bahia','BA', 1),
(6, 'Ceará','CE', 1),
(7, 'Distrito Federal','DF', 1),
(8, 'Espírito Santo','ES', 1),
(9, 'Goiás','GO', 1),
(10, 'Maranhão','MA', 1),
(11, 'Mato Grosso','MT', 1),
(12, 'Mato Grosso do Sul','MS', 1),
(13, 'Minas Gerais','MG', 1),
(14, 'Pará','PA', 1),
(15, 'Paraíba','PB', 1),
(16, 'Paraná','PR', 1),
(17, 'Pernambuco','PE', 1),
(18, 'Piauí','PI', 1),
(19, 'Rio de Janeiro','RJ', 1),
(20, 'Rio Grande do Norte','RN', 1),
(21, 'Rio Grande do Sul','RS', 1),
(22, 'Rondônia','RO', 1),
(23, 'Roraima','RR', 1),
(24, 'Santa Catarina','SC', 1),
(25, 'São Paulo','SP', 1),
(26, 'Sergipe','SE', 1),
(27, 'Tocantins','TO', 1);

INSERT INTO cities (city, state_id)
VALUES ('Rio Branco', 1),
('Capixaba', 1),
('Maceió', 2),
('Amapá', 3),
('Manaus', 4),
('Salvador', 5),
('Santa Luzia', 5),
('Canudos', 5),
('Fortaleza', 6),
('Brasília', 7),
('Vitória', 8),
('Águia Branca', 8),
('Goiânia', 9),
('São Luís', 10),
('Cuiabá', 11),
('Campo Grande', 12),
('Belo Horizonte', 13),
('Belém', 14),
('João Pessoa', 15),
('Campina Grande', 15),
('Curitiba', 16),
('Recife', 17),
('Teresina', 18),
('Rio de Janeiro', 19),
('Cabo Frio', 19),
('Nova Friburgo', 19),
('Natal', 20),
('Parnamirim', 20),
('Porto Alegre', 21),
('Porto Velho', 22),
('Boa Vista', 23),
('Florianópolis', 24),
('Balneário Camboriú', 24),
('Águas Frias', 24),
('São Paulo', 25),
('Campinas', 25),
('Mogi das Cruzes', 25),
('Aracaju', 26),
('Areia Branca', 26),
('Palmas', 27);


INSERT INTO adresses (cep, street, number, city_id)
VALUES ('69902467', 'Rua Flor de Maio', 203, 1),
('69931970', 'Rua Ocimar Tessinari', 07, 2),
('57010378', 'Travessa Capitão Cantuário', 132, 3),
('68950970', 'Avenida Guarani', 242, 4),
('69077755', 'Avenida Professor Valmir Souza', 324, 5),
('41204355', 'Rua Jacobina', 675, 6),
('45865970', 'Avenida 2 de Julho', 559, 7),
('60840375', 'Rua A', 413, 9),
('72428338', 'Núcleo Rural Casa Grande Módulo 10 MA', 22, 10),
('29032773', 'Rua São José Pescador', 631, 11),
('29795982', 'Estrada Ebenezer', 0, 12),
('74370804', 'Rua FV', 20, 13),
('65082281', '1ª Travessa José Sarney', 131, 14),
('78076310', 'Rua Dois', 642, 15),
('30290080', 'Praça Pero Vaz de Caminha', 203, 17),
('66115014', 'Passagem Treze de Outubro', 203, 18),
('58059134', 'Rua Costureira Maria Guedes dos Santos', 71, 19),
('58406476', 'Rua José João Damasceno', 203, 20),
('81920375', 'Rua Papa João XXIII', 1, 21),
('50740210', 'Rua Patrocínio', 1, 22),
('64078675', 'Rua Carnavalesco Zé Carvalho', 203, 23),
('22231150', 'Rua Martins Ribeiro', 203, 24),
('28921665', 'Rua Quatorze', 42, 25),
('28615305', 'Rua Ypê Roxo', 203, 26),
('59114077', 'Travessa Elviro Pessoa', 71, 27),
('59147275', 'Rua Projetada Onze', 203, 28),
('76824174', 'Rua Antônio Maria Valença', 203, 30),
('69313760', 'Rua Félix Valois de Araújo', 71, 31),
('88062310', 'Servidão Aurélio Garcia', 203, 32),
('88339010', 'Rua Paraná', 203, 33),
('89843971', 'Rua João Pessoa', 364, 34),
('02036017', 'Travessa da Estrela Fugaz', 203, 35),
('13087506', 'Rua Clóvis Teixeira', 71, 36),
('08746020', 'Rua José Cândido', 203, 37),
('49071200', 'Rua Edson Andrade', 203, 38),
('49580970', 'Largo Manoel do Prado, s/n', 0, 39),
('77015570', 'Quadra 403 Sul Alameda', 8, 40);

INSERT INTO phones (phone)
VALUES ('(63) 2347-5846'),
('(68) 3385-9180'),
('(21) 3996-5924'),
('(94) 2336-6168'),
('(83) 3944-6382'),
('(83) 3842-6122'),
('(35) 2356-2450'),
('(75) 3488-2455'),
('(91) 3545-2337'),
('(63) 3353-5143'),
('(67) 3187-8418'),
('(67) 2359-6853'),
('(33) 2423-8341'),
('(61) 3636-8798'),
('(82) 3562-4477'),
('(48) 3307-4756'),
('(91) 3275-6045'),
('(82) 3496-6426'),
('(82) 2212-3200'),
('(68) 3838-4184'),
('(98) 2447-3294'),
('(69) 2488-2411'),
('(69) 2488-2411'),
('(61) 3633-1453'),
('(95) 3792-8148'),
('(17) 3688-2417'),
('(99) 3542-6745'),
('(17) 3231-7130'),
('(63) 3769-3506'),
('(89) 3717-2582'),
('(54) 3076-7918'),
('(11) 2553-8784'),
('(63) 2028-6518'),
('(49) 3387-1480'),
('(79) 3528-2437'),
('(41) 2438-3738'),
('(83) 2662-2612');

INSERT INTO teachers (first_name, last_name, phone_id, address_id)
VALUES ('Matheus', 'Goyas', null, 1),
('Rafael', 'Luiz', 2, 2),
('Alberto', 'Cavalcanti', 3, 3),
('DjoDjo', 'Boeing', null, 4);

INSERT INTO subjects (name, teacher_id)
VALUES ('Fundamentos', 2), ('Front-end', 3), ('Back-end', 4), ('Ciência da Computação', 1);

INSERT INTO tribes (name, teacher_id)
VALUES ('A', 2), ('B', 3), ('C', 4);

INSERT INTO studants (id, first_name, last_name, buddie_id, tribe_id, phone_id, address_id)
VALUES
(1, 'David', 'Gonzaga', 3, 2, 5, 5),
(2, 'Patricia', 'Dias', 25, 3, null, 6),
(3, 'Laura', 'Fumagalli', 1, 1, 7, 7),
(4, 'Benício', 'Giovanni', 22, 2, 8, null),
(5, 'Rosa', 'Isabel', 30, 3, 9, 9),
(6, 'Pedro', 'Rodrigo', 29, 1, 10, null),
(7, 'Daniel', 'João', null, 3, 11, 11),
(8, 'Bruno', 'Severino', 23, 2, null, 12),
(9, 'Matheus', 'André', null, 1, 13, 13),
(10, 'Maitê', 'Nina', null, 3, 14, 14),
(11, 'Betina', 'Olivia', null, 1, 16, null),
(12, 'Ayla', 'Cristiane', 16, 1, 15, 15),
(13, 'Carlos', 'Eduardo', 15, 3, 17, 17),
(14, 'Jennifer', 'Kamilly', 24, 2, 18, 18),
(15, 'Giovanni', 'Henry', 13, 1, null, 19),
(16, 'Isaac', 'Samuel', 12, 3, 20, 20),
(17, 'Guilherme', 'Emanuel', 31, 2, 21, 21),
(18, 'Carolina', 'Elisa', null, 2, null, 22),
(19, 'Erick', 'Francisco', 21, 3, 24, null),
(20, 'Pietro', 'Miguel', null, 2, 23, 23),
(21, 'Henrique', 'Kevin', 19, 1, 25, 25),
(22, 'Beatriz', 'Emilly', 4, 3, 27, 26),
(23, 'Sérgio', 'Luís', 8, 1, 26, 27),
(24, 'Igor', 'Bento', 14, 1, 28, null),
(25, 'Benedito', 'Luiz', 2, 2, null, 29),
(26, 'Cláudia', 'Brenda', 28, 1, 30, 30),
(27, 'Rosa', 'Larissa', null, 3, 31, 31),
(28, 'Alícia', 'Mariana', 26, 1, null, null),
(29, 'Rosa', 'Luana', 6, 2, 33, null),
(30, 'Camila', 'Brenda', 5, 3, 34, 34),
(31, 'Vitor', 'Mateus', 17, 1, 36, 35),
(32, 'Lorena', 'Patrícia', null, 2, null, 36);
```

Algumas tabelas que vamos usar do nosso banco de dados:

[![teachers-subject-tribes-tables.png](https://i.postimg.cc/vmKh3mqf/teachers-subject-tribes-tables.png)](https://postimg.cc/qt827pdv)

Vamos exibir o primeiro nome do professor que ensina cada matéria:

```
SELECT S.id AS id_da_materia, S.name, T.first_name, T.id AS id_do_professor
FROM school.subjects AS S
INNER JOIN school.teachers AS T ON S.teacher_id = T.id;
```

Sem **AS**:

```
SELECT S.id id_da_materia, S.name, T.first_name, T.id id_do_professor
FROM school.subjects S
INNER JOIN school.teachers T ON S.teacher_id = T.id;
```

Exemplo de saída:

| id_da_materia | name                  | first_name | id_do_professor
| :-----------: | :-------------------: | :--------: | :-------------:
| 4             | Ciência da Computação | Matheus    | 1
| 1             | Fundamentos           | Rafael     | 2
| 2             | Front-end             | Alberto    | 3
| 3             | Back-end              | DjoDjo     | 4

#### Pra fixar:
1. Faça uma query que exiba o **nome da matéria** e o **primeiro nome do professor**:
2. Faça uma query que exiba o **nome da matéria** e o **sobrenome do professor**:
3. Faça uma query que exiba o **nome do professor** e a **tribo** que ele pertence.
4. Faça uma query que exiba o **nome da matéria** e o **nome completo do professor**:
5. Faça uma query que exiba o **nome completo do professor** e a **tribo** que ele pertence.

### Como utilizar o LEFT JOIN e o RIGHT JOIN

Como foi visto o **INNER JOIN** vai buscar as informações em comum que existem nas tabelas, já o **LEFT JOIN**
vai exibir os dados da tabela da esquerda independente de haver algum dado em comum com a tabela da direita. Observe a imagem abaixo:

[![left-join.png](https://i.postimg.cc/P5YN9t9H/left-join.png)](https://postimg.cc/ZWYTyhJs)

Vale salientar que a tabela referente ao **LEFT JOIN** sempre será após o **FROM**, mas para ficar claro a tradução de **LEFT** é esquerda e **RIGHT** direita.

#### Na prática:

Essas são as tabelas do nosso banco de dados, vamos trabalhar com algumas delas abaixo:
[![all-tables.png](https://i.postimg.cc/MGb4c9cF/all-tables.png)](https://postimg.cc/jW2vmQ4H)

Vamos montar uma query que exibe o nome das pessoas estudantes de nossa escola e seu respectivo endereço utilizando o **LEFT JOIN**:

```
SELECT S.first_name, S.address_id, A.cep, A.street, A.number
FROM school.studants S
LEFT JOIN school.adresses A ON S.address_id = A.id;
```

Exemplo de saída:

[![saida-left-join.png](https://i.postimg.cc/W1zGBq3d/saida-left-join.png)](https://postimg.cc/G40TY2vR)

Como é possível observar no exemplo acima, algumas pessoas estudantes possuem o **address_id** com valor **null**, só é possível
visualizar isso porque estamos utilizando o **LEFT JOIN**, vamos substituir o **LEFT** por **INNER** na nossa query e vamos comparar os
resultados:

```
SELECT S.first_name, S.address_id, A.cep, A.street, A.number
FROM school.studants S
INNER JOIN school.adresses A ON S.address_id = A.id;
```

Exemplo de saída:

[![saida-compare-left-inner-join.png](https://i.postimg.cc/9fKHd94Z/saida-compare-left-inner-join.png)](https://postimg.cc/Z98QZCx5)

Comparando os resultados é possível observar que algumas pessoas estudantes foram ocultadas, essa é a diferença do **INNER JOIN** para **LEFT JOIN**.

Agora vamos para o **RIGHT JOIN**, veja a ilustração abaixo:

[![right-join.jpg](https://i.postimg.cc/Px5vwBwP/right-join.jpg)](https://postimg.cc/sBb2FHKr)

Como é ilustrado o **RIGHT JOIN** é o oposto do **LEFT JOIN**, ele representa a tabela da direita, vamos executar a mesma query usando o **RIGHT JOIN**:

```
SELECT S.first_name, S.address_id, A.cep, A.street, A.number
FROM school.studants S
RIGHT JOIN school.adresses A ON S.address_id = A.id;
```

Exemplo de saída:

[![saida-right-join.png](https://i.postimg.cc/bwYPppcD/saida-right-join.png)](https://postimg.cc/qzFSGf74)

Sendo assim, como é mostrado acima, o **RIGHT JOIN** irá listar todos os endereços mesmo que não tenha nenhum estudante sendo referenciado.

#### Pra fixar:
1. Faça uma query que exiba o **nome de todas as pessoas estudantes** e seu **número de telefone**
2. Faça uma query que exiba o **nome de todos os professores** e seu **número de telefone**
3. Faça uma query que exiba **todos os números de telefone** com o **nome do professor** responsável por aquele número.
4. Faça uma query que exiba **todos os números de telefone** com o **nome da pessoa estudante** responsável por aquele número.

### O que é SELF JOIN e quando utilizar

A tradução da palavra **SELF** é a própria pessoa, isso significa que faremos um **JOIN** na própria tabela que estamos manipulando.

[![homem-aranha-meme.jpg](https://i.postimg.cc/XY43s1Mn/homem-aranha-meme.jpg)](https://postimg.cc/SJTwsrNP)

No nosso banco de dados temos uma tabela de estudantes, lá existe uma coluna com nome de **buddie_id**, ela refere-se ao id de outra pessoa estudante, a qual, é sua parceira. Para listar todas as pessoas estudantes com seu respectivo buddie é necessário fazer um **SELF JOIN**. Veja na prática:

```
SELECT Studant.first_name, Studant.buddie_id, Buddie.first_name
FROM school.studants Studant
INNER JOIN school.studants Buddie ON Studant.buddie_id = Buddie.id;
```

Sim! Você não viu errado, o **SELF JOIN** na verdade é apenas um **INNER JOIN** na própria tabela. Mas também podemos declarar
a tabela duas vezes, dessa forma:

```
SELECT Studant.first_name, Studant.buddie_id, Buddie.first_name
FROM school.studants Studant, school.studants Buddie
WHERE Studant.buddie_id = Buddie.id;
```

Exemplo de saída:

[![saida-self-join.png](https://i.postimg.cc/pVzCJRD5/saida-self-join.png)](https://postimg.cc/8skL18XT)

#### Pra fixar:
1. Exiba o **nome completo** do **estudante** e do seu **parceiro**

## **Vamos praticar!**
Vamos bater um papo sobre SQL? Hora da aula ao vivo! Vamos para o Slack, onde o link estará disponível.
## **Exercicios**

### Agora na prática

⚠️ Atencão! Para fazer o exercicio será necessário a utilização do banco de dados [Trybe ~~is cool~~ School](#na-prática):

1. Faça uma query que exiba **quantos estudantes** existem por **tribo**.
2. Faça uma query que conte **quantas duplas** de **buddies** existem no banco de dados.
3. Faça uma query que exiba **nome completo**, **cep**, **rua** e **número de telefone** de professores que **possuem** endereço e telefone.
4. Faça uma query que exiba **quantos estudantes possuem endereço registrado**.
5. Faça uma query que exiba o **nome completo do estudante**, **cep**, **rua**, **número**, **cidade** e **estado**.
6. Faça uma query que exiba **quantos estudantes residem por estado** em **ordem decrescente**.
7. Faça uma query que exiba o **nome completo**, **cep**, **rua** e **número de telefone** de **todos** os **professores**. (Dica: Use **LEFT JOIN** ou **RIGHT JOIN**)
8. Faça uma query que liste todos os **números de telefone** do banco de dados e caso haja um professor remetente exiba: **número de telefone** e **nome completo** do professor.

### Bônus

9. Faça uma query que exiba o **nome completo do estudante**, sua **tribo**, **número de telefone**, **cep**, **rua**, **cidade**, **estado** e **país**.
10. Faça uma query que liste todos os **endereços** do banco de dados e caso haja um estudante remetente exiba **cep**, **rua**, **cidade**  e **nome completo** do estudante.

## **Recursos Adicionais**

- https://www.w3schools.com/sql/sql_join.asp
- https://javascript.plainenglish.io/sql-understanding-joins-b5888eda54ae
- https://www.devmedia.com.br/sql-join-entenda-como-funciona-o-retorno-dos-dados/31006
- https://www.youtube.com/watch?v=165r4qUvp8Q