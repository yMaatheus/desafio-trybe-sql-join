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

![Imagem Inner Join](https://arquivo.devmedia.com.br/cursos/SQL_2199/inner.png)

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

No nosso banco de dados temos as seguintes tabelas:

[![tabelas](https://i.postimg.cc/437wxPWG/tabelas.png)](https://postimg.cc/t1bFr30v)

Vamos exibir o primeiro nome do professor que ensina cada materia:

<!-- TODO Colocar versão sem CONCAT e depois mostrar o com concat -->

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
| 3             | Back-end              | Djo        | 4

#### Pra fixar:
<!-- #TODO -->
1. Faça uma query que exiba o nome da materia e o primeiro nome do professor
2. Faça uma query que exiba o nome da materia e o sobrenome do professor
3. 

### Como utilizar o LEFT JOIN e o RIGHT JOIN

Como foi visto o **INNER JOIN** vai buscar as informações em comum que existem nas tabelas, já o **LEFT JOIN**
vai exibir os dados da tabela da esquerda independente de haver algum dado em comum com a tabela da direita. Observe a imagem abaixo:

[![left-join.png](https://i.postimg.cc/P5YN9t9H/left-join.png)](https://postimg.cc/ZWYTyhJs)


### O que é SELF JOIN e quando utilizar



## **Vamos praticar!**
Vamos bater um papo sobre SQL? Hora da aula ao vivo! Vamos para o Slack, onde o link estará disponível.
## **Exercicios**

### Agora na prática

### Bônus

## **Recursos Adicionais**

- https://www.w3schools.com/sql/sql_join.asp
- https://javascript.plainenglish.io/sql-understanding-joins-b5888eda54ae
- https://www.devmedia.com.br/sql-join-entenda-como-funciona-o-retorno-dos-dados/31006