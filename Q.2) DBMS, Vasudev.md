# DBMS-Assignment
DBMS Assignment to Mr. Vipin sir

 NAME- VASUDEV
 ROLL No.- 20191238
 COURSE- B.Sc. STATISTICS (H)


Q.2)
mysql> create database cs_student;

mysql> create table personal_informartion(
    -> Roll_no int(10) primary key,
    -> Name char(30) not null,
    -> DOB date not null,
    -> Address varchar(70) not null,
    -> Marks_in_12th int(2) not null,
    -> Phone_number Varchar(10) not null);

mysql> create table Paper_Details(
    -> Paper_Code int(4) primary key,
    -> NameofPaper char(30) unique);

mysql> create table Academic_Details(
    -> Roll_no int(10) primary key,
    -> Paper_code int(4) not null,
    -> Attendence int(3) not null,
    -> Marks int(3) not null,
    -> foreign key(roll_no) references personal_informartion(roll_no),
    -> foreign key(paper_code) references Paper_details(paper_code));

(a)
Primary key - Roll_no in table personal_informartion
                             Paper_code in table Paper_details
        Foreign key - Roll_no in table Academic_Details
                            Paper_code in table Academic_Details 

mysql> insert into personal_informartion values(1201,"Amit Kandpal",'2001-01-04',"Delhi",91,9102829875);
mysql> insert into personal_informartion values(1205,"Anuj Joshi",'2001-04-29',"Uttarakhand",89,9748483743);
mysql> insert into personal_informartion values(1209,"Bhawana Arora",'2000-03-19',"Delhi",94,9837643368);
mysql> insert into personal_informartion values(1214,"Ishita Pandey",'2001-09-21',"Uttar Pradesh",97,9637453672);
mysql> insert into personal_informartion values(1219,"Pooja Singh",'2001-11-09',"Delhi",92,9764563726);

mysql> insert into paper_details value(1,"Descriptive Statistics");
mysql> insert into paper_details value(2,"English Communication");
mysql> insert into paper_details value(3,"Algebra");
mysql> insert into paper_details value(4,"Introduction to Matrices");
mysql> insert into paper_details value(5,"Database management system");

mysql> insert into Academic_details values(1201,2,80,70);
mysql> insert into Academic_details values(1205,2,70,90);
mysql> insert into Academic_details values(1214,2,65,91);
mysql> insert into Academic_details values(1214,2,65,91);
mysql> insert into Academic_details values(1219,1,75,65);

(b)
mysql> select pd.paper_code, pd.nameofpaper, pi.name from paper_details as pd, personal_informartion as pi where paper_code=2 and pi.roll_no in(select roll_no from academic_details where paper_code=2 and attendence>75 and marks>60);

(c)
mysql> select name from personal_informartion as pi, academic_details as ad where pi.roll_no=ad.roll_no and ad.marks>60 and ad.paper_code=1;

(d)
mysql> select pi.name, ad.attendence, ad.marks from personal_informartion as pi, academic_details as ad where pi.roll_no=ad.roll_no;

(e)
mysql> select name from personal_informartion as pi, academic_details as ad where pi.roll_no=ad.roll_no and pi.roll_no=(select roll_no from academic_details where marks=(select max(marks) from academic_details));
