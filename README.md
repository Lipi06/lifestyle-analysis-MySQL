# lifestyle_analysis
Welcome to the mysql analysis project of lifestyle data. 
-- Analysation begins of The Lifestyle Data--
use lifestyle;

SELECT 
    *
FROM
    health_data;

-- showing female and male data--
SELECT 
    *
FROM
    health_data
WHERE
    Gender = 'Female';
SELECT 
    *
FROM
    health_data
WHERE
    Gender = 'Male';

SELECT 
    COUNT(Gender)
FROM
    health_data
WHERE
    Gender = 'Female';
SELECT 
    COUNT(Gender)
FROM
    health_data
WHERE
    Gender = 'Male';
    
-- avg age-- 
SELECT 
    AVG(Age)
FROM
    health_data;

-- Common Occupation--
SELECT 
    MAX(Occupation)
FROM
    health_data;
    
-- average quality of sleep--
SELECT 
    AVG(`Quality of Sleep`)
FROM
    health_data;
    
-- average Sleep Duration--
SELECT 
    AVG(`Sleep Duration`)
FROM
    health_data;

-- Are there any individuals with extremely low physical activity--
SELECT 
    Personid, Age, Gender, `Daily Steps`
FROM
    health_data
WHERE
    `Daily Steps` < 4000;
    
-- Relation between Physical Activity, Stress lever--
   SELECT 
   `Physical Activity Level`, `Stress Level`              
FROM
    health_data; 
    
-- ..... Occupation-specific Analysis ..... --
-- What is the average stress level for individuals in each occupation?
select avg(`Stress Level`) as 'Overall stress', Occupation from health_data 
group by Occupation;

-- Which occupation has the highest percentage of individuals with a sleep disorder?--
select count(Personid) from health_data;
select distinct(Occupation) from health_data;
select count(Personid) as 'Overall count', Occupation from health_data where `Sleep Disorder` != 'None'
group by Occupation;

-- Do people in certain occupations tend to have longer sleep durations than others?
select max(`Sleep Duration`) as 'Sleep Duration', Occupation from health_data 
group by Occupation;

-- Data Filtering--
-- How many individuals have a high stress level and a sleep disorder?--
select max(`Stress Level`) from health_data;
SELECT 
    COUNT(Personid)
FROM
    health_data
WHERE
    `Stress Level` = 8
        and `Sleep Disorder` != 'None';

-- Who are the individuals with a BMI category Overweight and high blood pressure?--
select max(`Blood Pressure`) from health_data;
SELECT 
    Personid, `BMI category`, `Blood Pressure`, Occupation
FROM
    health_data
WHERE
    `BMI category` = 'Overweight'
        and `Blood Pressure` >= 120
order by Personid;

-- overall distribution of BMI categories--
SELECT DISTINCT
    (`BMI Category`), COUNT(Personid)
FROM
    health_data
GROUP BY `BMI Category`;
SELECT DISTINCT
    (`BMI Category`), AVG(Age)
FROM
    health_data
GROUP BY `BMI Category`;

    
-- Specials--
-- how many of them are obsese above age 40--
SELECT 
    Age, `BMI Category`, Gender
FROM
    health_data
WHERE
    `BMI Category` = 'Obese' AND age > 40;
    
-- avg age--
SELECT 
    Personid, Age, Occupation
FROM
    health_data
WHERE
    Personid >= 20;

-- total count of personid in distinct occupation -- 
SELECT DISTINCT
    (Occupation), COUNT(Personid)
FROM
    health_data
GROUP BY Occupation;

-- bad quality of sleep between the age 30-40 --
SELECT 
    Age, Personid, `Quality of Sleep`
FROM
    health_data
WHERE
    Age BETWEEN '30' AND '41'
        AND `Quality of Sleep` <= 7
ORDER BY Age ASC;  

-- changing column name--
alter table health_data rename column Personid to person_id;
