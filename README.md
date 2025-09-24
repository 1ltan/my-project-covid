```bash
py -3.12 -m venv venv && \
venv\Scripts\activate && \
pip install --upgrade pip && \
pip install -r requirements.txt
```

```bash
docker-compose up -d
```

## Notes

SQL schemas
```sql
CREATE SCHEMA ods;
CREATE SCHEMA dm;
CREATE SCHEMA stg;
```

DDL `ods.fct_covid`:
```sql
CREATE TABLE ods.fct_covid
(
	date varchar,
	iso_code varchar,
	continent varchar,
	location varchar,
	total_cases varchar,
	new_cases varchar,
	total_deaths varchar,
	new_deaths varchar,
	new_vaccinations varchar,
	population varchar
)
```

DDL `dm.fct_count_day_covid`:

```sql
CREATE TABLE dm.fct_count_day_covid AS 
SELECT date AS date, count(*)
FROM ods.fct_covid
GROUP BY 1
```

DDL `dm.fct_avg_day_covid`:

```sql
CREATE TABLE dm.fct_avg_day_covid AS
SELECT date AS date, avg(new_cases::float)
FROM ods.fct_covid
GROUP BY 1 
```
