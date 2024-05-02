Ciao @qui
Utilizzando lo stesso database della volta scorsa, eseguite le query in allegato.
Caricate un secondo file nella stessa repo di ieri db-university con le query di oggi.

## Group by
-Contare quanti iscritti ci sono stati ogni anno
-Contare gli insegnanti che hanno l'ufficio nello stesso edificio
-Calcolare la media dei voti di ogni appello d'esame
-Contare quanti corsi di laurea ci sono per ogni dipartimento

## Joins
-Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
-Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
-Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
-Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
-Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
-Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
-BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.
confermate lettura come al solito e buon divertimento :baby-yoda:


# Group by
1. Contare quanti iscritti ci sono stati ogni anno
    - SELECT YEAR(`enrolment_date`) AS 'year', COUNT(`id`) AS 'number_of_students_per_year' FROM `students` GROUP BY YEAR(`enrolment_date`) ORDER BY `year` DESC;
    - (risulta una tabella, ordinata dall'anno piu recente, con 4 righe: 2021-734, 2020-1645, 2019-1709, 2018-912)
2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
   - SELECT `office_address` , COUNT(id) AS 'number_of_teachers' FROM `teachers` GROUP BY `office_address` ORDER BY `number_of_teachers` DESC;
   - (risulta una tabella, ordinata dall'ufficio con più docenti, con tutti i vari office_address e il numero dei docenti che ne hanno l'ufficio)
3. Calcolare la media dei voti di ogni appello d'esame
   - SELECT `exam_id` , AVG(`vote`) AS 'average_vote' FROM `exam_student` GROUP BY `exam_id` ORDER BY `exam_id` ASC;
   - (risulta una tabella ordinata per l'id dell'esame e la relativa media dei voti)
4. Contare quanti corsi di laurea ci sono per ogni dipartimento
   - SELECT `department_id` , COUNT(`id`) AS 'number_of_degrees' FROM `degrees` GROUP BY `department_id` ORDER BY `department_id` ASC;
   - (risulta una tabella ordinata per l'id del dipartimento e il numero di corsi)

# Joins
1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
   - SELECT `students`.* , `degrees`.`name` AS 'degree_name' FROM `students` INNER JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` WHERE `degrees`.`name` = 'Corso di Laurea in Economia' ORDER BY `students`.`enrolment_date` DESC;
   - (risulta una tabella, ordinata dalla registrazione più recente, che contiene tutti gli studenti iscritti al corso di laurea economia)
2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
   - SELECT `degrees`.* , `departments`.`name`, `departments`.`address` FROM `degrees` INNER JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` WHERE `departments`.`name` = 'Dipartimento di Neuroscienze' AND `degrees`.`level` = 'magistrale' ORDER BY `degrees`.`id` ASC;
   - (risulta una tabella, ordinata per l'id del corso anche se ne risulta solo 1 per ora, che contiene tutti i corsi di laurea magistrale del dipartimento neuroscienze)
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
   - SELECT `teachers`.*, `courses`.`id` AS 'course_id', `courses`.`name` AS 'course_name' FROM `teachers` INNER JOIN `courses` ON `teachers`.`id` = `courses`.`id` WHERE `teachers`.`id` = 44 ORDER BY `courses`.`id` ASC;
   - (risulta una tabella, ordinata per l'id del corso anche se ne risulta solo 1 per ora, che contiene tutti i corsi in cui Fulvio Amato insegna)
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
   - SELECT `students`.*, `degrees`.`name` AS 'degree_name', `departments`.`name` AS 'department_name' FROM `students` INNER JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` INNER JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` ORDER BY `students`.`surname` ASC, `students`.`name` ASC;
   - (risulta una tabella, ordinata per cognome e nome, che contiene tutti gli studenti con i relativi corsi di laurea e il relativo dipartimento per ogni corso di laurea)
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
   - SELECT `degrees`.*, `teachers`.`name` AS 'teacher_name', `teachers`.`surname` AS 'teacher_surname', `courses`.`name` AS 'course_name', `courses`.`name` AS 'course_name' FROM `degrees` INNER JOIN `courses` ON `courses`.`degree_id` = `degrees`.`id` INNER JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id` INNER JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`course_id`;

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
   - SELECT DISTINCT `teachers`.*, `departments`.`name` AS 'department_name' FROM `teachers` INNER JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id` INNER JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id` INNER JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id` INNER JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` WHERE `departments`.`name` = 'Dipartimento di Matematica' ORDER BY `teachers`.`surname` ASC, `teachers`.`name` ASC;
   - (risulta una tabella, ordinata per cognome e nome, che contiene tutti i docenti che insegnano nel dipartimento di matematica)

