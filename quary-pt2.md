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