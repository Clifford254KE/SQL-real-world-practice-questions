# SQL-real-world-practice-questions
```sql
SELECT * FROM patients

SELECT city, COUNT(city) AS city1, height
FROM patients
GROUP BY city
ORDER BY city1 ASC,height;

SELECT gender, COUNT(gender) AS gender_count
FROM patients
group by gender;


SELECT first_name, last_name, gender
FROM patients
WHERE gender = 'M';

Show first name and last name of patients who does not have allergies. (null)

SELECT first_name, last_name
FROM patients
WHERE allergies IS NULL;

Show first name of patients that start with the letter 'C'

SELECT first_name
FROM patients
WHERE first_name LIKE 'C%';

Show first name and last name of patients that weight within the range of 100 to 120 (inclusive)

SELECT first_name, last_name
FROM patients
WHERE weight>= 100 AND weight<=120;

Update the patients table for the allergies column. If the patient's allergies is null then replace it with 'NKA'

UPDATE patients
SET allergies = 'NKA'
WHERE allergies IS NULL;

Show first name and last name concatinated into one column to show their full name.

SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM patients;

Show first name, last name, and the full province name of each patient.

Example: 'Ontario' instead of 'ON'

SELECT
    p.first_name,
    p.last_name,
    pr.province_name
FROM
    patients AS p
JOIN
    province_names AS pr
ON
    p.province_id = pr.province_id;
   
Show how many patients have a birth_date with 2010 as the birth year.

SELECT COUNT(*) AS number_of_patients
FROM patients
WHERE YEAR(birth_date) = 2010;

Show the first_name, last_name, and height of the patient with the greatest height.

SELECT first_name, last_name, MAX(height) AS height
FROM patients

Show unique birth years from patients and order them by ascending.

SELECT
  DISTINCT YEAR(birth_date) AS birth_year
FROM patients
ORDER BY birth_year;
```
