# GROUP BY
# 1. Contare quanti iscritti ci sono stati ogni anno
SELECT COUNT(`id`) as `students_enrolled`, YEAR(`students`.`enrolment_date`) as `year`
FROM `students`
GROUP BY YEAR(`enrolment_date`);

# 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
SELECT COUNT(`id`) as `number_of_teachers`, `office_address`
FROM `teachers`
GROUP BY `office_address`;

# 3. Calcolare la media dei voti di ogni appello d'esame
SELECT `exam_id`, 
AVG(`vote`) as `average_vote`
FROM `exam_student`
GROUP BY (`exam_id`);

# 4. Contare quanti corsi di laurea ci sono per ogni dipartimento
SELECT COUNT(*) as `degrees`,
`department_id`
FROM `degrees`
GROUP BY (`department_id`);


# JOIN
# 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
SELECT `students`.`id` as `student_id`,
`students`.`name` as `student_name`,
`students`.`surname` as `student_surname`,
`degrees`.`name` as `degree_name`
FROM `students`
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

# 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
SELECT `departments`.`name` as `department`,
`degrees`.`name` as `degrees`
FROM `degrees`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze'
AND `degrees`.`level` = 'magistrale';

# 3. Selezionare tutti i corsi in cui insegna Fulvio Amato
SELECT `teachers`.`name` as `teacher_name`,
`teachers`.`surname` as `teacher_surname`,
`courses`.`name` as `course_name`,
`courses`.`description` as `course_description`,
`courses`.`period` as `course_period`,
`courses`.`year` as `course_year`,
`courses`.`cfu` as `course_cfu`
FROM `teachers`
JOIN `course_teacher` ON `course_teacher`.`teacher_id` = `teachers`.`id`
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
WHERE `teachers`.`name` = 'Fulvio' AND `teachers`.`surname` = 'Amato';

# 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
SELECT `students`.`surname` as `student_surname`,
`students`.`name` as `student_name`,
`degrees`.`name` as `degree_name`,
`degrees`.`level` as `degree_level`,
`departments`.`name` as `department`
FROM `students`
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname`, `students`.`name`;

# 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti 
SELECT `degrees`.`name` as `degree`,
`courses`.`name` as `course_name`,
`courses`.`description` as `course_description`,
`teachers`.`name` as `teacher_name`,
`teachers`.`surname` as `teacher_surname`
FROM `degrees`
JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`;

# 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica
SELECT `teachers`.`name` as `teacher_name`,
`teachers`.`surname` as `teacher_surname`,
`departments`.`name` as `department`
FROM `teachers`
JOIN `course_teacher` ON `course_teacher`.`teacher_id` = `teachers`.`id`
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id`
JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` = 'Dipartimento di Matematica';

# 7. Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo


