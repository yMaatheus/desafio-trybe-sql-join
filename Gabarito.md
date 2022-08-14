## Sumário

- [Exercicios de Fixação](#exercicios-de-fixação)
- [Exercicios](#exercicios)

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

### Exercicios:



