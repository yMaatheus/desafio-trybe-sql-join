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

<!-- #TODO -->
- Utilizar JOIN para combinar dados de duas ou mais tabelas;
- Utilizar INNER JOIN para combinar dados de duas ou mais tabelas;
- Utilizar LEFT JOIN e RIGHT JOIN para combinar dados de duas ou mais tabelas;
- Utilizar SELF JOIN para fazer join de uma tabela com ela própria.

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

Como é visivel na imagem, temos um campo de dados comuns, para obtermos essas informações é necessário fazer uso de uma condição chamada **ON**, com ela podemos especificar qual é a coluna comum entre as tabelas. Vamos ver um pouco como é essa sintaxe na prática:

```
SELECT tabela1.coluna1, tabela2.coluna2
FROM tabela1
INNER JOIN tabela2
ON tabela1.coluna_em_comum1 = tabela2.coluna_em_comum2;
```

*A tradução desse comando ficaria: Selecione a coluna1 da tabela1, a coluna2 da tabela2 vindo da tabela1 juntando com a tabela2
onde a coluna_em_comum1 da tabela1 é igual a coluna_em_comum2 da tabela2*

Você consegue perceber quantas vezes precisamos dizer tabela1 e tabela2? Não é uma boa pratica fazermos isso, para isso temos um aliado, ou melhor, **alias**. Mas afinal, o que é um *alias*? Um alias é um apelido que podemos dar a uma tabela, é como chamar uma pessoa de nome José de Zé. Veja o exemplo usando o **AS**:

```
SELECT t1.coluna, t2.coluna
FROM tabela1 AS t1
INNER JOIN tabela2 AS t2
ON t1.coluna_em_comum = t2.coluna_em_comum;
```

Também é possivel omitir o **AS**:

```
SELECT t1.coluna, t2.coluna
FROM tabela1 t1
INNER JOIN tabela2 t2
ON t1.coluna_em_comum = t2.coluna_em_comum;
```

#### Na prática:

