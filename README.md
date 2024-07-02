## Descrizione:

```txt
Usate il database che avete creato a lezione
per eseguire le query del file allegato.
```

## Query da eseguire:

1. [Selezionare tutti gli studenti nati nel 1990](#query-1) (160) &check;
2. [Selezionare tutti i corsi che valgono più di 10 crediti](#query-2) (479) &check;
3. [Selezionare tutti gli studenti che hanno più di 30 anni](#query-3) &check;
4. [Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea](#query-4) (286) &check;
5. [Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020](#query-5) (21) &check;
6. [Selezionare tutti i corsi di laurea magistrale](#query-6) (38) &check;
7. [Da quanti dipartimenti è composta l'università?](#query-7) (12) &check;
8. [Quanti sono gli insegnanti che non hanno un numero di telefono?](#query-8) (50) &check;
9. [Inserire nella tabella degli studenti un nuovo record con i propri dati (per il campo degree_id, inserire un valore casuale)](#query-9) &check;
10. [Cambiare il numero dell’ufficio del professor Pietro Rizzo in 126](#query-10) &check;
11. [Eliminare dalla tabella studenti il record creato precedentemente al punto 9](#query-11) &check;

## Svolgimento:

- #### Query 1
  Selezionare tutti gli studenti nati nel 1990 (160) &check;

```bash
SELECT
    *
FROM
    `students`
WHERE
    YEAR(`date_of_birth`) = 1990;
```

- #### Query 2
  Selezionare tutti i corsi che valgono più di 10 crediti (479) &check;

```bash
SELECT
    *
FROM
    `courses`
WHERE
    `cfu` > 10;
```

- #### Query 3
  Selezionare tutti gli studenti che hanno più di 30 anni &check;

```bash
SELECT
    *
FROM
    `students`
WHERE
    TIMESTAMPDIFF(YEAR, `date_of_birth`, CURDATE()) > 30;
```

- #### Query 4
  Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di &check;
  laurea (286)

```bash
SELECT
    *
FROM
    `courses`
WHERE
    `period` = 'I semestre' AND `year` = 1;
```

- #### Query 5
  Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
  20/06/2020 (21) &check;

```bash
SELECT
    *
FROM
    `exams`
WHERE
    DATE(`date`) = '2020-06-20' AND HOUR(`hour`) > 14;
```

- #### Query 6
  Selezionare tutti i corsi di laurea magistrale (38) &check;

```bash
SELECT
    *
FROM
    `degrees`
WHERE
    `level` = 'magistrale';
```

- #### Query 7
  Da quanti dipartimenti è composta l'università? (12) &check;

```bash
SELECT
    COUNT(`id`)
FROM
    `departments`;
```

- #### Query 8
  Quanti sono gli insegnanti che non hanno un numero di telefono? (50) &check;

```bash
SELECT
    COUNT(`id`)
FROM
    `teachers`
WHERE
    `phone` IS NULL OR `phone` = '';
```

- #### Query 9
  Inserire nella tabella degli studenti un nuovo record con i propri dati (per il campo
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
    28, 'Alessandro', 'Palumbo', '1996-02-29', 'PLMLSN96B29G999T', '2024-07-01', 999999, 'alessandro1palumbo@gmail.com');
```

- #### Query 10
  Cambiare il numero dell’ufficio del professor Pietro Rizzo in 126 &check;

```bash
UPDATE
    `teachers`
SET
    `office_number` = '126'
WHERE
    `name` = 'Pietro' AND `surname` = 'Rizzo';
```

- #### Query 11
  Eliminare dalla tabella studenti il record creato precedentemente al punto 9 &check;

```bash
DELETE
FROM
    `students`
WHERE
    `id` = (SELECT `id` FROM(SELECT `id` FROM `students` ORDER BY `id` DESC LIMIT 1) AS `temp`) ;

    # elimina sempre la riga con l' id più alto ordinando tutte le righe in ordine decrescente dell' id e prendendo solo la prima riga(quindi quella con l'id più alto)
```
