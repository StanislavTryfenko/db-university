## Esercizio di oggi

# nome repo: db-university

Dopo aver creato un nuovo database nel vostro phpMyAdmin e aver importato lo schema allegato, eseguite le query del file allegato.
Cosa consegnare?
Dopo aver testato le vostre query con phpMyAdmin, riportatele in un file query.md e caricatelo nella vostra repo.

-Selezionare tutti gli studenti nati nel 1990 (160)
-Selezionare tutti i corsi che valgono più di 10 crediti (479)
-Selezionare tutti gli studenti che hanno più di 30 anni
-Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)
-Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)
-Selezionare tutti i corsi di laurea magistrale (38)
-Da quanti dipartimenti è composta l'università? (12)
-Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

   Confermate lettura come al solito e buon divertimento :baby-yoda: :sql:

1. Selezionare tutti gli studenti nati nel 1990 (160)
   - SELECT * FROM `students` WHERE YEAR(`date_of_birth`) = 1990;
2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
   - SELECT * FROM `courses` WHERE `cfu` > 10;
3. Selezionare tutti gli studenti che hanno più di 30 anni (manca ma sono 3702, quando ho svolto l'esercizio perlomeno)
   - SELECT * FROM `students` WHERE `date_of_birth` < DATE_SUB(NOW(), INTERVAL 30 YEAR);
4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)
   - SELECT * FROM `courses` WHERE `period` = 'I semestre' AND `year` = 1;
5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)
   - SELECT * FROM `exams` WHERE TIME(`hour`) > '14:00:00' AND `date` = '2020-06-20';
6. Selezionare tutti i corsi di laurea magistrale (38)
   - SELECT * FROM `degrees` WHERE `level` = 'magistrale';
7. Da quanti dipartimenti è composta l'università? (12)
   - SELECT COUNT(*) FROM `departments`;
8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)
   - SELECT COUNT(*) FROM `teachers` WHERE `phone` IS NULL;