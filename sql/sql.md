
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