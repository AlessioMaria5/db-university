ESERCIZIO BOOLEAN PHPMYADMIN	


ESERCIZIO SELECT

1. Selezionare tutti gli studenti nati nel 1990(160) SELECT * FROM `students` WHERE YEAR(`date_of_birth`) = 1990; 
2. Selezionare tutti i corsi che valgono piu di 10 crediti (479) SELECT * FROM `courses` WHERE `cfu` > 10; 
3. Selezionare tutti gli studenti che hanno piu di 30 anni  SELECT * FROM `students` WHERE YEAR(CURRENT_DATE) - YEAR(`date_of_birth`) >= 30; 
4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea ( 286) SELECT * FROM `courses` WHERE `period` = "I semestre" AND `year` = "1"; 
5. Selezionare tutti gli appelli d’esame che avvengono nel pomeriggio ( dopo le 14 ) del 20/06/2020 ( 21 ) SELECT * FROM `exams` WHERE `date` = DATE("2020-06-20") AND HOUR(`hour`) >= HOUR("14:00:00"); 
6. Selezionare tutti i corsi di laurea magistrale ( 38 ) SELECT * FROM `degrees` WHERE `level` = "magistrale"; 
7. Da quanti dipartimenti è composta l’università? ( 12 ) SELECT COUNT(*) AS "totale_dipartimenti" FROM `departments`; 
8. Quanti sono gli insegnanti che non hanno un numero di telefono?  (50)SELECT * FROM `teachers` WHERE `phone` IS NULL; 

ESERCI∑IO GROUP_BY1. 


1. Contare quanti iscritti ci sono stati ogni anno 
SELECT COUNT(*), YEAR(`enrolment_date`) FROM `students` GROUP BY YEAR(`enrolment_date`);

2. Contare gli insegnanti che hanno l’ufficio nello stesso edificio
SELECT COUNT(*), `office_address` FROM `teachers` GROUP BY `office_address`;

3. Calcolare la media dei voti di ogni appello d’esame
SELECT TRUNCATE(AVG(`vote`),0), `exam_id` FROM `exam_student` GROUP BY `exam_id`

4. Contare quanti corsi di laurea ci sono per ogni dipartimento
SELECT COUNT(*) AS "numero_corsi" , `department_id` FROM `degrees` GROUP BY `department_id`; 


1.
 
Selezionare tutti gli studenti iscritti al Corso di
 
Laurea in Economia

SELECT * FROM `students` JOIN `degrees` ON students.degree_id = degrees.id WHERE degrees.name = "Corso di Laurea in Economia";


SELECT students.name, students.surname, students.id, degrees.name FROM `students` JOIN `degrees` ON students.degree_id = degrees.id WHERE degrees.name = "Corso di Laurea in Economia";





2.
 
Selezionare tutti i Corsi di Laurea del Dipartimento
 
di Neuroscienze

SELECT DISTINCT degrees.name , departments.name FROM `courses` JOIN `degrees` ON courses.degree_id = degrees.id JOIN `departments` ON degrees.department_id = departments.id WHERE departments.name LIKE "%Neuroscienze%";



3.
 
Selezionare tutti i corsi in cui insegna Fulvio Amato
 
(id=44)

SELECT teachers.name , teachers.surname , course_teacher.course_id , degrees.name , courses.name FROM `teachers` JOIN `course_teacher` ON course_teacher.teacher_id = teachers.id JOIN `courses` ON teachers.id = courses.id JOIN `degrees` ON courses.degree_id = degrees.id WHERE course_teacher.teacher_id = 44;


4.
 
Selezionare tutti gli studenti con i dati relativi
 
al corso di laurea a cui sono iscritti e il

relativo dipartimento, in ordine alfabetico per cognome
 
e nome

SELECT * FROM `students` JOIN `degrees` ON students.degree_id = degrees.id JOIN `departments` ON degrees.department_id = departments.id ORDER BY students.surname ASC, students.name ASC;

5.
 
Selezionare tutti i corsi di laurea con i relativi
 
corsi e insegnanti

SELECT teachers.name , teachers.surname , degrees.name , courses.name , courses.id FROM `degrees` JOIN `courses` ON courses.degree_id = degrees.id JOIN `teachers` ON courses.id = teachers.id;

6.
 
Selezionare tutti i docenti che insegnano nel Dipartimento
 
di Matematica (54)

SELECT DISTINCT departments.name , teachers.name , teachers.surname FROM `teachers` JOIN `course_teacher` ON course_teacher.teacher_id = teachers.id JOIN `courses` ON courses.id = course_teacher.course_id JOIN `degrees` ON degrees.id = courses.degree_id JOIN `departments` ON departments.id = degrees.department_id WHERE departments.name = "Dipartimento di Matematica" ORDER BY teachers.surname ASC;
