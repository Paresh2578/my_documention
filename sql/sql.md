
# Sql Note 

`All information in SQL Notes available`
Create datbase
Drop DataBase
Cretae Table
Insert value in Table

## Data types in SQL

1. **CHAR**: string(0-255 byts), can store chaarcters of fiexed length
2. **VARCHAR**: string(0-65535 bytes), can store chaarcters of variable length
3. **INT**: 4 bytes, can store whole numbers from -2,147,483,648 to 2,147,483,647
4. **FLOAT**: 4 bytes, can store decimal numbers from 23 digit
5. **DATE**:  can store dates in the format YYYY-MM-DD
6. **YEAR**: 1 byte, can store years in the format YYYY
7. **SIGNED** : Both Value store positive or negative (-128 to 127)
8. **UNSIGNED** Only positive value are store (0 to 255)


### What is diffrence between CHAR and VARCHAR?
CHAR is fixed length and VARCHAR is variable length.
VARCHAR is more flexible than CHAR, but it can be slower in some cases.
VARCHAR is use bite that use to store data

for Example
```SQL
ch1 CHAR(5)
ch2 VARCHAR(5)
```
Store data in ch1 = "abc"
Store data in ch2 = "abc"

`in CHAR`
_____________________
|  a | b   | c   |  -  |  -  |
_____________________
CHAR is fixed length and VARCHAR is variable length.
Oqupaid store 5 character in CHAR and VARCHAR

`in VARCHAR`
_____________________
|  a | b   | c   |
_____________________
Ouqupaid store 3 character in VARCHAR



### PrimaryKey
How to Two or more column combination primary key

```sql
create table User(
    id int,
    name varchar(30),
    Primary key (id , name)
)
```


### top in MsSQL and Limit in MySQL
select top rows

```sql
select top 1 * from user
select * from user limit 1
```



### Group By
Gorup by basically use for get value in group like number of student in each deparment

```sql
select deparment , count(name) from college
group by deparmant
```
Only those parameter use that apply group by 

#### This is wrong sintax
```sql
select deparment, name, count(name) from college
group by deparmant
```

#### This is Write sintax
```sql
select deparment, name, count(name) from college
group by deparmant , name
```

#### Nots in Where and Having
Where use for apply condition in column
Having use for apply condition in Group


#### Union
Union use for two table data but not dupplication data get
```sql
select * from student
union
select * from teacher
```

#### Union All
Union use for two table data with dupplication
```sql
select * from student
union all
select * from teacher
```

#### update with using joining query
```sql
UPDATE 
    e
SET 
    e.Salary = e.Salary + (e.Salary * 0.1)
FROM 
    Employee AS e
INNER JOIN 
    Department AS d
ON 
    e.Department_Id = d.Department_Id
WHERE 
    d.Department_Name = 'CSE';      
```

#### delete with using joining query
```sql
delete e from Employee As e
inner join department as d
on e.Department_Id= d.Department_Id
where d.Department_Name = 'CSE' and e.salary >= 4500   
```

#### Full Join
Full join not sported in my SQL
But full join use like left join and right join combination

```sql
select s.name , t.name from student as s
left join teacher as t
on s.id = t.id

union

select s.name , t.name from student as s
right join teacher as t
on s.id = t.id
```


#### SQL sub Queries
write a query inside the other query that called SQL sub Queries

- Totel Three way to write a query in inside to other query
1. select
2. from
3. where


#### Find privus value in table Using LAG Metod
```sql
SELECT 
    SaleID,
    SaleDate,
    Amount,
    LAG(Amount, 1, 0) OVER (ORDER BY SaleDate) AS PreviousAmount
FROM 
    Sales;
```

last 0 is options if use 



#### One table value store in diffrent diffrent tables with condition
```sql
with
startWith as 
(select * from Activity where activity_type = 'start'),
endWith as
(select * from Activity where activity_type = 'end')
select startWith.machine_id , round(avg(endWith.timesTamp - startWith.timestamp) , 3) as processing_time from startWith 
join endWith 
on startWith.machine_id = endWith.machine_id
group by startWith.machine_id

```



### apply some condition in count 
## using case 
```sql
SELECT 
    S.user_id , 
    -- NOTE-1: 'COUNT()' doesn't consider/count NULL
    --          so used 'CASE' to return 1 when condition satisfy else return NULL
    -- NOTE-2: num/denom => integer unless either num or denom is float
    --          hence for num or denom, either CAST(xx AS FLOAT) or multiple with 1.0 (faster shortcut)
    ROUND( COUNT(CASE WHEN C.action = 'confirmed' THEN 1 ELSE NULL END)*1.0 /COUNT(S.user_id) ,2) AS confirmation_rate
-- LEFT JOIN to include all users as per output requirement
FROM Signups AS S LEFT JOIN Confirmations AS C 
ON S.user_id = C.user_id 
GROUP BY S.user_id 
```
## using iif
```sql
select query_name , ,count(iif(rating < 3 , 1 , null)) as poor_query_percentage  from Queries
```



### How to use between
```sql
select p.product_id , isnull(round((sum(p.price*u.units)/(sum(u.units)*1.0)),2) , 0) as average_price from Prices as p
left join UnitsSold as u
on p.product_id = u.product_id and u.purchase_date between p.start_date and p.end_date
group by p.product_id
```



### Find any Table Count
```sql
select r.contest_id , round(count(r.user_id)/(select count(user_id) from Users)*100,2) as percentage from Users as u
inner join Register as r
on r.user_id = u.user_id
group by r.contest_id
order by percentage desc , r.contest_id
```

### Date format 
```
select FORMAT(trans_date, 'yyyy-MM') as month  from  Transactions
```

### Convert and LEFT 
```sql
SELECT LEFT(CONVERT(VARCHAR, GETDATE(), 23), 7) AS YearMonth

```

### Check Triangel
```sql
select x , y , z ,case when x+y>z and y+z>x and z+x>y then 'Yes' else 'No' end  as triangle from Triangle
```

### Get Prev and Next Value using Lag() for prev and Lead() for next
```sql
SELECT 
        LAG(id) OVER (ORDER BY id) AS prev_id,
        id,
        LEAD(id) OVER (ORDER BY id) AS next_id,
        LAG(num) OVER (ORDER BY id) AS prev_num,
        num,
        LEAD(num) OVER (ORDER BY id) AS next_num
FROM logs
```


### coalesce or isnull
-COALESCE or isnull is a SQL function that returns the first non-null value from a list of expressions. It is commonly used to handle null values by providing a default when a field or expression may be null.
-- isnull are only two argument are accept any one null then secoud value are pass
```sql
SELECT COALESCE(NULL, NULL, 'Hello', 'World');
SELECT isnull(NULL, 'Hello');

```


### create collum using union
```sql
select 'Low Salary' as category ,count(case when income < 20000 then 1 else null end)  as accounts_count from Accounts
union
select 'Average Salary' as category ,count(case when income between 20000 and 50000 then 1 else null end)  as accounts_count from Accounts
union
select 'High Salary' as category ,count(case when income > 50000 then 1 else null end)  as accounts_count from Accounts
```


### Exists and Not Exists 
- this is use for check any record are exists or not in output
```sql
SELECT e.employee_id
FROM Employees AS e
WHERE 
    e.salary <= 30000 
    AND Not EXISTS (
        SELECT 1 
        FROM Employees AS e1 
        WHERE e.manager_id = e1.employee_id
    );
```