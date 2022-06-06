1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia.

SELECT `students`.*, `degrees`.`name` 
FROM `students` 
JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id` 
WHERE `degrees`.`name` = 'Corso di Laurea in Economia'


2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze.

SELECT `degrees`.*, `departments`.`name` 
FROM `degrees` 
JOIN `departments` ON `departments`.`id` = `degrees`.`department_id` 
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze' AND `degrees`.`level` = 'magistrale';

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44).

SELECT `courses`.*, `teachers`.`name`, `teachers`.`surname` 
FROM `courses` 
JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id` 
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id` 
WHERE `teachers`.`id` = 44;

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome.

SELECT `students`.`name`, `students`.`surname`, `degrees`.*, `departments`.`name` 
FROM `students` 
JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id` 
JOIN `departments` ON `departments`.`id` = `degrees`.`department_id` 
ORDER BY `students`.`surname` ASC;


5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti.

SELECT `degrees`. `name` AS "Nome corso di laurea", `courses` . `name` AS "Nome corso singolo", `teachers`.`name` AS "Nome prof",`teachers`.`surname` AS "Cognome prof" 
FROM `degrees` 
JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id` 
JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id` 
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
ORDER BY "Nome corso di laurea"

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

SELECT DISTINCT `teachers`.`name` AS "Nome prof",`teachers`.`surname` AS "Cognome prof" , `departments`.`name` AS "Nome del Dipartimento"
FROM `teachers`
JOIN `course_teacher`ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Matematica';

7. BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami
