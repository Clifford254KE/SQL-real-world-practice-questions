# SQL-real-world-practice-questions

This is a practice that takes on 4 tables in a sql server. 

### The first table is called patients table containing the following fields:

patient_id	INT

first_name	TEXT

last_name	TEXT

gender	CHAR(1)

birth_date	DATE

city	TEXT

primary key icon	province_id	CHAR(2)

allergies	TEXT

height	INT

weight  INT

### Table 2 (admissions table) contains the following fields:

patient_id	INT

admission_date	DATE

discharge_date	DATE

diagnosis	TEXT

primary key icon	attending_doctor_id	INT

### Table 3 (doctors table): 

doctor_id	INT

first_name	TEXT

last_name	TEXT

specialty	TEXT

### Table 4 (province names)

province_id	CHAR(2)

province_name	TEXT


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
```

Show first name and last name of patients who does not have allergies. (null)`

```sql
SELECT first_name, last_name
FROM patients
WHERE allergies IS NULL;
```
Show first name of patients that start with the letter 'C'
```sql
SELECT first_name
FROM patients
WHERE first_name LIKE 'C%';
```
Show first name and last name of patients that weight within the range of 100 to 120 (inclusive)
```sql
SELECT first_name, last_name
FROM patients
WHERE weight>= 100 AND weight<=120;
```
Update the patients table for the allergies column. If the patient's allergies is null then replace it with 'NKA'
```
UPDATE patients
SET allergies = 'NKA'
WHERE allergies IS NULL;
```
Show first name and last name concatinated into one column to show their full name.
```
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM patients;
```
Show first name, last name, and the full province name of each patient.

Example: 'Ontario' instead of 'ON'
```
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
 ```  
Show how many patients have a birth_date with 2010 as the birth year.
```
SELECT COUNT(*) AS number_of_patients
FROM patients
WHERE YEAR(birth_date) = 2010;
```
Show the first_name, last_name, and height of the patient with the greatest height.
```
SELECT first_name, last_name, MAX(height) AS height
FROM patients
```
Show unique birth years from patients and order them by ascending.
```
SELECT
  DISTINCT YEAR(birth_date) AS birth_year
FROM patients
ORDER BY birth_year;
```
Show unique first names from the patients table which only occurs once in the list.

```sql
SELECT first_name
FROM patients
GROUP BY first_name
HAVING COUNT(first_name) = 1

or

SELECT first_name
FROM (
    SELECT
      first_name,
      count(first_name) AS occurrencies
    FROM patients
    GROUP BY first_name
  )
WHERE occurrencies = 1
HAVING COUNT(first_name) = 1
```
