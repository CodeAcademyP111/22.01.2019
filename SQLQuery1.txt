create table Employee(
	Id int primary key identity,
	Name nvarchar(100) not null,
	Surname nvarchar(100)
)

create table ExEmployee(
	Id int primary key identity,
	Name nvarchar(100) not null,
	Surname nvarchar(100)
)

--Select * from Employee

--intersect,union, union all,except

--Select * from ExEmployee

--Alter table Employee
--add CityId int references City(Id)



--Select City.Cname 'City',Count(*) 'Count' from Employee
--Join City
--on Employee.CityId=City.Id

--Group by City.Cname
--having Count(*)>=2
----having City.Cname Like 'S%'

--Alter table Employee
--add Salary int

--Select Max(Salary) 'Max Salary' from Employee

--Select Min(Salary) 'Min Salary' from Employee

--Select AVG(Salary) 'Average Salary' from Employee

--Select SUM(Salary) 'Sum Salary' from Employee

--Select * from Employee
--where Salary>=(
--	Select AVG(Salary) from Employee
--)


--Select Name from Employee
--where Salary=(

--    Select Min(Salary) from Employee
--)


CREATE view StudentDetailInfo 
AS
SELECT ST.Name,ST.Surname, ST.Mark, GRD.Letter,GR.Gname 'GROUP',GRT.Tname 'GROUP TYPE',C.Cname 'CITY' FROM Student AS ST

INNER JOIN Groups AS GR
ON ST.GroupsId = GR.Id

INNER JOIN GroupType AS GRT
ON GR.GroupTypeId = GRT.Id

INNER JOIN City AS C
ON ST.CityId = C.Id

JOIN Grade AS GRD
ON ST.Mark BETWEEN GRD.MinGrade AND GRD.MaxGrade

Select * from StudentDetailInfo

Select * from Student
where Student.Mark>=80

Select * from Student
where Student.Mark>=90

Select * from Student
where Student.Mark>=70

exec usp_GetStudentSendingMark 80

create procedure usp_GetStudentSendingMark @Mark int
as
Select * from Student
where Student.Mark>=@Mark

create procedure usp_GetStudentSendingMark2 @Mark int,@Name nvarchar(100)
as
Select * from Student
where Student.Mark>=@Mark AND Student.Name=@Name

create procedure usp_GetStudentSendingMark3 @Mark int,@CityId int
as
Select * from Student
where Student.Mark>=@Mark AND Student.CityId=@CityId


Select * from Student
where Student.Mark>=80 AND Student.Name='Cavid'

exec usp_GetStudentSendingMark2 80,'Cavid';

exec usp_GetStudentSendingMark3 80,5



create procedure usp_GetAvgMark @Mark int,@AVG int OUTPUT
AS
Select @AVG=AVG(Mark) from Student
where Student.Mark>=@Mark

declare @AvgMark int
exec usp_GetAvgMark 70,@AVG=@AvgMark OUTPUT

select @AvgMark 'Average mark'