⚠️ Atencão! Para acompanhar os comandos e fazer o exercicio de fixação será necessário a utilização do banco de dados [Trybe ~~is cool~~ School](https://sqldeploys.github.io/desafio-join/TRYBE-IS-ChOOL.sql).

Algumas tabelas que vamos usar do nosso banco de dados:

[![teachers-subject-tribes-tables.png](https://i.postimg.cc/J0Mj9c5w/teachers-subject-tribes-tables.png)](https://postimg.cc/KkpKTTWQ)

Vamos exibir o primeiro nome do professor que ensina cada materia:

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

Exemplo de saida:

| id_da_materia | name                  | first_name | id_do_professor
| :-----------: | :-------------------: | :--------: | :-------------:
| 4             | Ciência da Computação | Matheus    | 1
| 1             | Fundamentos           | Rafael     | 2
| 2             | Front-end             | Alberto    | 3
| 3             | Back-end              | DjoDjo     | 4

#### Pra fixar:
1. Faça uma query que exiba o **nome da materia** e o **primeiro nome do professor**:
2. Faça uma query que exiba o **nome da materia** e o **sobrenome do professor**:
3. Faça uma query que exiba o **nome do professor** e a **tribo** que ele pertence.
4. Faça uma query que exiba o **nome da materia** e o **nome completo do professor**:
5. Faça uma query que exiba o **nome completo do professor** e a **tribo** que ele pertence.

### Como utilizar o LEFT JOIN e o RIGHT JOIN

Como foi visto o **INNER JOIN** vai buscar as informações em comum que existem nas tabelas, já o **LEFT JOIN**
vai exibir os dados da tabela da esquerda independente de haver algum dado em comum com a tabela da direita. Observe a imagem abaixo:

[![left-join.png](https://i.postimg.cc/P5YN9t9H/left-join.png)](https://postimg.cc/ZWYTyhJs)

Vale salientar que a tabela referente ao **LEFT JOIN** sempre será a após o **FROM**, mas para ficar claro a tradução de **LEFT** é esquerda e **RIGHT** direita. Veja abaixo como funciona na prática:

Essas são as tabelas do nosso banco de dados, vamos trabalhar com algumas delas abaixo:
[![all-tables.png](https://i.postimg.cc/MGb4c9cF/all-tables.png)](https://postimg.cc/jW2vmQ4H)

Vamos montar uma query que exibe o nome das pessoas estudantes de nossa escola e seu respectivo endereço utilizando o **LEFT JOIN**:

```
SELECT S.first_name, S.address_id, A.cep, A.street, A.number
FROM school.studants S
LEFT JOIN school.adresses A ON S.address_id = A.id;
```

Exemplo de saida:

[![saida-left-join.png](https://i.postimg.cc/W1zGBq3d/saida-left-join.png)](https://postimg.cc/G40TY2vR)

Como é possivel observar no exemplo acima, algumas pessoas estudantes possuem o **address_id** com valor **null**, só é possivel
vizualizar isso porque estamos utilizando o **LEFT JOIN**, vamos substituir o **LEFT** por **INNER** na nossa query e vamos comparar os
resultados:

```
SELECT S.first_name, S.address_id, A.cep, A.street, A.number
FROM school.studants S
INNER JOIN school.adresses A ON S.address_id = A.id;
```

Exemplo de saida:

[![saida-compare-left-inner-join.png](https://i.postimg.cc/9fKHd94Z/saida-compare-left-inner-join.png)](https://postimg.cc/Z98QZCx5)

Comparando os resultados é possivel observar que algumas pessoas estudantes foram ocultadas, essa é a diferença do **INNER JOIN** para **LEFT JOIN**.

Agora vamos para o **RIGHT JOIN**, veja a ilustração abaixo:

[![right-join.jpg](https://i.postimg.cc/Px5vwBwP/right-join.jpg)](https://postimg.cc/sBb2FHKr)

Como é ilustrado o **RIGHT JOIN** é o oposto do **LEFT JOIN**, ele representa a tabela da direita, vamos executar a mesma query usando o **RIGHT JOIN**:

```
SELECT S.first_name, S.address_id, A.cep, A.street, A.number
FROM school.studants S
RIGHT JOIN school.adresses A ON S.address_id = A.id;
```

Exemplo de saida:

[![saida-right-join.png](https://i.postimg.cc/bwYPppcD/saida-right-join.png)](https://postimg.cc/qzFSGf74)

#### Pra fixar:
1. Faça uma query que exiba o **nome de todas as pessoas estudantes** e seu **número de telefone**
2. Faça uma query que exiba o **nome de todos os professores** e seu **número de telefone**
3. Faça uma query que exiba **todos os numeros de telefone** com o **nome do professor** responsável por aquele número.
4. Faça uma query que exiba **todos os numeros de telefone** com o **nome da pessoa estudante** responsável por aquele número.

### O que é SELF JOIN e quando utilizar

A palavra **SELF** significa você mesmo, isso significa que faremos um **JOIN** na própria tabela que estamos manipulando.

[![homem-aranha-meme.jpg](https://i.postimg.cc/XY43s1Mn/homem-aranha-meme.jpg)](https://postimg.cc/SJTwsrNP)

No nosso banco de dados temos uma tabela de estudantes, lá existe uma coluna com nome de **buddie_id**, ela refere-se ao id de outra pessoa estudante, a qual, é sua parceira. Para listar todas as pessoas estudantes com seu respectivo buddie é necessário fazer um **SELF JOIN**. Veja na prática:

```
SELECT Studant.first_name, Studant.buddie_id, Buddie.first_name
FROM school.studants Studant
INNER JOIN school.studants Buddie ON Studant.buddie_id = Buddie.id;
```

Siim! Você não viu errado, o **SELF JOIN** na verdade é apenas um **INNER JOIN** na própria tabela. Mas também podemos apenas declarar
a mesma tabela duas vezes, dessa forma:

```
SELECT Studant.first_name, Studant.buddie_id, Buddie.first_name
FROM school.studants Studant, school.studants Buddie
WHERE Studant.buddie_id = Buddie.id;
```

Exemplo de saida:

[![saida-self-join.png](https://i.postimg.cc/TY8CMZ3v/saida-self-join.png)](https://postimg.cc/JtqbjYXp)

#### Pra fixar:
1. Exiba o **nome completo** do **estudante** e do seu **parceiro**

## **Vamos praticar!**
Vamos bater um papo sobre SQL? Hora da aula ao vivo! Vamos para o Slack, onde o link estará disponível.
## **Exercicios**

### Agora na prática

1.
2.
3.
4.
5.

### Bônus

6.

## **Recursos Adicionais**

- https://www.w3schools.com/sql/sql_join.asp
- https://javascript.plainenglish.io/sql-understanding-joins-b5888eda54ae
- https://www.devmedia.com.br/sql-join-entenda-como-funciona-o-retorno-dos-dados/31006