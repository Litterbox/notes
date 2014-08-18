## Relations

Always remember
- belongs_to has FK
- define both sides of the relationship
- put your FKs in migration files!

## Relationship types

#### One to one
Classroom has 1 teacher
Teacher is assigned 1 classroom
Room 107 <=> Martha Cook

FK goes in the teacher table

With Rails
Classroom has_one :teacher
Teacher belongs_to :classroom

#### One to many
1 Teacher has many courses
Course belogs to teacher
FK goes in course
Martha Cook -> Algebra, Geometry, Physics

Teacher has_many :courses
Course belongs_to :teacher

Methods attached (include all array methods too)
Course.teacher
Teacher.courses (returns an array)

#### Many to many - simple

A course has many students and belongs to many students
A student has many courses and belongs to many courses

Two FKs go in a join table

4 students 
4 courses

we cant have 4 diff FKs on each course
so we need a join table

Course has_and_belongs_to_many :students
Student has_and_belongs_to_many :courses

Join table should not have a FK! so you pass in hash of :id => false in the create table method (before the do)
We get the same methods as the 1-M relationships

First thing you do is create a migration

##### Rails convention 
- first_table + _ + second_table
- both table names are plural and in alphabetical
- ex: collaborators_projects

#### Many to many - rich joins

If you want to add more than just IDs, use rich join! This table needs a PK!

Example:

- Course has_many :course_enrollments
- CourseEnrollment belongs_to :course, belongs_to :student
- Students has_many :course_enrollments

In the join table use

t.references MODEL1
t.references MODEL2

then add

add_index :TABLE_NAME, ["MODEL1_ID", "MODEL2_ID"]

using has_many:through allows reaching across a rich join and treats rich join like a has_and_belongs_to_many join

Example:

- Course has_many :students, :through => :course_enrollments
- CourseEnrollment belongs_to :course, belongs_to :student
- Students has_many :courses, :through => :course_enrollments

#### Polymorphic associations

Treehouse
See old notes

https://github.com/wdi-sf-march-2014/notes/blob/master/IntroRailsRelated/ModelAssociations/ModelAssociations.md

https://github.com/wdi-sf-jan-2014/notes/blob/master/polymorphic_association/polymorphic_association.md