## Descrizione:

```txt
Usate il database che avete creato a lezione
per eseguire le query del file allegato.
```

## Query da eseguire:

1. Selezionare tutti gli studenti nati nel 1990 (160) &check;
2. Selezionare tutti i corsi che valgono più di 10 crediti (479) &check;
3. Selezionare tutti gli studenti che hanno più di 30 anni &check;
4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
   laurea (286) &check;
5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
   20/06/2020 (21) &check;
6. Selezionare tutti i corsi di laurea magistrale (38) &check;
7. Da quanti dipartimenti è composta l'università? (12) &check;
8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50) &check;
9. Inserire nella tabella degli studenti un nuovo record con i propri dati (per il campo
   degree_id, inserire un valore casuale) &check;
10. Cambiare il numero dell’ufficio del professor Pietro Rizzo in 126 &check;
11. Eliminare dalla tabella studenti il record creato precedentemente al punto 9

## Svolgimento:

1. Selezionare tutti gli studenti nati nel 1990 (160) &check;

```bash
SELECT
    *
FROM
    `students`
WHERE
    YEAR(`date_of_birth`) = '1990';
```

2. Selezionare tutti i corsi che valgono più di 10 crediti (479) &check;

```bash
SELECT
    *
FROM
    `courses`
WHERE
    `cfu` > '10';
```

3. Selezionare tutti gli studenti che hanno più di 30 anni &check;

```bash
SELECT
    *
FROM
    `students`
WHERE
    TIMESTAMPDIFF(YEAR, `date_of_birth`, CURDATE()) > 30;
```

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di &check;
   laurea (286)

```bash
SELECT
    *
FROM
    `courses`
WHERE
    `period` = 'I Semestre' AND `year` = '1';
```

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
   20/06/2020 (21) &check;

```bash
SELECT
    *
FROM
    `exams`
WHERE
    DATE(`date`) = '2020-06-20' AND TIME(`hour`) > '14:00:00';
```

6. Selezionare tutti i corsi di laurea magistrale (38) &check;

```bash
SELECT
    *
FROM
    `degrees`
WHERE
    `level` = 'magistrale';
```

7. Da quanti dipartimenti è composta l'università? (12) &check;

```bash
SELECT
    COUNT(*)
FROM
    `departments`;
```

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50) &check;

```bash
SELECT
    COUNT(*)
FROM
    `teachers`
WHERE
    `phone` IS NULL;
```

9. Inserire nella tabella degli studenti un nuovo record con i propri dati (per il campo
   degree_id, inserire un valore casuale) &check;

```bash
INSERT INTO `students`(
    `degree_id`,
    `name`,
    `surname`,
    `date_of_birth`,
    `fiscal_code`,
    `enrolment_date`,
    `registration_number`,
    `email`
)
VALUES(
    FLOOR(1 +(RAND() * 100) + 1), 'Alessandro', 'Palumbo', '1996-02-29', 'PLMLSN96B29G999T', '2024-07-01', 999999, 'alessandro1palumbo@gmail.com');
```

10. Cambiare il numero dell’ufficio del professor Pietro Rizzo in 126 &check;

```bash
UPDATE
    `teachers`
SET
    `office_number` = '126'
WHERE
    `name` = 'Pietro' AND `surname` = 'Rizzo';
```

11. Eliminare dalla tabella studenti il record creato precedentemente al punto 9 &cross;

```bash

```
