## Sumário

- [Exercicios de Fixação](#exercicios-de-fixação)
  - [INNER JOIN](#inner-join)
  - [LEFT JOIN e RIGHT JOIN](#left-join-e-right-join)
  - [SELF JOIN](#self-join)
- [Exercicios](#exercicios)
  - [Agora na prática:](#agora-na-prática)
  - [Bônus](#bônus)

## Gabarito

<!-- TODO Colocar saida esperada de todos os exercicios -->
### Exercicios de Fixação:

#### **INNER JOIN**

1. Exibe nome da materia, primeiro nome do professor:

```
SELECT S.name AS materia, T.first_name AS nome_professor
FROM school.subjects S
INNER JOIN school.teachers T ON S.teacher_id = T.id;
```

2. Exibe nome da materia, sobrenome do professor:

```
SELECT S.name AS materia, T.last_name AS sobrenome_professor
FROM school.subjects S
INNER JOIN school.teachers T ON S.teacher_id = T.id;
```

3. Exibe o nome do professor e a tribo:

```
SELECT T.first_name nome_professor, TR.name tribo
FROM school.teachers T
INNER JOIN school.tribes TR ON T.id = TR.teacher_id;
```

4. Exibe o nome da materia e nome completo do professor:

```
SELECT S.name AS materia, CONCAT(T.first_name, ' ', T.last_name) AS nome_completo_professor
FROM school.subjects S
INNER JOIN school.teachers T ON S.teacher_id = T.id;
```

5. Exibe o nome completo do professor e a tribo:

```
SELECT CONCAT(T.first_name, ' ', T.last_name) nome_completo_professor, TR.name tribo
FROM school.teachers T
INNER JOIN school.tribes TR ON T.id = TR.teacher_id;
```

#### **LEFT JOIN** e **RIGHT JOIN**

1. Exibe o nome de todas as pessoas esutantes com número de telefone:

```
SELECT S.first_name AS pessoa_estudante, P.phone AS telefone
FROM school.studants S
LEFT JOIN school.phones P ON S.phone_id = P.id;
```

2. Exibe o nome de todos os professores com número de telefone:

```
SELECT T.first_name AS nome_professor, P.phone AS telefone
FROM school.teachers T
LEFT JOIN school.phones P ON T.phone_id = P.id;
```

3. Exibe todos os números de telefone com o nome do respectivo professor:

```
SELECT T.first_name AS nome_professor, P.phone AS telefone
FROM school.teachers T
RIGHT JOIN school.phones P ON T.phone_id = P.id;
```

também pode ser feito assim:

```
SELECT T.first_name AS nome_professor, P.phone
FROM school.phones P
LEFT JOIN school.teachers T ON P.id = T.phone_id;
```

4. Exibe todos os números de telefone com o nome da pessoa estudante remetente:

```
SELECT S.first_name AS pessoa_estudante, P.phone AS telefone
FROM school.studants S
RIGHT JOIN school.phones P ON S.phone_id = P.id;
```

também pode ser feito assim:

```
SELECT S.first_name AS pessoa_estudante, P.phone AS telefone
FROM school.phones P
LEFT JOIN school.studants S ON P.id = S.phone_id;
```

#### **SELF JOIN**

1. Exiba o **nome completo** do **estudante** e do seu **parceiro**

```
SELECT
 CONCAT(S.first_name, ' ', S.last_name) AS nome_completo_estudante,
 CONCAT(B.first_name, ' ', B.last_name) AS nome_completo_buddie
FROM school.studants S
INNER JOIN school.studants B ON S.buddie_id = B.id;
```

### Exercicios:

#### Agora na prática:

1. Faça uma query que exiba **quantos estudantes** existem por **tribo**.

```
SELECT TRI.name AS tribo, COUNT(TRI.id) AS quantidade_estudantes FROM school.studants S
INNER JOIN school.tribes TRI ON S.tribe_id = TRI.id
GROUP BY TRI.id;
```

2. Faça uma query que conte **quantas duplas** de **buddies** existem no banco de dados.

```
SELECT (COUNT(*) / 2) AS quantidades_de_duplas FROM school.studants S
INNER JOIN school.studants B ON S.buddie_id = B.id;
```

3. Faça uma query que exiba **nome completo**, **cep**, **rua** e **número de telefone** de professores que **possuem** endereço e telefone.

```
SELECT
 CONCAT(T.first_name, ' ', T.last_name) nome_completo_professor,
 A.cep,
 A.street,
 P.phone
FROM school.teachers T
INNER JOIN school.adresses A ON T.address_id = A.id
INNER JOIN school.phones P ON T.phone_id = P.id;
```

4. Faça uma query que exiba **quantos estudantes possuem endereço registrado**.

```
SELECT COUNT(*) AS quantidade_estudantes_com_endereco FROM school.studants S
INNER JOIN school.adresses A ON S.address_id = A.id;
```

5. Faça uma query que exiba o **nome completo do estudante**, **cep**, **rua**, **número**, **cidade** e **estado**.

```
SELECT
 CONCAT(S.first_name, ' ', S.last_name) nome_completo_estudante,
 A.cep,
 A.street,
 A.number,
 C.city,
 STA.state
FROM school.studants S
INNER JOIN school.adresses A ON S.address_id = A.id
INNER JOIN school.cities C ON A.city_id = C.id
INNER JOIN school.states STA ON C.state_id = STA.id;
```

6. Faça uma query que exiba **quantos estudantes residem por estado** em **ordem decrescente**.

```
SELECT
 STA.state,
 STA.state_code,
 COUNT(STA.id) AS quantidade_de_estudante_por_estado
FROM school.studants S
INNER JOIN school.adresses A ON S.address_id = A.id
INNER JOIN school.cities C ON A.city_id = C.id
INNER JOIN school.states STA ON C.state_id = STA.id
GROUP BY C.state_id 
ORDER BY quantidade_de_estudante_por_estado DESC;
```

7. Faça uma query que exiba o **nome completo**, **cep**, **rua** e **número de telefone** de **todos** os **professores**.

```
SELECT
 CONCAT(T.first_name, ' ', T.last_name) nome_completo_professor,
 A.cep,
 A.street,
 P.phone
FROM school.teachers T
LEFT JOIN school.adresses A ON T.address_id = A.id
LEFT JOIN school.phones P ON T.phone_id = P.id;
```

8. Faça uma query que liste todos os **números de telefone** do banco de dados e caso haja um professor remetente exiba: **número de telefone** e **nome completo** do professor.

```
SELECT
 P.phone,
 CONCAT(T.first_name, ' ', T.last_name) nome_completo_professor
FROM school.teachers T
RIGHT JOIN school.phones P ON T.phone_id = P.id;
```
#### Bônus

9. Faça uma query que exiba o **nome completo do estudante**, sua **tribo**, **número de telefone**, **cep**, **rua**, **cidade**, **estado** e **país**.

```
SELECT 
 CONCAT(S.first_name, ' ', S.last_name) AS nome_completo_estudante,
 TRI.name,
 P.phone,
 A.cep,
 A.street,
 A.number,
 C.city,
 STA.state,
 CO.country
FROM school.studants S
INNER JOIN school.tribes TRI ON S.tribe_id = TRI.id
INNER JOIN school.phones P ON S.phone_id = P.id
INNER JOIN school.adresses A ON S.address_id = A.id
INNER JOIN school.cities C ON A.city_id = C.id
INNER JOIN school.states STA ON C.state_id = STA.id
INNER JOIN school.countries CO ON STA.country_id = CO.id;
```

10. Faça uma query que liste todos os **endereços** do banco de dados e caso haja um estudante remetente exiba **cep**, **rua**, **cidade**  e **nome completo** do estudante.

```
SELECT
 A.cep,
 A.street,
 C.city,
 CONCAT(S.first_name, ' ', S.last_name) nome_completo_estudante
FROM school.studants S
RIGHT JOIN school.adresses A ON S.address_id = A.id 
INNER JOIN school.cities C ON A.city_id = C.id;
```