# Intro to Ruby Lab

For this lab, we'd like you to complete a few challenges to reenforce your knowledge of integers, strings, arrays and booleans as well as iterators.

### Challenge 1 - Temperature Converter

Create a simple temperature convertor.  It should function like the example below:

```
Type '1' to convert from Celsius to Fahrenheit OR type '2' to convert from Fahrenheit to Celsius
1
Enter Celsius Temperature:
24
24 degrees Celsius is equal to 75.2 degrees Fahrenheit
```

### Challenge 2 - Calculator

Create a simple calculator that first asks the user what method they would like to use (addition, subtraction, multiplication, division) and then asks the user for two numbers, returning the result of the method with the two numbers. Here is a sample prompt:

```
What calculation would you like to do? (add, sub, mult, div)
add
What is number 1?
3
What is number 2?
6
Your result is 9
```

### Challenge 3 - Reverse a string

Reverse a string in place.  In other words, do not create a new string or use other methods on the string such as reverse.  The goal of the problem is to use a loop and the string accessors to figure out which values to swap for other values.  Below is the output.

```
Enter a string:
reverse_me
em_esrever
```

### Challenge 4 - Bank Transactions

Create a prompt that asks the user if they would like to display their balance, withdraw or deposit. Write three methods to perform these calculations and output the result to the user. Here is a sample output:

```
Your current balance is
4000
What would you like to do? (deposit, withdraw, check_balance)
deposit
How much would you like to deposit?
1000
Your current balance is 5000
Are you done?
yes
Thank you!
```

### Challenge 5 - Guessing Game

Create a program that asks the user to guess a number between 1 and 100.  Once the user guesses a number, the program should say, higher, lower, or tell the user that he got the number correct.  The user should continue to make guesses until he guesses correctly.  Also, once the user guesses correctly, the program should print the number of guesses needed to arrive at the correct answer. Below is sample output:

```
Guess a number between 1 and 100
50
The number is lower than 50.  Guess again
25
The number is lower than 25.  Guess again
13
The number is higher than 13.  Guess again
20
The number is lower than 20.  Guess again
17
The number is higher than 17.  Guess again
18
The number is higher than 18.  Guess again
19
You got it in 7 tries
```




### Bonus Challenge - Class List

Create an array of students and allow the user to keep adding new students to the array. After each student is added, display the array to the user (use the inspect method to display the array). If the user deciders to not add an additional student, display the list of the students and the index that each student is at (check out .each_with_index)