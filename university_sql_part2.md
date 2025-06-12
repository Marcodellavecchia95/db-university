1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

SELECT `students`.\*
FROM `students`
INNER JOIN `degrees`
ON `degrees`.`id` = `students`.`degree_id`
WHERE `degrees`.`name`= "Corso di Laurea in Economia";

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

SELECT \*
FROM `degrees`
INNER JOIN `departments`
ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` = "Dipartimento di Neuroscienze"
AND `degrees`.`level` = "magistrale";

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

SELECT `courses`.\*,
`teachers`.`name`,
`teachers`.`surname`
FROM `courses`
INNER JOIN `teachers`
ON `teachers`.`id`= `courses`.`id`
WHERE `teachers`.`id`= 44;

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
   sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
   nome

   SELECT \*
   FROM `students`
   INNER JOIN `degrees`
   ON `students`.`degree_id` = `degrees`.`id`

INNER JOIN `courses`
ON `courses`.`degree_id` = `degrees`.`id`

ORDER BY `students`.`surname`, `students`.`name`;

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

SELECT \*
FROM `degrees`
INNER JOIN `courses`
ON `degrees`.`id`= `courses`.`degree_id`
INNER JOIN `teachers`
ON `teachers`.`id`=`courses`.`id`;

6. Selezionare tutti i docenti che insegnano nel Dipartimento di
   Matematica (54)

SELECT `teachers`. \*
FROM `teachers`
INNER JOIN `course_teacher`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
INNER JOIN `courses`
ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `degrees`
ON `courses`.`degree_id`=`degrees`.`id`
INNER JOIN `departments`
ON `degrees`.`department_id`=`departments`.`id`
WHERE `departments`.`name`= "Dipartimento di Matematica"
GROUP BY `teachers`.`id`;

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
   per ogni esame, stampando anche il voto massimo. Successivamente,

SELECT `students`.\*, COUNT(`exam_student`.`exam_id`) AS exams_taken , MAX(`exam_student`.`vote`) AS max_vote
FROM `students`
INNER JOIN `exam_student`
ON `students`.`id` = `exam_student`.`student_id`
WHERE `exam_student`.`vote`> 18
GROUP BY `students`.`id`;
