# Contare quanti iscritti ci sono stati ogni anno
SELECT COUNT(id) as students_enrolled, YEAR(students.enrolment_date) as year
FROM students
GROUP BY YEAR(enrolment_date);

# Contare gli insegnanti che hanno l'ufficio nello stesso edificio
SELECT COUNT(id) as number_of_teachers, office_address
FROM teachers
GROUP BY office_address;

# Calcolare la media dei voti di ogni appello d'esame
SELECT exam_id, 
AVG(exam_student.vote) as average_vote
FROM exam_student
GROUP BY (exam_id);