# Lab 2 - SQL

Monday, October 12, 2026

## Task

Write SQL statements to create these three tables:

- **Students:** `student_id` (integer, primary key), `student_name`.
- **Courses:** `course_id` (course code, primary key), `course_name`.
- **Enrollments:** `enrollment_id` (integer, primary key), `student_id`, `course_id`.

Link each enrollment to a student and a course using foreign keys.

If a student or course is deleted, their enrollments should be deleted too.

Then insert the data below.

## Students

| Student ID | Name |
| --- | --- |
| 46710 | Egecan |
| 40350 | Olcay |
| 46720 | Melisa |

## Courses

| Course ID | Course name |
| --- | --- |
| CS466 | Introduction to Deep Learning |
| CS104 | Introduction to Programming |
| CS202 | Database Management Systems |

## Enrollments

| Enrollment ID | Student ID | Course ID |
| --- | --- | --- |
| 101 | 46710 | CS202 |
| 102 | 40350 | CS466 |
| 103 | 46720 | CS104 |