# Analyzing Students' Mental Health using PostgreSQL
A SQL project aimed at analyzing and getting insight into the mental health condition of international students studying in Japan.

## Project Overview
Does going to university in a different country affect your mental health? A Japanese international university surveyed its students in 2018 and published a study the following year that was approved by several ethical and regulatory boards. The study found that international students have a higher risk of mental health difficulties than the general population, and that social connectedness (belonging to a social group) and acculturative stress (stress associated with joining a new culture) are predictive of depression.
We will explore the students data using PostgreSQL to find out if we would come to a similar conclusion for international students and see if the length of stay is a contributing factor.

## Techniques Used
Various techniques such as grouping, filtering and aggregation of data has been used utilizing CASE, WHERE, GROUP BY and other functions in order to obtain meaninful insights into the data. This project demonstrates a variety of SQL skills, including:
- Basic SQL syntax for data retrieval
- Sorting, filtering, and grouping to organize data effectively
- Subqueries for complex data extraction
- CASE statements for conditional logic and custom sorting
- Percentage Calculations to compare proportions within the dataset

## Dataset Description
The dataset includes the following key columns:
- `inter_dom`: Student type (International or Domestic)
- `japanese_cate`: Japanese language proficiency (Low, Average, High)
- `english_cate`: English language proficiency
- `academic`: Academic level (Undergraduate or Graduate)
- `age`: Student's current age
- `stay`: Length of stay in years
- `todep`: Depression score (PHQ-9 scale)
- `tosc`: Social connectedness score (SCS scale)
- `toas`: Acculturative stress score (ASISS scale)

## Sample Queries
### Relationship between mental health scores and language proficiency level
```sql
SELECT japanese_cate,
	COUNT(inter_dom) AS count_int,
	ROUND(AVG(todep), 2) AS average_phq,
	ROUND(AVG(tosc), 2) AS average_scs,
	ROUND(AVG(toas), 2) AS average_as
FROM students
WHERE inter_dom = 'Inter'
GROUP BY japanese_cate
ORDER BY 
	CASE 
		WHEN japanese_cate = 'Low' THEN 0
		WHEN japanese_cate = 'Average' THEN 1
		WHEN japanese_cate = 'High' THEN 2
		ELSE NULL
	END;
```
