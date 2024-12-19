# Functions
SQL Commands

## QN: Consider the Country table and Persons table that you created earlier and perform the following:
 1. Add a new column called DOB in Persons table with data type as Date.
 2. Write a user-defined function to calculate age using DOB. 
3. Write a select query to fetch the Age of all persons using the function that has been created.
 4. Find the length of each country name in the Country table.
 5. Extract the first three characters of each country's name in the Country table.
 6. Convert all country names to uppercase and lowercase in the Country table.




    Create database Country_And_Polulation;
use  Country_And_Polulation;
--  Create a table named Country with fields: Id, Country_name, Population_Area 

create table Country ( ID int primary Key, Country_name varchar(20) not null, Population int ,Area int );
-- Create another table named Persons with fields: Id Fname Lname Population Rating Country_Id Country_name

Create Table Persons ( ID int , F_name varchar (20) not null ,  Lname varchar (20) , Population int , Rating dec,  Country_Id int ,Country_name varchar (20), foreign key (Country_Id) references Country(ID));

insert into Country(ID, Country_name,Population,Area) values 

(1,'India',1420000000,3287000),
(2,'USA',331000000,9834000),
(3,'UAE',83200000,357022),
(4,'Oman',25600000,3287000),
(5,'Lanka',1428700000,987000),
(6,'China',1444216107,9597000),
(7,'Canada',38000000,9985000),
(8,'Japan',213000000,377975),
(9,'Brazil',67000000,8516000),
(10,'UK',67000000,243610);

insert into Persons ( ID , F_name ,  Lname, Population, Rating,  Country_Id ,Country_name) values
(1,'Sharon','Pindi',331000000, 4,2,'India'),
(2,'Karthika','Nelath',38765890, 5,3,'USA'),
(3,'Giri','Krishna',331000000, 5,5,'UAE'),
(15,'Surya','Kumar',35640000, 3,7,'Oman'),
(5,'Sam','John',331087000, 9,6,'Lanka'),
(6,'Hari','Murali',201000000, 4,2,'China'),
(7,'Prathap','Chandra',101000000, 3,7,'Canada'),
(13,'Manu','Manohar',671000000, 4,8,'Australia'),
(9,'Sree','Kala',381000000, 3,10,'Brazil'),
(12,'Krish','Lol',121000000, 5,1,'UK');

--  1. Add a new column called DOB in Persons table with data type as Date.
alter table Persons add DOB date;

-- 2. Write a user-defined function to calculate age using DOB.

delimiter //
create function Find_The_Age (DOB Date)
returns int
deterministic
begin
Declare Age int;
 Set Age = Floor(datediff(curdate(), DOB) / 365);
 return Age ;
end //
delimiter ;

-- 3. Write a select query to fetch the Age of all persons using the function that has been created.

alter table Persons;
 update persons  set DOB = '1990-10-12'
 where ID=1;

update persons  set DOB = '1992-08-10'
 where ID=2;
 update persons  set DOB = '1991-03-08'
 where ID=3;
 update persons  set DOB = '1989-01-04'
 where ID=12;
 update persons  set DOB = '1994-09-06'
 where ID=15;
 update persons  set DOB = '1999-12-11'
 where ID=6;

select ID,F_name, Find_The_Age(DOB) as Age from Persons;

-- 4. Find the length of each country name in the Country table.

Delimiter //
create function Length_of_country (Country_name Varchar (50))
returns int
deterministic
begin
return length(Country_name);
end//
Delimiter ;

select Country_name , Length_of_country(Country_name) from Country;

-- 5. Extract the first three characters of each country's name in the Country table.

select country_name , substr(country_name,1,3) as first_three from Country;

-- 6. Convert all country names to uppercase and lowercase in the Country table.
select country_name , upper(country_name) as first_three from Country;

