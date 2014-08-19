## Console Lab

For this lab, we'd like you to strengthen your Rails console skills. This lab is going to be very familiar to the SQL lab, where we'll ask you to create a table and then write out the console commands you would use to execute these queries

### To Start

1. Create a model called Student, that has a first_name, last_name and age

### Tasks to create

1. Using the new/save syntax, create a student a first and last name and an age 
2. Save the student to the database
3. Using the find/set/save syntax update the student's first name to taco
4. Delete the student
5. Validate that every Student created is unique, 
6. Validate that every Student has a first and last name that is longer than 6 characters and can never be null
7. Combine these validations into one validate 
8. Using the create syntax create a student named John Doe who is 33 years old
9. Show if this new student entry is valid
10. Show the number of errors in the errors array for this student
11. In one command, Change John Doe's name to Jonathan Doesmith 
12. Clear the errors array
13. Save Jonathan Doesmithco. 
15. Find all of the Students
16. Find the student with an ID of 128 and if it does not exist, make sure it returns nil and not an error
17. Find the first student in the table
18. Find the last student in the table
19. Find the student with the last name of Doesmith
21. Find all of the students and limit the search to 5 students, starting with the 2nd student and finally, order the students in alphabetical order
20. Delete Jonathan Doesmith

### Bonus
1. Use the validates_format_of and regex to only validate names that have letters and start with a capital letter
2. Write a custom validation to ensure that no one named Delmer Reed, Tim Licata, Anil Bridgepal or Elie Schoppik is included in the students table


