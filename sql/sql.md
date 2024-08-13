
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



