1. Contare quanti iscritti ci sono stati ogni anno.

SELECT DISTINCT YEAR(enrolment_date) As "anni", COUNT(id) As "numero degli studenti"
FROM `students`
GROUP BY `enrolment_date`

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio.

SELECT `office_address`, COUNT(`id`) AS "numero dei prof"
FROM `teachers`
GROUP BY `office_address`

3. Calcolare la media dei voti di ogni appello d'esame

SELECT AVG(`vote`) AS "media dei voti",`exam_id`  AS "sessione"
FROM `exam_student` 
GROUP by `exam_id`;

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

SELECT (`department_id`) AS "dipartimento" , COUNT(`id`) AS "numero dei corsi di laurea"
FROM `degrees`
GROUP BY `department_id`;