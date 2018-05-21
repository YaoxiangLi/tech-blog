---
title: Introduction to JavaScript
categories: JavaScript
abbrlink: 50727
date: 2016-01-21 10:03:20
tags:
  - JavaScript
---

## Hello world

console.log is used to display content to the JavaScript console. Run the following code in the console:

```javascript
console.log("Hello, world!");
```

Let’s use console.log to do something a little more interesting. Here’s a block of JavaScript code that loops through the numbers 0 through 9 and prints them out to the console:

```javascript
for (var i = 0; i < 10; i++) {
  console.log(i);
}
```

## Data types

### Numbers

7

### Arithmetic operations

3 + 2.1

### Comparing numbers

< > <= >= == !=

### Comments

```javascript
// this is a single-line comment

/*
this is
a multi-line
comment
*/
```

### Programming Quiz

Write an expression that uses at least 3 different arithmetic operators.
The expression should equal 42.
Hint: +, -, *, /, and % are possible arithmetic operators

```javascript
/*
 * Programming Quiz: First Expression
 *
 * Write an expression that uses at least three, different, arithmetic operators
 * to log the number 42 to the console.
 */

// this expression equals 4, change it to equal 42
console.log(8 - 5 + 3 - 1);
```

### Strings

```javascript
"hello"
'world'
```

It is correct to either use double " or single ' quotes with strings, as long as you're consistent.

### String concatenation

```javascript
"Hello," + " New York City"
```

1. What's the result with "hello" + "world"?

2. What do you think will happen when you type "Hello + 5*10" into the JavaScript console?

3. What do you think will happen when you type "Hello" + 5*10 into the console?

### Variables

Variable is a place to storage data and use it later:

```javascript
var greeting = "Hello";
```

### Naming conventions

When you create a variable, you write the name of the variable using camelCase (the first word is lowercase, and all following words are uppercase). Also try to use a variable name that accurately, but succinctly describes what the data is about.

```javascript
var totalAfterTax = 53.03; // uses camelCase if the variable name is multiple words
var tip = 8; // uses lowercase if the variable name is one word
```

### Programming quiz

To convert Celsius to Fahrenheit, you can use the following formula:
F=C×1.8+32

```javascript
/*
 * Programming Quiz: Converting Tempatures
 *
 * Use the Celsius-to-Fahrenheit formula to set the fahrenheit varible:
 *
 *     F = C x 1.8 + 32
 *
 * Log the fahrenheit variable to the console.
 *
 */

var celsius = 12;
var fahrenheit = celsius * 1.8 + 32 /* convert celsius to fahrenheit here */

console.log(fahrenheit)
```

### String index

```javascript
"Steve Jobs"[0];

var name = "Steve Jobs";
name[0]

var quote = "Stay hungery. Stay foolish.";
console.log(quote[6]);
```

### Escaping Strings

```javascript
// Wrong
"The man whispered, "please speak to me.""

// Right
"The man whispered, \"please speak to me.\""
```

### Comparing strings

```javascript
"Yes" == "yes"
'Y' != 'y'
```

### Programming quiz

Create a string with the name of your favorite food. The first letter of the string should be capitalized.

```javascript
/*
 * Programming Quiz: Favorite Food
 */

console.log("Peking Roast Duck");
```

Fix the right side expression so it evaluates to true.

```javascript
"ALL Strings are CrEaTeD equal" == "All STRINGS are CrEaTED Equal"
```

```javascript
/*
 * Programming Quiz: String Equality for All
 */

// fix the right side of the expression
var answer = "ALL Strings are CrEaTeD equal" == "ALL Strings are CrEaTeD equal";
console.log(answer);
```

Build a single string that resembles the following joke.

```
Why couldn't the shoes go out and play?
They were all "tied" up!
```

```javascript
/*
 * Programming Quiz: All Tied Up
 */

var joke = "Why couldn't the shoes go out and play?\nThey were all \"tied\" up!";
console.log(joke);
```

Build a string using concatenation by combining the lines from this famous haiku poem by Yosa Buson.

```
Blowing from the west
Fallen leaves gather
In the east.
```

```javascript
/*
 * Programming Quiz: Yosa Buson
 */

var haiku = "Blowing from the west\n" + "Fallen leaves gather\n" + "In the east.";/* concatenate the strings here */
console.log(haiku);
```

### Null, Undefined, and NaN

Recap of number, string and boolean

```javascript
var myNumber = 7; // this is a number
var myString = "Bach" // this is a string
var myBoolean = false // this is a boolean
```

null refers to the "value of nothing", while undefined refers to the "absence of value".
NaN stands for "Not-A-Number" and it's often returned indicating an error with number operations. For instance, if you wrote some code that performed a math calculation, and the calculation failed to produce a valid number, NaN might be returned.

```javascript
// calculating the square root of a negative number will return NaN
Math.sqrt(-10)

// trying to divide a string by 5 will return NaN
"hello"/5
```

What will be printed out?

```javascript
var signedIn;
console.log(signedIn);
```

### Equality

So far, you’ve seen how you can use == and != to compare numbers and strings for equality. However, if you use == and != in situations where the data you’re comparing is mixed, it can lead to some interesting results. For example,

```javascript
"1" == 1
Returns: true
```
and
```javascript
0 == false
Returns: true
```
both evaluate to true. Why is that?

JavaScript is known as a loosely typed language.

Basically, this means that when you’re writing JavaScript code, you do not need to specify data types. Instead, when your code is interpreted by the JavaScript engine it will automatically be converted into the "appropriate" data type. This is called implicit type coercion and you’ve already seen examples like this before when you tried to concatenate strings with numbers.
```
"julia" + 1
Returns: "julia1"
```
In this example, JavaScript takes the string "julia" and adds the number 1 to it resulting in the string "julia1". In other programming languages, this code probably would have returned an error, but in JavaScript the number 1 is converted into the string "1" and then is concatenated to the string "julia".

It’s behavior like this which makes JavaScript unique from other programming languages, but it can lead to some quirky behavior when doing operations and comparisons on mixed data types.

Example of strongly typed programming language code
```
int count = 1;
string name = "Julia";
double num = 1.2932;
float price = 2.99;
```
Equivalent code in JavaScript
```javascript
// equivalent code in JavaScript
var count = 1; 
var name = "Julia";
var num = 1.2932;
var price = 2.99;
```

In the example below, JavaScript takes the string "1", converts it to true, and compares it to the boolean true.
```
"1" == true
Returns: true
```
When you use the == or != operators, JavaScript first converts each value to the same type (if they’re not already the same type); this is why it's called "type coercion"! This is often not the behavior you want, and **it’s actually considered bad practice to use the == and != operators when comparing values for equality.**

### Strict equality

Instead, in JavaScript it’s better to use strict equality to see if numbers, strings, or booleans, etc. are identical in type and value without doing the type conversion first. To perform a strict comparison, simply add an additional equals sign = to the end of the == and != operators.

```javascript
"1" === 1
Returns: false
```

This returns false because the string "1" is not the same type and value as the number 1.

```javascript
0 === false
Returns: false
```

This returns false because the number 0 is not the same type and value as the boolean false.

### Programming quiz

Define two variables called thingOne and thingTwo and assign them values. Print the values of both variables in one console.log statement using concatenation. For example,

```javascript
red blue
```

```javascript
/*
 * Programming Quiz: Semicolons! (2-8)
 */

// your code goes here
var thingOne = "red";
var thingTwo = "blue";
console.log(thingOne + " " + thingTwo);
```

Create a variable called fullName and assign it your full name as a string.

```javascript
/*
 * Programming Quiz: What's my Name? (2-9)
 */

// your code goes here
var fullName = "Harry Potter";
```

Create a variable called bill and assign it the result of 10.25 + 3.99 + 7.15 (don't perform the calculation yourself, let JavaScript do it!). Next, create a variable called tip and assign it the result of multiplying bill by a 15% tip rate. Finally, add the bill and tip together and store it into a variable called total.

Print the total to the JavaScript console.

```javascript
/*
 * Programming Quiz: Out to Dinner (2-10)
 */

// your code goes here
var bill = 10.25 + 3.99 + 7.15;
var tip = bill * 0.15;
var total = bill + tip;
console.log(total);
```

Mad Libs is a word game where players have fun substituting words for blanks in a story. For this exercise, use the adjective variables below to fill in the blanks and complete the following message.

```javascript
"The Intro to JavaScript course is __________. James and Julia are so __________. I cannot wait to work through the rest of this __________ content!"
var adjective1 = "amazing";
var adjective2 = "fun";
var adjective3 = "entertaining";
```

Assign the resulting string to a variable called madLib.

```javascript
/*
 * Programming Quiz: MadLibs
 * 
 * 1. Declare a madLib variable
 * 2. Use the adjective1, adjective2, and adjective3 variables to set the madLib variable to the message:
 * 
 * 'The Intro to JavaScript course is amazing. James and Julia are so fun. I cannot wait to work through the rest of this entertaining content!'
 */

var adjective1 = 'amazing';
var adjective2 = 'fun';
var adjective3 = 'entertaining';

// your code goes here

var madLib = 'The Intro to JavaScript course is ' + adjective1 + '. James and Julia are so ' + adjective2 + '. I cannot wait to work through the rest of this ' + adjective3 + ' content!';
```

Here are two awesome messages:

```javascript
"Hi, my name is Julia. I love cats. In my spare time, I like to play video games."
"Hi, my name is James. I love baseball. In my spare time, I like to read."
```

Declare and assign values to three variables for each part of the sentence that changes (firstName, interest, and hobby).

Use your variables and string concatenation to create your own awesome message and store it in an awesomeMessage variable. Finally, print your awesome message to the JavaScript console.

```javascript
/*
 * Programming Quiz: One Awesome Message (2-12)
 *
 * 1. Create the variables:
 *     - firstName
 *     - interest
 *     - hobby
 * 2. Create a variable named awesomeMessage and, using string concatenation 
      and the variables above, create an awesome message.
 * 3. Print the awesomeMessage variable to the console.
 */
 
/*
 * Notes:
 * - Using the above as an example, firstName would have been assigned to
 *   "Julia", interest to "cats", and hobby to "play video games".
 * - Be sure to include spaces and periods where necessary!
 */

// Add your code here
var firstName = "Julia";
var interest = "cats";
var hobby = "play video games";
var awesomeMessage = "Hi, my name is " + firstName + ". I love " + interest + ". In my spare time, I like to " + hobby + ".";
console.log(awesomeMessage);
```

### If...Else Statements

If...else statements allow you to execute certain pieces of code based on a condition, or set of conditions, being met.

```javascript
if (/* this expression is true */) {
  // run this code
} else {
  // run this code
}
```

This is extremely helpful because it allows you to choose which piece of code you want to run based on the result of an expression. For example,

```javascript
var a = 1;
var b = 2;

if (a > b) {
  console.log("a is greater than b");
} else {
  console.log("a is less than or equal to b");
}
```
Prints: "a is less than or equal to b"

A couple of important things to notice about if...else statements.

The value inside the if statement is always converted to true or false. Depending on the value, the code inside the if statement is run or the code inside the else statement is run, but not both. The code inside the if and else statements are surrounded by curly braces {...} to separate the conditions and indicate which code should be run.

### Else If Statements

In some situations, two conditionals aren’t enough. Consider the following situation.

```javascript
var weather = "sunny";

if (weather === "snow") {
  console.log("Bring a coat.");
} else if (weather === "rain") {
  console.log("Bring a rain jacket.");
} else {
  console.log("Wear what you have on.");
}
```

### Logical AND and OR

&& (AND)

A	|B	|A && B
----|---|-------
true	|true	|true
true	|false	|false
false	|true	|false
false	|false	|false

|| (OR)

A	|B	|A || B
----|---|-------
true	|true	|true
true	|false	|true
false	|true	|true
false	|false	|false

### Programming quiz

Write an if...else statement that:

prints "even" if the number is an even number
prints "odd" if the number is an odd number
Hint: Use the % (modulo) operator to determine if a number is even or odd. The modulo operater takes two numbers and returns the remainder when the first number is divided by the second one:
```javascript
console.log(12 % 3);
console.log(10 % 4);
```

```javascript
/*
 * Programming Quiz: Even or Odd (3-2)
 *
 * Write an if...else statement that prints `even` if the 
 * number is even and prints `odd` if the number is odd.
 *
 * Note - make sure to print only the string "even" or the string "odd"
 */

// change the value of `number` to test your if...else statement
var number = 2;

if (number % 2 === 0) {
    console.log("even");
} else {
    console.log("odd");
}
```

Musical groups have special names based on the number of people in the group.

For example, a "quartet" is a musical group with four musicians. Barbershop quartets were a popular type of quartet in the early 1900s and featured four singers made up of a lead, tenor, baritone, and bass.

Write a series of conditional statements that:

- prints "not a group" if musicians is less than or equal to 0
- prints "solo" if musicians is equal to 1
- prints "duet" if musicians is equal to 2
- prints "trio" if musicians is equal to 3
- prints "quartet" if musicians is equal to 4
- prints "this is a large group" if musicians is greater than 4

TIP: Make sure to test your code with different values. For example,

- If musicians equals 3, then trio should be printed to the console.
- If musicians equals 20, then this is a large group should be printed to the console.
- If musicians equals -1, then not a group should be printed to the console.

```javascript
/*
 * Programming Quiz: Musical Groups (3-3)
 */

// change the value of `musicians` to test your conditional statements
var musicians = 1;

// your code goes here
if (musicians <= 0){
    console.log("not a group");
} else if(musicians === 1){
    console.log("solo");
} else if(musicians === 2){
    console.log("duet");
} else if(musicians === 3){
    console.log("trio");
} else if(musicians === 4){
    console.log("quartet");
} else if(musicians > 4){
    console.log("this is a large group");
}
```

For this quiz, you're going to help solve a fictitious murder mystery that happened here at Udacity! A murder mystery is a game typically played at parties wherein one of the partygoers is secretly, and unknowingly, playing a murderer, and the other attendees must determine who among them is the criminal. It's a classic case of whodunnit.

Since this might be your first time playing a murder mystery, we've simplified things quite a bit to make it easier. Here's what we know! In this murder mystery there are:

four rooms: the ballroom, gallery, billiards room, and dining room,
four weapons: poison, a trophy, a pool stick, and a knife,
and four suspects: Mr. Parkes, Ms. Van Cleve, Mrs. Sparr, and Mr. Kalehoff.

We also know that each weapon corresponds to a particular room, so...

the poison belongs to the ballroom,
the trophy belongs to the gallery,
the pool stick belongs to the billiards room,
and the knife belongs to the dining room.
And we know that each suspect was located in a specific room at the time of the murder.

Mr. Parkes was located in the dining room.
Ms. Van Cleve was located in the gallery.
Mrs. Sparr was located in the billiards room.
Mr. Kalehoff was located in the ballroom.
To help solve this mystery, write a combination of conditional statements that:

sets the value of weapon based on the room and
sets the value of solved to true if the value of room matches the suspect's room
Afterwards, print the following to the console if the mystery was solved:

__________ did it in the __________ with the __________!
Fill in the blanks with the name of the suspect, the room, and the weapon. For example,

Mr. Parkes did it in the dining room with the knife!
TIP: Make sure to test your code with different values. For example,

If room equals gallery and suspect equals Ms. Van Cleve, then Ms. Van Cleve did it in the gallery with the trophy! should be printed to the console.


```javascript
/*
 * Programming Quiz: Murder Mystery (3-4)
 */

// change the value of `room` and `suspect` to test your code
var room = "dining room";
var suspect = "Mr. Parkes";

var weapon = "";
var solved = false;

if (room === "ballroom" && suspect === "Mr. Kalehoff") {
    weapon = "poison";
    solved = true;
} else if (room === "gallery" && suspect === "Ms. Van Cleve") {
    weapon = "trophy";
    solved = true;
} else if (room === "billiards room" && suspect === "Mrs. Sparr") {
    weapon = "pool stick";
    solved = true;
} else if (room === "dining room" && suspect === "Mr. Parkes"){
    weapon = "knife";
    solved = true;
}

if (solved) {
	console.log(suspect +" did it in the "+ room + " with the "+ weapon +"!");
}
```


Using the flowchart below, write the code to represent checking your balance at the ATM. The yellow diamonds represent conditional statements and the blue rectangles with rounded corners represent what should be printed to the console.

![](https://d17h27t6h515a5.cloudfront.net/topher/2016/November/582cc7b8_atm-check-balance-cropped/atm-check-balance-cropped.jpeg)


Use the following variables in your solution:

balance - the account balance
isActive - if account is active
checkBalance - if you want to check balance
Hint: The variable balance could be a value less than, greater than, or equal to 0. The variables isActive and checkBalance are booleans that can be set to true or false.

TIP: To print out the account balance with decimal points (i.e. 325.00), use the .toFixed() method and pass it the number of decimal points you want to use. For example, balance.toFixed(2) returns 325.00.

TIP: Make sure to test your code with different values. For example,

If checkBalance equals true and isActive equals false, then Your account is no longer active. should be printed to the console.


```javascript
/*
 * Programming Quiz - Checking Your Balance
 */

// change the values of `balance`, `checkBalance`, and `isActive` to test your code
var balance = 325.00;
var checkBalance = true;
var isActive = false;

// your code goes here
if (checkBalance === true){
    if (isActive === true){
        if (balance > 0){
            console.log("Your balance is $" + balance + ".")
        }
        else if (balance === 0){
            console.log("Your account is empty.")
        } else {
            console.log("Your balance is negative. Please contact bank.")
        }
    } else {
        console.log("Your account is no longer active.")
    }
} else {
    console.log("Thank you. Have a nice day!")
}
```


Directions:
Ice cream is one of the most versatile desserts on the planet because it can be done up so many different ways. Using logical operators, write a series of complex logical expressions that prints only if the following conditions are true:

if flavor is set to vanilla or chocolate and
if vessel is set to cone or bowl and
if toppings is set to sprinkles or peanuts
If the above conditions are true, then print out:

I'd like two scoops of __________ ice cream in a __________ with __________.
Fill in the blanks with the flavor of the ice cream, vessel, and toppings. For example,

I'd like two scoops of vanilla ice cream in a cone with peanuts.
TIP: Make sure to test your code with different values. For example,

If flavor equals "chocolate", vessel equals "cone" and toppings equals "sprinkles", then "I'd like two scoops of chocolate ice cream in a cone with sprinkles." should be printed to the console.


```javascript
/*
 * Programming Quiz: Ice Cream
 *
 * Write a single if statement that logs out the message:
 * 
 * "I'd like two scoops of __________ ice cream in a __________ with __________."
 * 
 * ...only if:
 *   - flavor is "vanilla" or "chocolate"
 *   - vessel is "cone" or "bowl"
 *   - toppings is "sprinkles" or "peanuts"
 *
 * We're only testing the if statement and your boolean operators. 
 * It's okay if the output string doesn't match exactly.
 */

// change the values of `flavor`, `vessel`, and `toppings` to test your code
var flavor = "strawberry";
var vessel = "cone";
var toppings = "cookies";

// Add your code here
if ((flavor === "vanilla" || flavor === "chocolate") && (vessel === "cone" || vessel === "bowl") && (toppings === "sprinkles" || toppings === "peanuts")) {
    console.log("I\'d like two scoops of "+ flavor +" ice cream in a "+ vessel +" with "+ toppings +".");
}
```

What do I Wear?

If you're like me, finding the right size t-shirt can sometimes be a challenge. What size am I? What's the difference between S (small), M (medium), and L (large)? I usually wear L, but what if I need an XL (extra large)?

Thankfully, our friends at Teespring have got us covered because they've created a sizing chart to make things a lot easier.

![]
(https://d17h27t6h515a5.cloudfront.net/topher/2016/December/5852beb9_tshirt-guide/tshirt-guide.png)

Use the sizing chart above, create a series of logical expressions that prints the size of a t-shirt based on the measurements of shirtWidth, shirtLength, and shirtSleeve. Valid sizes include S, M, L, XL, 2XL, and 3XL.

For example, if...
```javascript
var shirtWidth = 23; // size L (large)
var shirtLength = 30; // size L (large)
var shirtSleeve = 8.71; // size L (large)
```
Then print L to the console.

Hint: You will need to compare a range of values when checking for shirtWidth, shirtLength, and shirtSleeve. For example, if the shirt's width is at least 20", but no more than 22", then the t-shirt should be medium (M) — as long as the other values for the shirt's length and sleeve measurements match up.

If shirtWidth, shirtLength, and shirtSleeve don't fit within the range of acceptable values for a specific size, then print N/A to the console. For example, if...
```javascript
var shirtWidth = 18; // size S (small)
var shirtLength = 29; // size M (medium)
var shirtSleeve = 8.47; // size M (medium)
```
Then print N/A to the console because the measurements don't all match up with one particular size.

TIP: Make sure to test your code with different values. For example,

If shirtWidth equals 19, shirtLength equals 28 and shirtSleeve equals 8.21, then S should be printed to the console.
If shirtWidth equals 26, shirtLength equals 33 and shirtSleeve equals 9.63, then 2XL should be printed to the console.
If shirtWidth equals 18, shirtLength equals 29 and shirtSleeve equals 8.47, then N/A should be printed to the console.

```javascript
/*
 * Programming Quiz: What do I Wear? (3-7)
 */

// change the values of `shirtWidth`, `shirtLength`, and `shirtSleeve` to test your code
var shirtWidth = 23;
var shirtLength = 30;
var shirtSleeve = 8.71;

// your code goes here
if (((shirtWidth >= 18 && shirtWidth < 20) && (shirtLength >= 28 && shirtLength < 29) && (shirtSleeve >= 8.13 && shirtSleeve < 8.38))) {
  console.log("S"); 
}else if (((shirtWidth >= 20 && shirtWidth < 22) && (shirtLength >= 29 && shirtLength< 30) && (shirtSleeve >= 8.38 && shirtSleeve < 8.63))){
  console.log("M");
}else if (((shirtWidth >= 22 && shirtWidth < 24) && (shirtLength >= 30 && shirtLength< 31) && (shirtSleeve >= 8.63 && shirtSleeve < 8.88))){
  console.log("L");
}else if (((shirtWidth >= 24 && shirtWidth < 26) && (shirtLength >= 31 && shirtLength< 33) && (shirtSleeve >= 8.88 && shirtSleeve < 9.63))){
  console.log("XL");
}else if (((shirtWidth >= 26 && shirtWidth < 28) && (shirtLength >= 33 && shirtLength< 34) && (shirtSleeve >= 9.63 && shirtSleeve < 10.13))){
  console.log("2XL");
}else if (((shirtWidth >= 28) && (shirtLength >= 34 ) && (shirtSleeve >= 10.13 ))){
  console.log("3XL");
}else {
  console.log("N/A");
}
```


### Truthy and Falsy

Every value in JavaScript has an inherent boolean value. When that value is evaluated in the context of a boolean expression, the value will be transformed into that inherent boolean value.

Falsy values

A value is **falsy** if it converts to false when evaluated in a boolean context. For example, an empty String "" is falsy because, "" evaluates to false. You already know if...else statements, so let's use them to test the truthy-ness of "".

```javascript
if ("") {
    console.log("the value is truthy");
} else {
    console.log("the value is falsy");
}
```
Returns: "the value is falsy"

Here’s the list of all of the falsy values:
- the Boolean value false
- the null type
- the undefined type
- the number 0
- the empty string ""
- the odd value NaN (stands for "not a number", check out the NaN MDN article)
That's right, there are **only** six falsy values in all of JavaScript!

Truthy values

A value is **truthy** if it converts to true when evaluated in a boolean context. For example, the number 1 is truthy because, 1 evaluates to true. Let's use an if...else statement again to test this out:

```javascript
if (1) {
    console.log("the value is truthy");
} else {
    console.log("the value is falsy");
}
```
Returns: "the value is truthy"

Here are some other examples of truthy values:
```javascript
true
42
"pizza"
"0"
"null"
"undefined"
{}
[]
```
Essentially, if it's not in the list of falsy values, then it's truthy!

### Ternary Operator

Sometimes, you might find yourself with the following type of conditional.

```javascript
var isGoing = true;
var color;

if (isGoing) {
  color = "green";
} else {
  color = "red";
}

console.log(color);
```

In this example, the variable color is being assigned to either "green" or "red" based on the value of isGoing. This code works, but it’s a rather lengthy way for assigning a value to a variable. Thankfully, in JavaScript there’s another way.


The **ternary operator** provides you with a shortcut alternative for writing lengthy if...else statements.

```
conditional ? (if condition is true) : (if condition is false)
```

To use the ternary operator, first provide a conditional statement on the left-side of the ?. Then, between the ? and : write the code that would run if the condition is true and on the right-hand side of the : write the code that would run if the condition is false. For example, you can rewrite the example code above as:

```javascript
var isGoing = true;
var color = isGoing ? "green" : "red";
console.log(color);
```

This code not only replaces the conditional, but it also handles the variable assignment for color.

If you breakdown the code, the condition isGoing is placed on the left side of the ?. Then, the first expression, after the ?, is what will be run if the condition is true and the second expression after the, :, is what will be run if the condition is false.

What will be printed to the console if the following code is run?

```javascript
var adult = true;
var preorder = true;

console.log("It costs $" + (adult ? "40.00" : "20.00") + " to attend the concert. Pick up your tickets at the " + (preorder ? "will call" : "the gate") + ".");
```

### Programming quiz
From the smallest of creatures to the largest of animals, inevitably every living, breathing thing must ingest other organisms to survive. This means that all animals will fall within one of the three consumer-based categories based on the types of food that they eat.

- Animals that eat only plants are called herbivores
- Animals that eat only other animals are called carnivores
- Animals that eat both plants and animals are called omnivores

Write a series of ternary statements that sets the variable category equal to:

- "herbivore" if an animal eats plants
- "carnivore" if an animal eats animals
- "omnivore" if an animal eats plants and animals
- undefined if an animal doesn't eat plants or animals
Use the eatsPlants and eatsAnimals variables to test your code.

TIP: Make sure to test your code with different values. For example,

If eatsPlants equals true and eatsAnimals equals false, then herbivore should be printed to the console.

```javascript
/*
 * Programming Quiz - Navigating the Food Chain
 *
 * Use a series of ternary operator to set the category to one of the following:
 *   - "herbivore" if an animal eats plants
 *   - "carnivore" if an animal eats animals
 *   - "omnivore" if an animal eats plants and animals
 *   - undefined if an animal doesn't eat plants or animals
 *
 * Notes
 *   - use the variables `eatsPlants` and `eatsAnimals` in your ternary expressions
 *   - `if` statements aren't allowed ;-)
 */

// change the values of `eatsPlants` and `eatsAnimals` to test your code
var eatsPlants = false;
var eatsAnimals = true;

var category = eatsPlants && eatsAnimals ? "omnivore": eatsPlants ? "herbivore" : eatsAnimals ? "carnivore" : undefined;  /* your code goes here */

console.log(category);
```

### Switch Statement

If you find yourself repeating else if statements in your code, where each condition is based on the same value, then it might be time to use a switch statement.

```javascript
if (option === 1) {
  console.log("You selected option 1.");
} else if (option === 2) {
  console.log("You selected option 2.");
} else if (option === 3) {
  console.log("You selected option 3.");
} else if (option === 4) {
  console.log("You selected option 4.");
} else if (option === 5) {
  console.log("You selected option 5.");
} else if (option === 6) {
  console.log("You selected option 6.");
}
```
A switch statement is an another way to chain multiple else if statements that are based on the same value without using conditional statements. Instead, you just switch which piece of code is executed based on a value.

```javascript
switch (option) {
  case 1:
    console.log("You selected option 1.");
  case 2:
    console.log("You selected option 2.");
  case 3:
    console.log("You selected option 3.");
  case 4:
    console.log("You selected option 4.");
  case 5:
    console.log("You selected option 5.");
  case 6:
    console.log("You selected option 6.");
}
```

Here, each else if statement (option === [value]) has been replaced with a case clause (case: [value]) and those clauses have been wrapped inside the switch statement.

When the switch statement first evaluates, it looks for the first case clause whose expression evaluates to the same value as the result of the expression passed to the switch statement. Then, it transfers control to that case clause, executing the associated statements.

So, if you set option equal to 3...

```javascript
var option = 3;

switch (option) {
  ...
}
```

```
Prints:
You selected option 3.
You selected option 4.
You selected option 5.
You selected option 6.
```

...then the switch statement prints out options 3, 4, 5, and 6.

But that’s not exactly like the original if...else code at the top? So what’s missing?

The break statement can be used to terminate a switch statement and transfer control to the code following the terminated statement. By adding a break to each case clause, you fix the issue of the switch statement falling-through to other case clauses.

```javascript
var option = 3;

switch (option) {
  case 1:
    console.log("You selected option 1.");
    break;
  case 2:
    console.log("You selected option 2.");
    break;
  case 3:
    console.log("You selected option 3.");
    break;
  case 4:
    console.log("You selected option 4.");
    break;
  case 5:
    console.log("You selected option 5.");
    break;
  case 6:
    console.log("You selected option 6.");
    break; // technically, not needed
}
```

What will be the result from the following switch statement?

```javascript
var month = 2;

switch(month) {
  case 1:
  case 3:
  case 5:
  case 7:
  case 8:
  case 10:
  case 12:
    days = 31;
    break;
  case 4:
  case 6:
  case 9:
  case 11:
    days = 30;
    break;
  case 2:
    days = 28;
}

console.log("There are " + days + " days in this month.");
```

### Programming quiz

In 2015, the U.S. Bureau of Labor Statistics conducted research to reveal how average salary is directly related to the number of years spent in school. In their findings, they found that people with:

- no high school diploma earned an average of $25,636/year,
- a high school diploma earned an average of $35,256/year,
- an Associate's degree earned an average of $41,496/year,
- a Bachelor's degree earned an average of $59,124/year,
- a Master's degree earned an average of $69,732/year,
- a Professional degree earned an average of $89,960/year,
- and a Doctoral degree earned an average of $84,396/year.

NOTE: Wondering what the average salary would be for a person with a Nanodegree from Udacity? That's a hard question to answer, but that doesn't mean we haven't tried to quantify the value of our Nanodegrees. Click here to read more about Nanodegrees from resident Udacity writer Chris Watkins.

Write a switch statement to set the average salary of a person based on their type of completed education.

Afterwards, print the following to the console.

```javascript
In 2015, a person with __________ earned an average of __________/year.
```

Fill in the blanks with the type of education and the expected average salary. Make sure to use correct grammar in your printed statement. For help, refer to the findings above.

```javascript
In 2015, a person with a Bachelor's degree earned an average of $59,124/year.
```

TIP: To print out the average salary with commas (i.e. 59,124), use the toLocaleString() method and pass it the locale "en-US". For example, salary.toLocaleString("en-US").

TIP: Make sure to test your code with different values. For example,

```javascript
If education equals "an Associate's degree", then In 2015, a person with an Associate's degree earned an average of $41,496/year. should be printed to the console.
```

```javascript
/*
 * Programming Quiz: Back to School (3-9)
 */

// change the value of `education` to test your code
var education = "no high school diploma";

// set the value of this based on a person's education
var salary;

// your code goes here
switch (education) {
  case "no high school diploma":
    salary ="$25,636";
    break;
  case "a high school diploma":
    salary ="$35,256";
    break;
  case"an Associate's degree" :
    salary ="$41,496";
    break;
  case "a Bachelor's degree":
    salary ="$59,124";
    break;
  case "a Master's degree": 
    salary ="$69,732";
    break;
  case "a Professional degree":
    salary ="$89,960";
    break;
  case "a Doctoral degree":
    salary="$84,396";
    break;
}
console.log("In 2015, a person with " + education +" earned an average of "+ salary+"/year.");
```

### While loops

"Fizzbuzz" is a famous interview question used in programming interviews. It goes something like this:

- Loop through the numbers 1 to 100
- If the number is divisible by 3, print "Fizz"
- If the number is divisible by 5, print "Buzz"
- If the number is divisible by both 3 and 5, print "FizzBuzz"
- If the number is not divisible by 3 or 5, print the number

```javascript
TIP: A number x is divisible by a number y if the answer to x / y has a remainder of 0. For example, 10 is divisible by 2 because 10 / 2 = 5 with no remainder. You can check if a number is divisible by another number by checking if x % y === 0.
```

We're going to have you program your own version of FizzBuzz called "JuliaJames" (yes, imaginative, right?) Keep in mind that in an interview, you would want to write efficient code with very little duplication. We don't want you to worry about that for this question. Just focus on practicing using loops.

Write a while loop that:

- Loop through the numbers 1 to 20
- If the number is divisible by 3, print "Julia"
- If the number is divisible by 5, print "James"
- If the number is divisible by 3 and 5, print "JuliaJames"
- If the number is not divisible by 3 or 5, print the number

```javascript
/*
 * Programming Quiz: JuliaJames
 */

var x = 1;

while (x <= 20) {
    // check divisibility
    if ((x % 3 === 0) && (x % 5 === 0)){
        console.log("JuliaJames");
    } else if (x % 3 === 0){
        console.log("Julia");
    } else if (x % 5 === 0){
        console.log("James");
    } else {
        console.log(x);
    }
    x += 1;
    // print Julia, James, or JuliaJames
    // increment x
}
```

Write a loop that prints out the following song. Starting at 99, and ending at 1 bottle.

```javascript
99 bottles of juice on the wall! 99 bottles of juice! Take one down, pass it around... 98 bottles of juice on the wall!
98 bottles of juice on the wall! 98 bottles of juice! Take one down, pass it around... 97 bottles of juice on the wall!
...
2 bottles of juice on the wall! 2 bottles of juice! Take one down, pass it around... 1 bottle of juice on the wall!
1 bottle of juice on the wall! 1 bottle of juice! Take one down, pass it around... 0 bottles of juice on the wall!
```

Some Notes:

- Note the pluralization of the word "bottle" when you go from 2 bottles to 1 bottle.
- Your text editor may try to autocorrect your ellipses ... to the ellipses character … Do not use the ellipses character for this quiz.

```javascript
/*
 * Programming Quiz: 99 Bottles of Juice (4-2)
 *
 * Use the following `while` loop to write out the song "99 bottles of juice".
 * Log the your lyrics to the console.
 *
 * Note
 *   - Each line of the lyrics needs to be logged to the same line.
 *   - The pluralization of the word "bottle" changes from "2 bottles" to "1 bottle" to "0 bottles".
 */

var num = 99;

while (num >= 1){
    if (num > 2){
    console.log(num +" bottles of juice on the wall! " + num + " bottles of juice! Take one down, pass it around... " + (num - 1) + " bottles of juice on the wall!");
    }else if(num === 2) {
        console.log(num +" bottles of juice on the wall! "+num +" bottles of juice! Take one down, pass it around... " + (num - 1) + " bottle of juice on the wall!");
    }else {
        console.log(num +" bottle of juice on the wall! "+num +" bottle of juice! Take one down, pass it around... " + (num - 1) + " bottles of juice on the wall!");
    }
    num --;
}
```

NASA's countdown to launch includes checkpoints where NASA engineers complete certain technical tasks. During the final minute, NASA has 6 tasks to complete:

- Orbiter transfers from ground to internal power (T-50 seconds)
- Ground launch sequencer is go for auto sequence start (T-31 seconds)
- Activate launch pad sound suppression system (T-16 seconds)
- Activate main engine hydrogen burnoff system (T-10 seconds)
- Main engine start (T-6 seconds)
- Solid rocket booster ignition and liftoff! (T-0 seconds)

NOTE: "T-50 seconds" read as "T-minus 50 seconds".

Write a while loop that counts down from 60 seconds and:

- If there's a task being completed, it prints out the task
- If there is no task being completed, it prints out the time as T-x seconds

Use the task and time descriptions described above.

Your output should look like the following:

```javascript
T-60 seconds
T-59 seconds
T-58 seconds
...
T-51 seconds
Orbiter transfers from ground to internal power
T-49 seconds
...
T-3 seconds
T-2 seconds
T-1 seconds
Solid rocket booster ignition and liftoff!
```

```javascript
/*
 * Programming Quiz: Countdown, Liftoff! (4-3)
 *
 * Using a while loop, print out the countdown output above.
 */

// your code goes here
var x = 60;

while (x >= 0){
  if (x === 50) {
    console.log("Orbiter transfers from ground to internal power");
  }else if (x === 31) {
    console.log("Ground launch sequencer is go for auto sequence start");
  }else if (x === 16) {
    console.log("Activate launch pad sound suppression system");
  }else if (x === 10) {
    console.log("Activate main engine hydrogen burnoff system");
  }else if (x === 6) {
    console.log ("Main engine start"); 
  }else if (x === 0) {
    console.log("Solid rocket booster ignition and liftoff!");
  }else {
    console.log("T-" + x + " seconds");
  }
  x--;
}
```

### For loops

The for loop explicitly forces you to define the start point, stop point, and each step of the loop. In fact, you'll get an Uncaught SyntaxError: Unexpected token ) if you leave out any of the three required pieces.

```javascript
for ( start; stop; step ) {
  // do this thing
}
```

Here's an example of a for loop that prints out the values from 0 to 5. Notice the semicolons separating the different statements of the for loop: var i = 0; i < 6; i = i + 1

```javascript
for (var i = 0; i < 6; i = i + 1) {
  console.log("Printing out i = " + i);
}
```

### Nested loops

```javascript
for (var x = 0; x < 5; x = x + 1) {
  for (var y = 0; y < 3; y = y + 1) {
    console.log(x + "," + y);
  }
}
```

What will this loop print out?

```javascript
for (var i = 0; i <= 6; i = i + 2) {
  console.log(i);
}
```

### Increment and decrement

Here is a summary of operators you've learned so far:

```javascript
x++ or ++x // same as x = x + 1 
x-- or --x // same as x = x - 1
x += 3 // same as x = x + 3
x -= 6 // same as x = x - 6
x *= 2 // same as x = x * 2
x /= 5 // same as x = x / 5
```

### Programming quiz

Rewrite the following while loop as a for loop:

```javascript
var x = 9;
while (x >= 1) {
  console.log("hello " + x);
  x = x - 1;
}
```

```javascript
/*
 * Programming Quiz: Changing the Loop (4-4)
 */

// rewrite the while loop as a for loop
for (var x = 9; x >= 1; x --){
    console.log("hello " + x);
}
```

Here is a for loop that's supposed to print the numbers 5 through 9. Fix the error!

```javascript
for (x < 10; x++) {
  console.log(x);
}
```

The for loop below has an error. Fix it!

```javascript
for (var k = 0 k < 200 k++) {
  console.log(k);
}
```

Write a for loop that prints out the factorial of the number 12:

Save your final answer in a variable called solution and print it to the console.

```javascript
/*
 * Programming Quiz: Factorials (4-7)
 */

// your code goes here
var solution = 1;

for (var x = 12; x >= 1; x--){
    solution *= x;
}

console.log(solution);
```

Theater seats often display a row and seat number to help theatergoers find their seats. If there are 26 rows (0 to 25) and 100 seats (0 to 99) in each row, write a nested for loop to print out all of the different seat combinations in the theater.

Example output for row-seat information: output each row and seat number on a separate line

```javascript
0-0
0-1
0-2
...
25-97
25-98
25-99
```

```javascript
/*
 * Programming Quiz: Find my Seat (4-8)
 *
 * Write a nested for loop to print out all of the different seat combinations in the theater.
 * The first row-seat combination should be 0-0
 * The last row-seat combination will be 25-99
 *
 * Things to note:
 *  - the row and seat numbers start at 0, not 1
 *  - the highest seat number is 99, not 100
 */

// Write your code here
for (var x = 0; x < 26; x++) {
    for (var y = 0; y <100; y++) {
        console.log(x + "-" + y)
    }
}
```

### Functions

Functions allow you to package up lines of code that you can use (and often reuse) in your programs.

Sometimes they take parameters like the pizza button from the beginning of this lesson. reheatPizza() had one parameter: the number of slices.

```javascript
function reheatPizza(numSlices) {
  // code that figures out reheat settings!
}
```

The reverseString() function that you saw also had one parameter: the string to be reversed.

```javascript
function reverseString(reverseMe) {
  // code to reverse a string!
}
```

In both cases, the parameter is listed as a variable after the function name, inside the parentheses. And, if there were multiple parameters, you would just separate them with commas.

```javascript
function doubleGreeting(name, otherName) {
  // code to greet two people!
}
```

But, you can also have functions that don't have any parameters. Instead, they just package up some code and perform some task. In this case, you would just leave the parentheses empty. Take this one for example. Here's a simple function that just prints out "Hello!".

```javascript
// accepts no parameters! parentheses are empty
function sayHello() {
  var message = "Hello!"
  console.log(message);
}
```

If you tried pasting any of the functions above into the JavaScript console, you probably didn't notice much happen. In fact, you probably saw undefined returned back to you. undefined is the default return value on the console when nothing is explicitly returned using the special return keyword.

Return statements
In the sayHello() function above, a value is printed to the console with console.log, but not explicitly returned with a return statement. You can write a return statement by using the return keyword followed by the expression or value that you want to return.

```javascript
// declares the sayHello function
function sayHello() {
  var message = "Hello!"
  return message; // returns value instead of printing it
}
```

How to run a function
Now, to get your function to do something, you have to invoke or call the function using the function name, followed by parentheses with any arguments that are passed into it. Functions are like machines. You can build the machine, but it won't do anything unless you also turn it on. Here's how you would call the sayHello() function from before, and then use the return value to print to the console:

```javascript
// declares the sayHello function
function sayHello() {
  var message = "Hello!"
  return message; // returns value instead of printing it
}

// function returns "Hello!" and console.log prints the return value
console.log(sayHello());
```

Prints: "Hello!"

Parameters vs. Arguments

At first, it can be a bit tricky to know when something is either a parameter or an argument. The key difference is in where they show up in the code. A parameter is always going to be a variable name and appears in the function declaration. On the other hand, an argument is always going to be a value (i.e. any of the JavaScript data types - a number, a string, a boolean, etc.) and will always appear in the code when the function is called or invoked.

Try declaring and calling some functions on your own:

```javascript
function findAverage(x, y) {
  var answer = (x + y) / 2;
  return answer;
}

var avg = findAverage(5, 9);
```

Are x and y parameters or arguments for this function?

### Programming quiz

Declare a function called laugh() that returns "hahahahahahahahahaha!". Print the value returned from the laugh() function to the console.

```javascript
/*
 * Programming Quiz: Laugh it Off 1 (5-1)
 */

// your code goes here
function laugh() {
    var m = "hahahahahahahahahaha!";
    return m;
}
console.log(laugh());
```

Write a function called laugh() that takes one parameter, num that represents the number of "ha"s to return.

Here's an example of the output and how to call the function that you will write:

```javascript
console.log(laugh(3));
Prints: "hahaha!"
```

```javascript
/*
 * Programming Quiz: Laugh it Off 2 (5-2)
 *
 * Write a function called `laugh` with a parameter named `num` that represents the number of "ha"s to return.
 *
 * Note:
 *  - make sure your the final character is an exclamation mark ("!")
 */
function laugh(num) {
    var m = "";
    for (var x = 1; x <= num; x++){
        m += "ha";
    }
    return m += "!";
}

console.log(laugh(3));
```

### Return values

It’s important to understand that return and print are not the same thing. Printing a value to the JavaScript console only displays a value (that you can view for debugging purposes), but the value it displays can't really be used for anything more than that. For this reason, you should remember to only use console.log to test your code in the JavaScript console.

Paste the following function declaration and function invocation into the JavaScript console to see the difference between logging (printing) and returning:

```javascript
function isThisWorking(input) {
  console.log("Printing: isThisWorking was called and " + input + " was passed in as an argument.");
  return "Returning: I am returning this string!";
}

isThisWorking(3);

```

If you don't explicitly define a return value, the function will return undefined by default.

```javascript
function isThisWorking(input) {
  console.log("Printing: isThisWorking was called and " + input + " was passed in as an argument.");
}

isThisWorking(3);


```

What does this function "return"?

```javascript
function sleep() {
  console.log("I'm sleepy!");
  return "zzz";
  return "snore";
}

sleep();
```

What number will be "printed" (to the JavaScript console)?

```javascript
function square(x) {
  return x * x;
}

function subtractFour(x) {
  return square(x) - 4;
}

console.log(subtractFour(5)); // 21

```

What do you think will happen with the following code?

```javascript
function test() {
  return 1;
  return 2;
}

test();
```

Returning a value from a function is great, but what's the use of a return value if you're not going to use the value to do something?

A function's return value can be stored in a variable or reused throughout your program as a function argument. Here, we have a function that adds two numbers together, and another function that divides a number by 2. We can find the average of 5 and 7 by using the add() function to add a pair of numbers together, and then by passing the sum of the two numbers add(5, 7) into the function divideByTwo() as an argument.

And finally, we can even store the final answer in a variable called average and use the variable to perform even more calculations in more places!

```javascript
// returns the sum of two numbers
function add(x, y) {
  return x + y;
}


// returns the value of a number divided by 2
function divideByTwo(num) {
  return num / 2;
}


var sum = add(5, 7); // call the "add" function and store the returned value in the "sum" variable
var average = divideByTwo(sum); // call the "divideByTwo" function and store the returned value in the "average" variable
```

Try predicting what will be printed in the console.log statement below. Then, check your prediction by pasting the code into the JavaScript console. Functions can be tricky, so try figuring it out before running the code!

```javascript
function addTen(x) {
  return x + 10;
}

function divideByThree(y) {
  return y / 3;
}

var result = addTen(2);
console.log(divideByThree(result));
```

### Scope

Which of these variables a, b, c, or d, is defined in the global scope?

```javascript
var a = 1;
function x() {
  var b = 2;
  function y() {
    var c = 3;
    function z() {
      var d = 4;
    }
    z();
  }
  y();
}

x();
```

Where can you print out the value of variable c without resulting in an error?

```javascript
var a = 1;
function x() {
  var b = 2;
  function y() {
    var c = 3;
    function z() {
      var d = 4;
    }
    z();
  }
  y();
}

x();
```

### Shadowing

Without pasting into your console, what do you think this code will print out?

```javascript
var x = 1;

function addTwo() {
  x = x + 2;
}

addTwo();
x = x + 1;
console.log(x);
```

Without pasting into your console, what do you think this code will print out?

```javascript
var x = 1;

function addTwo() {
  var x = x + 2;
}

addTwo();
x = x + 1;
console.log(x);
```

- If an identifier is declared in global scope, it's available everywhere.
- If an identifier is declared in function scope, it's available in the function it was declared in (even in functions declared inside the function).
- When trying to access an identifier, the JavaScript Engine will first look in the current function. If it doesn't find anything, it will continue to the next outer function to see if it can find the identifier there. It will keep doing this until it reaches the global scope.
- Global identifiers are a bad idea. They can lead to bad variable names, conflicting variable names, and messy code.

### Hoisting

Sometimes your JavaScript code will produce errors that may seem counterintuitive at first. Hoisting is another one of those topics that might be the cause of some of these tricky errors you're debugging.

Hoisting is JavaScript's default behavior of moving **declarations** to the top.

```javascript
function sayGreeting() {
    console.log(greeting);
    var greeting;
}

sayGreeting();
```

What value will be printed to the console?

```javascript
sayHi("Julia");

function sayHi(name) {
  console.log(greeting + " " + name);
  var greeting;
}
```

What value will be printed to the console?

```javascript
sayHi("Julia");

function sayHi(name) {
  console.log(greeting + " " + name);
  var greeting = "Hello";
}
```

What value will be printed to the console?

```javascript
function sayHi(name) {
  var greeting = "Hello";
  console.log(greeting + " " + name);
}

sayHi("Julia");
```

Conclusion:

- JavaScript hoists function declarations and variable declarations to the top of the current scope.
- Variable assignments are not hoisted.
- Declare functions and variables at the top of your scripts, so the syntax and behavior are consistent with each other.

For this quiz, you're going to create a function called buildTriangle() that will accept an input (the triangle at its widest width) and will return the string representation of a triangle. See the example output below.

buildTriangle(10);

Returns:

```javascript
*
* *
* * *
* * * *
* * * * *
* * * * * *
* * * * * * *
* * * * * * * *
* * * * * * * * *
* * * * * * * * * *
```

We've given you one function makeLine() to start with. The function takes in a line length, and builds a line of asterisks and returns the line with a newline character.

```javascript
function makeLine(length) {
  var line = "";
  for (var j = 1; j <= length; j++) {
    line += "* "
  }
  return line + "\n";
}
```

You will need to call this makeLine() function in buildTriangle().

This will be the most complicated program you've written yet, so take some time thinking through the problem before diving into the code. What tools will you need from your JavaScript tool belt? Professionals plan out their code before writing anything. Think through the steps your code will need to take and write them down in order. Then go through your list and convert each step into actual code. Good luck!

```javascript
/*
 * Programming Quiz: Build A Triangle
 */

// creates a line of * for a given length
function makeLine(length) {
    var line = "";
    for (var j = 1; j <= length; j++) {
        line += "* ";
    }
    return line + "\n";
}

// your code goes here.  Make sure you call makeLine() in your own code.
function buildTriangle(lines) {
    var triangle = "";
    for (i = 1; i <= lines; i++){
        triangle += makeLine(i);
    }
    return triangle;
}
// test your code by uncommenting the following line
console.log(buildTriangle(10));
```

### Function Expression

Once you know how to declare a function, a whole new set of possibilities will open up to you.

For instance, remember how you can store anything you want in a variable? Well, in JavaScript, you can also store functions in variables. When a function is stored inside a variable it's called a function expression.

```javascript
var catSays = function(max) {
  var catMessage = "";
  for (var i = 0; i < max; i++) {
    catMessage += "meow ";
  }
  return catMessage;
};
```

Notice how the function keyword no longer has a name.

```javascript
var catSays = function(max) { 
  // code here 
};
```

It's an anonymous function, a function with no name, and you've stored it in a variable called catSays.

And, if you try accessing the value of the variable catSays, you'll even see the function returned back to you.

```javascript
catSays;
```

```javascript
function(max) {
  var catMessage = ""
  for (var i = 0; i < max; i++) {
    catMessage += "meow ";
  }
  return catMessage;
}
```

### Functions as parameters

Being able to store a function in a variable makes it really simple to pass the function into another function. A function that is passed into another function is called a callback. Let's say you had a helloCat() function, and you wanted it to return "Hello" followed by a string of "meows" like you had with catSays. Well, rather than redoing all of your hard work, you can make helloCat() accept a callback function, and pass in catSays.

```javascript
// function expression catSays
var catSays = function(max) {
  var catMessage = "";
  for (var i = 0; i < max; i++) {
    catMessage += "meow ";
  }
  return catMessage;
};

// function declaration helloCat accepting a callback
function helloCat(callbackFunc) {
  return "Hello " + callbackFunc(3);
}

// pass in catSays as a callback function
helloCat(catSays);
```

A function expression is when a function is assigned to a variable. And, in JavaScript, this can also happen when you pass a function inline as an argument to another function. Take the favoriteMovie example for instance:

```javascript
// Function expression that assigns the function displayFavorite 
// to the variable favoriteMovie
var favoriteMovie = function displayFavorite(movieName) {
  console.log("My favorite movie is " + movieName);
};

// Function declaration that has two parameters: a function for displaying
// a message, along with a name of a movie
function movies(messageFunction, name) {
  messageFunction(name);
}

// Call the movies function, pass in the favoriteMovie function and name of movie
movies(favoriteMovie, "Finding Nemo");
```

But you could have bypassed the first assignment of the function, by passing the function to the movies() function inline.

```javascript
// Function declaration that takes in two arguments: a function for displaying
// a message, along with a name of a movie
function movies(messageFunction, name) {
  messageFunction(name);
}

// Call the movies function, pass in the function and name of movie
movies(function displayFavorite(movieName) {
  console.log("My favorite movie is " + movieName);
}, "Finding Nemo");
```

This type of syntax, writing function expressions that pass a function into another function inline, is really common in JavaScript. It can be a little tricky at first, but be patient, keep practicing, and you'll start to get the hang of it!

Using an anonymous inline function expression might seem like a very not-useful thing at first. Why define a function that can only be used once and you can't even call it by name?

Anonymous inline function expressions are often used with function callbacks that are probably not going to be reused elsewhere. Yes, you could store the function in a variable, give it a name, and pass it in like you saw in the examples above. However, when you know the function is not going to be reused, it could save you many lines of code to just define it inline.

Conclusion:

Function Expression: When a function is assigned to a variable. The function can be named, or anonymous. Use the variable name to call a function defined in a function expression.

```javascript
// anonymous function expression
var doSomething = function(y) {
  return y + 1;
};

// named function expression
var doSomething = function addOne(y) {
  return y + 1;
};

// for either of the definitions above, call the function like this:
doSomething(5);
```

You can even pass a function into another function inline. This pattern is commonly used in JavaScript, and can be helpful streamlining your code.

```javascript
// function declaration that takes in two arguments: a function for displaying
// a message, along with a name of a movie
function movies(messageFunction, name) {
  messageFunction(name);
}

// call the movies function, pass in the function and name of movie
movies(function displayFavorite(movieName) {
  console.log("My favorite movie is " + movieName);
}, "Finding Nemo");
```

### Programming quiz

Write an anonymous function expression that stores a function in a variable called "laugh" and outputs the number of "ha"s that you pass in as an argument.

```javascript
laugh(3);
Returns: hahaha!

```

```javascript
/*
 * Programming Quiz: Laugh (5-4)
 */

var laugh = function(times) {
    var str = "";
    for (i = 1; i <= times; i++){
    str += "ha"
    }
    return str + "!";
}/* finish the function expression */

console.log(laugh(2));
```

Write a named function expression that stores the function in a variable called cry and returns "boohoo!". Don't forget to call the function using the variable name, not the function name:

```javascrpt
cry();
Returns: boohoo!
```

```javascrpt
/*
 * Programming Quiz: Cry (5-5)
 */

// your code goes here
var cry= function sad() {
    return"boohoo!";
}
cry();
```

Call the emotions() function so that it prints the output you see below, but instead of passing the laugh() function as an argument, pass an inline function expression instead.

```javascript
emotions("happy", laugh(2)); // you can use your laugh function from the previous quizzes

Prints: "I am happy, haha!"

```

```javascript
/*
 * Programming Quiz: Inline Functions
 */

// don't change this code
function emotions(myString, myFunc) {
    console.log("I am " + myString + ", " + myFunc(2));
}

/* finish the function expression */
emotions("happy", function(n) {
      var laghter="";
      for (i=1;i<=n;i++){
        laghter +="ha";}
    return laghter +='!';
});
// your code goes here
// call the emotions function here and pass in an
// inline function expression
```

### Arrays

An array is useful because it stores multiple values into a single, organized data structure. You can define a new array by listing values separated with commas between square brackets [].

```javascript
// creates a `donuts` array with three strings
var donuts = ["glazed", "powdered", "jelly"];
```

But strings aren’t the only type of data you can store in an array. You can also store numbers, booleans… and really anything!

```javascript
// creates a `mixedData` array with mixed data types
var mixedData = ["abcd", 1, true, undefined, null, "all the things"];
```

You can even store an array in an array to create a nested array!

```javascript
// creates a `arraysInArrays` array with three arrays
var arraysInArrays = [[1, 2, 3], ["Julia", "James"], [true, false, true, false]];
```

Nested arrays can be particularly hard to read, so it's common to write them on one line, using a newline after each comma:

```javascript
var arraysInArrays = [
  [1, 2, 3],
  ["Julia", "James"],
  [true, false, true, false]
];
```

### Programming quiz

The space western TV drama Firefly premiered in the United States on September 20, 2002. Although the show only featured fourteen episodes and was canceled during its first season, it continues to remain popular today with a growing fan base. In the show, the captain Mal, played by Nathan Fillion, leads a crew of renegades on the spaceship Serenity.

Create an array called crew to organize the Serenity’s crew and set it equal to the variables below . You don't need to type out the actual strings, just use the provided variables.

```javascript
var captain = "Mal";
var second = "Zoe";
var pilot = "Wash";
var companion = "Inara";
var mercenary = "Jayne";
var mechanic = "Kaylee";
```

Then, print the crew array to the console.

```javascript
/*
 * Programming Quiz: Building the Crew
 */

var captain = "Mal";
var second = "Zoe";
var pilot = "Wash";
var companion = "Inara";
var mercenary = "Jayne";
var mechanic = "Kaylee";

// your code goes here
var crew= [captain, second, pilot, companion, mercenary, mechanic];

console.log(crew);
```

Starting with this array of prices, change the prices of the 1st, 3rd, and 7th elements in the array.

```javascript
var prices = [1.23, 48.11, 90.11, 8.50, 9.99, 1.00, 1.10, 67.00];
```

Afterwards, print out the prices array to the console.

```javascript
/*
 * Programming Quiz: The Price is Right
 */

var prices = [1.23, 48.11, 90.11, 8.50, 9.99, 1.00, 1.10, 67.00];

// your code goes here
prices[0]=0;
prices[2]=0;
prices[6]=0;

console.log(prices);
```

### Array Properties and Methods

Array.length

You can find the length of an array by using its length property.

```javascript
var donuts = ["glazed", "powdered", "sprinkled"];
console.log(donuts.length);
```

What is the length of the following inventory array?

```javascript
var inventory = [
  ["gold pieces", 25],
  ["belt", 4],
  ["ring", 1],
  ["shoes", 2]
];
```

Array.push()

```javascript
var donuts = ["glazed", "chocolate frosted", "Boston creme", "glazed cruller", "cinnamon sugar", "sprinkled"];
donuts.push("powdered"); // pushes "powdered" onto the end of the `donuts` array
```

Array.pop()

Alternatively, you can use the pop() method to remove elements from the end of an array.

```javascript
var donuts = ["glazed", "chocolate frosted", "Boston creme", "glazed cruller", "cinnamon sugar", "sprinkled", "powdered"];

donuts.pop(); // pops "powdered" off the end of the `donuts` array
donuts.pop(); // pops "sprinkled" off the end of the `donuts` array
donuts.pop(); // pops "cinnamon sugar" off the end of the `donuts` array
```

Array.splice()

splice() is another handy method that allows you to add and remove elements from anywhere within an array.

While push() and pop() limit you to adding and removing elements from the end of an array, splice() lets you specify the index location to add new elements, as well as the number of elements you'd like to delete (if any).

```javascript
var donuts = ["glazed", "chocolate frosted", "Boston creme", "glazed cruller"];
donuts.splice(1, 1, "chocolate cruller", "creme de leche"); // removes "chocolate frosted" at index 1 and adds "chocolate cruller" and "creme de leche" starting at index 1
```

The first argument represents the starting index from where you want to change the array, the second argument represents the numbers of elements you want to remove, and the remaining arguments represent the elements you want to add.

We’ve decided to replace some of the donuts in the donuts array.

```javascript
var donuts = ["cookies", "cinnamon sugar", "creme de leche"];

donuts.splice(-2, 0, "chocolate frosted", "glazed");
```

What does the donuts array look like after the following changes?

### Programming quiz

James was creating an array with the colors of the rainbow, and he forgot some colors. The standard rainbow colors are usually listed in this order:

```javascript
var rainbow = ["Red", "Orange", "Yellow", "Green", "Blue", "Purple"];
```

but James had this:

```javascript
var rainbow = ["Red", "Orange", "Blackberry", "Blue"];
```

Using only the splice() method, insert the missing colors into the array, and remove the color "Blackberry" by following these steps:

- Remove "Blackberry"
- Add "Yellow" and "Green"
- Add "Purple"

```javascript
/*
 * Programming Quiz: Colors of the Rainbow
 */

var rainbow = ["Red", "Orange", "Blackberry", "Blue"];

// your code goes here
rainbow.splice(2, 1,"Yellow", "Green");
rainbow.splice(5, 0, "Purple");
console.log(rainbow);
```

In the Harry Potter novels, children attending the Hogwarts School of Witchcraft and Wizardry belong to one of four houses: Gryffindor, Hufflepuff, Ravenclaw, or Slytherin. Each year, the houses assemble a Quidditch team of seven players to compete for the coveted Quidditch Cup.

Consider the following:

```javascript
var team = ["Oliver Wood", "Angelina Johnson", "Katie Bell", "Alicia Spinnet", "George Weasley", "Fred Weasley", "Harry Potter"];
```

Create a function called hasEnoughPlayers() that takes the team array as an argument and returns true or false depending on if the array has at least seven players.

```javascript
/*
 * Programming Quiz: Quidditch Cup
 */

// your code goes here
function hasEnoughPlayers(team) {
    if (team.length >= 7){
        return true;
    } else {
        return false;
    }
}
var team = ["Oliver Wood", "Angelina Johnson", "Katie Bell", "Alicia Spinnet", "George Weasley", "Fred Weasley", "Harry Potter"];
console.log(hasEnoughPlayers(team));
```

In an earlier exercise, you created a crew array to represent Mal’s crew from the hit show Firefly.

```javascript
var captain = "Mal";
var second = "Zoe";
var pilot = "Wash";
var companion = "Inara";
var mercenary = "Jayne";
var mechanic = "Kaylee";

var crew = [captain, second, pilot, companion, mercenary, mechanic];
```

Later in the show, Mal takes on three new crew members named "Simon", "River", and "Book". Use the push() method to add the three new crew members to the crew array.

```javascript
var doctor = "Simon";
var sister = "River";
var shepherd = "Book";
```

```javascript
/*
 * Programming Quiz: Joining the Crew (6-6)
 */

var captain = "Mal";
var second = "Zoe";
var pilot = "Wash";
var companion = "Inara";
var mercenary = "Jayne";
var mechanic = "Kaylee";

var crew = [captain, second, pilot, companion, mercenary, mechanic];

var doctor = "Simon";
var sister = "River";
var shepherd = "Book";

// your code goes here
crew.push(doctor, sister, shepherd);
console.log(crew);
```

Use the MDN Documentation to determine which of these methods would be best for reversing elements in this array:

```javascript
var reverseMe = ["h", "e", "l", "l", "o"];
```

What would be the best array method to sort the elements in this array:

```javascript
var sortMe = [2, 1, 10, 7, 6];
```

Consider the following array, removeFirstElement:

> var removeFirstElement = ["a", "b", "c"];

Let's say that you want to modify (i.e., mutate) removeFirstElement by removing the first element within it. Which method(s) could you use?

> shift()
> splice()

What method would be best for changing this array into a string?

> var turnMeIntoAString = ["U", "d", "a", "c", "i", "t", "y"];
> join()

### Traverse array

Once the data is in the array, you want to be able to efficiently access and manipulate each element in the array without writing repetitive code for each element.

For instance, if this was our original donuts array:

> var donuts = ["jelly donut", "chocolate donut", "glazed donut"];

and we decided to make all the same donut types, but only sell them as donut holes instead, we could write the following code:

> donuts[0] += " hole";
> donuts[1] += " hole";
> donuts[2] += " hole";
> donuts array: ["jelly donut hole", "chocolate donut hole", "glazed donut hole"]

```javascript
var donuts = ["jelly donut", "chocolate donut", "glazed donut"];

// the variable `i` is used to step through each element in the array
for (var i = 0; i < donuts.length; i++) {
    donuts[i] += " hole";
    donuts[i] = donuts[i].toUpperCase();
}
```

### The forEach() loop

Arrays have a set of special methods to help you iterate over and perform operations on collections of data. You can view the MDN Documentation list of Array methods here, but a couple big ones to know are the forEach() and map() methods.

The forEach() method gives you an alternative way to iterate over an array, and manipulate each element in the array with an inline function expression.

```javascript
var donuts = ["jelly donut", "chocolate donut", "glazed donut"];

donuts.forEach(function(donut) {
  donut += " hole";
  donut = donut.toUpperCase();
  console.log(donut);
});
```

Notice that the forEach() method iterates over the array without the need of an explicitly defined index. In the example above, donut corresponds to the element in the array itself. This is different from a for or while loop where an index is used to access each element in the array:

```javascript
for (var i = 0; i < donuts.length; i++) {
  donuts[i] += " hole";
  donuts[i] = donuts[i].toUpperCase();
  console.log(donuts[i]);
}
```

The function that you pass to the forEach() method can take up to three parameters. In the video, these are called element, index, and array, but you can call them whatever you like.

The forEach() method will call this function once for each element in the array (hence the name forEach.) Each time, it will call the function with different arguments. The element parameter will get the value of the array element. The index parameter will get the index of the element (starting with zero). The array parameter will get a reference to the whole array, which is handy if you want to modify the elements.

Here's another example:

```javascript
words = ["cat", "in", "hat"];
words.forEach(function(word, num, all) {
  console.log("Word " + num + " in " + all.toString() + " is " + word);
});
```

### Programming quiz

Use the array's forEach() method to loop over the following array and add 100 to each of the values if the value is divisible by 3.

var test = [12, 929, 11, 3, 199, 1000, 7, 1, 24, 37, 4, 19, 300, 3775, 299, 36, 209, 148, 169, 299, 6, 109, 20, 58, 139, 59, 3, 1, 139];

```javascript
/*
 * Programming Quiz: Another Type of Loop (6-8)
 *
 * Use the existing `test` variable and write a `forEach` loop 
 * that adds 100 to each number that is divisible by 3.
 *
 * Things to note:
 *  - use an `if` statement to verify code is divisible by 3
 *  - use `console.log` to print the `test` variable when you're finished looping
 */

var test = [12, 929, 11, 3, 199, 1000, 7, 1, 24, 37, 4,
            19, 300, 3775, 299, 36, 209, 148, 169, 299,
            6, 109, 20, 58, 139, 59, 3, 1, 139];

// Write your code here
test.forEach(function(num, index, array){
  if(num % 3 === 0){
    array[index] = num += 100;
  }

});

console.log(test);
```

### Map

Using forEach() will not be useful if you want to permanently modify the original array. forEach() always returns undefined. However, creating a new array from an existing array is simple with the powerful map() method.

With the map() method, you can take an array, perform some operation on each element of the array, and return a new array.

```javascript
var donuts = ["jelly donut", "chocolate donut", "glazed donut"];
var improvedDonuts = donuts.map(function(donut) {
  donut += " hole";
  donut = donut.toUpperCase();
  return donut;
});
```

> donuts array: ["jelly donut", "chocolate donut", "glazed donut"]
> improvedDonuts array: ["JELLY DONUT HOLE", "CHOCOLATE DONUT HOLE", "GLAZED DONUT HOLE"]

Oh man, did you just see that? The map() method accepts one argument, a function that will be used to manipulate each element in the array. In the above example, we used a function expression to pass that function into map(). This function is taking in one argument, donut which corresponds to each element in the donuts array. You no longer need to iterate over the indices anymore. map() does all that work for you.

Use the map() method to take the array of bill amounts shown below, and create a second array of numbers called totals that shows the bill amounts with a 15% tip added.

> var bills = [50.23, 19.12, 34.01, 100.11, 12.15, 9.90, 29.11, 12.99, 10.00, 99.22, 102.20, 100.10, 6.77, 2.22];

Print out the new totals array using console.log.

> TIP: Check out the toFixed() method for numbers to help with rounding the values to a maximum of 2 decimal places. Note, that the method returns a string to maintain the "fixed" format of the number. So, if you want to convert the string back to a number, you can cast it or convert it back to a number:

### Arrays in Arrays

```javascript
var donutBox = [
  ["glazed", "chocolate glazed", "cinnamon"],
  ["powdered", "sprinkled", "glazed cruller"],
  ["chocolate cruller", "Boston creme", "creme de leche"]
];

// here, donutBox.length refers to the number of rows of donuts
for (var row = 0; row < donutBox.length; row++) {
  console.log(donutBox[row]);
}

for (var row = 0; row < donutBox.length; row++) {
  // here, donutBox[row].length refers to the length of the donut array currently being looped over
  for (var column = 0; column < donutBox[row].length; column++) {
    console.log(donutBox[row][column]);
  }
}
```

Use a nested for loop to take the numbers array below and replace all of the values that are divisible by 2 (even numbers) with the string "even" and all other numbers with the string "odd".

```javascript
/*
 * Programming Quiz: Nested Numbers (6-10)
 *
 *   - The `numbers` variable is an array of arrays.
 *   - Use a nested `for` loop to cycle through `numbers`.
 *   - Convert each even number to the string "even"
 *   - Convert each odd number to the string "odd"
 */

var numbers = [
    [243, 12, 23, 12, 45, 45, 78, 66, 223, 3],
    [34, 2, 1, 553, 23, 4, 66, 23, 4, 55],
    [67, 56, 45, 553, 44, 55, 5, 428, 452, 3],
    [12, 31, 55, 445, 79, 44, 674, 224, 4, 21],
    [4, 2, 3, 52, 13, 51, 44, 1, 67, 5],
    [5, 65, 4, 5, 5, 6, 5, 43, 23, 4424],
    [74, 532, 6, 7, 35, 17, 89, 43, 43, 66],
    [53, 6, 89, 10, 23, 52, 111, 44, 109, 80],
    [67, 6, 53, 537, 2, 168, 16, 2, 1, 8],
    [76, 7, 9, 6, 3, 73, 77, 100, 56, 100]
];

// your code goes here
for (var row = 0; row < numbers.length; row++) {
  for (var column = 0; column < numbers[row].length; column++) {
    if (numbers[row][column] % 2 ===0){
        numbers[row][column] = "even";
    } else {
        numbers[row][column] = "odd";
    }
  }
}

```

### Objects

Primitive data types: strings, numbers, booleans, undefined, null

typeof is an operator that returns the name of the data type that follows it:

```javascript
typeof "hello" // returns "string"
typeof true // returns "boolean"
typeof [1, 2, 3] // returns "object" (Arrays are a type of object)
typeof function hello() { } // returns "function"
```

Using the umbrella example from the previous video, see if you can follow the example open() method and create the close() method. It's alright if you have trouble at first! We'll go into more detail later in this lesson.

```javascript
var umbrella = {
  color: "pink",
  isOpen: false,
  open: function() {
    if (umbrella.isOpen === true) {
      return "The umbrella is already opened!";
    } else {
      umbrella.isOpen = true;
      return "Julia opens the umbrella!";
    }
   }
};
```

TIP: Remember to put all of your object's properties and methods inside curly braces: var myObject = { greeting: "hello", name: "Julia" };. Also, remember that an object is just another data type. Just like how you would put a semicolon after a string variable declaration var myString = "hello";, don't forget to put a semi-colon at the end of your object's declaration.

```javascript
/*
 * Programming Quiz: Umbrella
 */

var umbrella = {
    color: "pink",
    isOpen: true,
    open: function() {
        if (umbrella.isOpen === true) {
            return "The umbrella is already opened!";
        } else {
            umbrella.isOpen = true;
            return "Julia opens the umbrella!";
        }
    },
    close: function() {
        if (umbrella.isOpen === false) {
            return "The umbrella is already closed!";
        } else {
            umbrella.isOpen = false;
            return "Julia closes the umbrella!";
        }
    },
};
```

### Object-literal notation

```javascript
var sister = {
  name: "Sarah",
  age: 23,
  parents: [ "alice", "andy" ],
  siblings: ["julia"],
  favoriteColor: "purple",
  pets: true
};
```

The syntax you see above is called object-literal notation. There are some important things you need to remember when you're structuring an object literal:

- The "key" (representing a property or method name) and its "value" are separated from each other by a colon
- The key: value pairs are separated from each other by commas
- The entire object is wrapped inside curly braces { }.

And, kind of like how you can look up a word in the dictionary to find its definition, the key in a key:value pair allows you to look up a piece of information about an object. Here's are a couple examples of how you can retrieve information about my sister's parents using the object you created.

```javascript
// two equivalent ways to use the key to return its value
sister["parents"] // returns [ "alice", "andy" ]
sister.parents // also returns ["alice", "andy"]
```

Using sister["parents"] is called bracket notation (because of the brackets!) and using sister.parents is called dot notation (because of the dot!).

The sister object above contains a bunch of properties about my sister, but doesn't really say what my sister does. For instance, let's say my sister likes to paint. You might have a paintPicture() method that returns "Sarah paints a picture!" whenever you call it. The syntax for this is pretty much exactly the same as how you defined the properties of the object. The only difference is, the value in the key:value pair will be a function.

```javascript
var sister = {
  name: "Sarah",
  age: 23,
  parents: [ "alice", "andy" ],
  siblings: ["julia"],
  favoriteColor: "purple",
  pets: true,
  paintPicture: function() { return "Sarah paints!"; }
};

sister.paintPicture();
```

### Variable naming conventions

Feel free to use upper and lowercase numbers and letters, but don't start your property name with a number. You don't need to wrap the string in quotes! If it's a multi-word property, use camel case. Don't use hyphens in your property names

```javascript
var richard = {
  "1stSon": true;
  "loves-snow": true;
};

richard.1stSon // error
richard.loves-snow // error
```

### Programmming quiz

Create a breakfast object to represent the following menu item:

> The Lumberjack - $9.95
> eggs, sausage, toast, hashbrowns, pancakes

The object should contain properties for the name, price, and ingredients.

```javascript
/*
 * Programming Quiz: Menu Items (7-2)
 */

// your code goes here
var breakfast = {
    name:"The Lumberjack",
    price:9.95,
    ingredients:["eggs", "sausage", "toast", "hashbrowns", "pancakes"]
}
```

Using the given object:

```javascript
var savingsAccount = {
  balance: 1000,
  interestRatePercent: 1,
  deposit: function addMoney(amount) {
    if (amount > 0) {
      savingsAccount.balance += amount;
    }
  },
  withdraw: function removeMoney(amount) {
    var verifyBalance = savingsAccount.balance - amount;
    if (amount > 0 && verifyBalance >= 0) {
      savingsAccount.balance -= amount;
    }
  }
};
```

add a printAccountSummary() method that returns the following account message:

> Welcome!
> Your balance is currently $1000 and your interest rate is 1%.

```javascript
/*
 * Programming Quiz: Bank Accounts 1 (7-3)
 */

var savingsAccount = {
    balance: 1000,
    interestRatePercent: 1,
    deposit: function addMoney(amount) {
        if (amount > 0) {
            savingsAccount.balance += amount;
        }
    },
    withdraw: function removeMoney(amount) {
        var verifyBalance = savingsAccount.balance - amount;
        if (amount > 0 && verifyBalance >= 0) {
            savingsAccount.balance -= amount;
        }
    },
    // your code goes here
    printAccountSummary() {
        return("Welcome!\nYour balance is currently $"+savingsAccount.balance+" and your interest rate is "+ savingsAccount.interestRatePercent+"%.");
    }
};

console.log(savingsAccount.printAccountSummary());
```

Create an object called facebookProfile. The object should have 3 properties:

- your name
- the number of friends you have, and
- an array of messages you've posted (as strings)
- The object should also have 4 methods:

- postMessage(message) - adds a new message string to the array
- deleteMessage(index) - removes the message corresponding to the index provided
- addFriend() - increases the friend count by 1
- removeFriend() - decreases the friend count by 1

```javascript
/*
 * Programming Quiz: Facebook Friends (7-5)
 */

// your code goes here
var facebookProfile = {
  name: "James",
  friends: 1,
  messages: ["1", "2", "3"],
  postMessage: function addMessage(message){
      facebookProfile.messages.push(message);
  },
  deleteMessage: function removeMessage(index){
      if (facebookProfile.messages.length > 0){
          facebookProfile.messages.splice(index,1);
      }
  },
  addFriend: function(){
      facebookProfile.friends++;
  },
  removeFriend: function(){
      facebookProfile.friends--;
  },
};
```

Here is an array of donut objects.

```javascript
var donuts = [
  { type: "Jelly", cost: 1.22 },
  { type: "Chocolate", cost: 2.45 },
  { type: "Cider", cost: 1.59 },
  { type: "Boston Cream", cost: 5.99 }
];
```

Use the forEach() method to loop over the array and print out the following donut summaries using console.log.

```javascript
Jelly donuts cost $1.22 each
Chocolate donuts cost $2.45 each
Cider donuts cost $1.59 each
Boston Cream donuts cost $5.99 each
```

```javascript
/*
 * Programming Quiz: Donuts Revisited (7-6)
 */

var donuts = [
    { type: "Jelly", cost: 1.22 },
    { type: "Chocolate", cost: 2.45 },
    { type: "Cider", cost: 1.59 },
    { type: "Boston Cream", cost: 5.99 }
];

// your code goes here

donuts.forEach(function(donut) {
    console.log(donut.type + " donuts cost $" + donut.cost + " each");
});
 ```

## Syntax with ES6 and more

### Let and Const

There are now two new ways to declare variables in JavaScript: let and const.

Up until now, the only way to declare a variable in JavaScript was to use the keyword var. To understand why let and const were added, it’s probably best to look at an example of when using var can get us into trouble.

Take a look at the following code.

What do you expect to be the output from running getClothing(false)?

```javascript
function getClothing(isCold) {
  if (isCold) {
    var freezing = 'Grab a jacket!';
  } else {
    var hot = 'It’s a shorts kind of day.';
    console.log(freezing);
  }
}
```

Hoisting is a result of how JavaScript is interpreted by your browser. Essentially, before any JavaScript code is executed, all variables are "hoisted", which means they're raised to the top of the function scope. So at run-time, the getClothing() function actually looks more like this…

```javascript
function getClothing(isCold) {
  var freezing, hot;
  if (isCold) {
    freezing = 'Grab a jacket!';
  } else {
    hot = 'It’s a shorts kind of day.';
    console.log(freezing);
  }
}
```

Variables declared with let and const eliminate this specific issue of hoisting because they’re scoped to the block, not to the function. Previously, when you used var, variables were either scoped globally or locally to an entire function scope.

If a variable is declared using let or const inside a block of code (denoted by curly braces { }), then the variable is stuck in what is known as the temporal dead zone until the variable’s declaration is processed. This behavior prevents variables from being accessed only until after they’ve been declared.

What do you expect to be the output from running getClothing(false)?

```javascript
function getClothing(isCold) {
  if (isCold) {
    const freezing = 'Grab a jacket!';
  } else {
    const hot = 'It’s a shorts kind of day.';
    console.log(freezing);
  }
}
```

let and const also have some other interesting properties.

- Variables declared with let can be reassigned, but can’t be redeclared in the same scope.
- Variables declared with const must be assigned an initial value, but can’t be redeclared in the same scope, and can’t be reassigned.

Is there any reason to use var anymore? Not really.

There are some arguments that can be made for using var in situations where you want to globally define variables, but this is often considered bad practice and should be avoided. From now on, we suggest ditching var in place of using let and const.

### Template Literals

Prior to ES6, the old way to concatenate strings together was by using the string concatenation operator ( + ).

```javascript
const student = {
  name: 'Richard Kalehoff',
  guardian: 'Mr. Kalehoff'
};

const teacher = {
  name: 'Mrs. Wilson',
  room: 'N231'
}

let message = student.name + ' please see ' + teacher.name + ' in ' + teacher.room + ' to pick up your report card.';
```

This works alright, but it gets more complicated when you need to build multi-line strings.

```javascript
let note = teacher.name + ',\n\n' +
  'Please excuse ' + student.name + '.\n' +
  'He is recovering from the flu.\n\n' +
  'Thank you,\n' +
  student.guardian;
```

Template literals are essentially string literals that include embedded expressions.

Denoted with backticks ( `` ) instead of single quotes ( '' ) or double quotes ( "" ), template literals can contain placeholders which are represented using ${expression}. This makes it much easier to build strings.

Here's the previous examples using template literals.

```javascript
let message = `${student.name} please see ${teacher.name} in ${teacher.room} to pick up your report card.`;
```

By using template literals, you can drop the quotes along with the string concatenation operator. Also, you can reference the object's properties inside expressions.

Here, you try. Change the greeting string below to use a template literal. Also, feel free to swap in your name for the placeholder.

```javascript
/*
 * Instructions: Change the `greeting` string to use a template literal.
 */

const myName = 'Simon';
const greeting = `Hello, my name is ${myName}`;
console.log(greeting);
```

Here’s where template literals really shine. In the animation above, the quotes and string concatenation operator have been dropped, as well as the newline characters ( \n ). That's because template literals also preserve newlines as part of the string!

```javascript
const student = {
  name: 'Richard Kalehoff',
  guardian: 'Mr. Kalehoff'
};

const teacher = {
  name: 'Mrs. Wilson',
  room: 'N231'
}
/*
let note = teacher.name + ',\n\n' +
  'Please excuse ' + student.name + '.\n' +
  'He is recovering from the flu.\n\n' +
  'Thank you,\n' +
  student.guardian;
*/
let note = `${teacher.name},

Please excuse ${student.name}.
He is recovering from the flu.

Thank you,
${student.gurdian}`;
```

Modify the createAnimalTradingCardHTML() function to use a template literal for cardHTML.

```javascript
/*
 * Programming Quiz: Build an HTML Fragment (1-2)
 */

const cheetah = {
    name: 'Cheetah',
    scientificName: 'Acinonyx jubatus',
    lifespan: '10-12 years',
    speed: '68-75 mph',
    diet: 'carnivore',
    summary: 'Fastest mammal on land, the cheetah can reach speeds of 60 or perhaps even 70 miles (97 or 113 kilometers) an hour over short distances. It usually chases its prey at only about half that speed, however. After a chase, a cheetah needs half an hour to catch its breath before it can eat.',
    fact: 'Cheetahs have “tear marks” that run from the inside corners of their eyes down to the outside edges of their mouth.'
};

// creates an animal trading card
function createAnimalTradingCardHTML(animal) {
    const cardHTML = '<div class="card">' +
        '<h3 class="name">' + animal.name + '</h3>' +
        '<img src="' + animal.name + '.jpg" alt="' + animal.name +'" class="picture">' +
        '<div class="description">' +
            '<p class="fact">' + animal.fact + '</p>' +
            '<ul class="details">' +
                '<li><span class="bold">Scientific Name</span>: ' + animal.scientificName + '</li>' +
                '<li><span class="bold">Average Lifespan</span>: ' + animal.lifespan + '</li>' +
                '<li><span class="bold">Average Speed</span>: ' + animal.speed + '</li>' +
                '<li><span class="bold">Diet</span>: ' + animal.diet + '</li>' +
            '</ul>' +
            '<p class="brief">' + animal.summary + '</p>' +
        '</div>' +
    '</div>';

    return cardHTML;
}

console.log(createAnimalTradingCardHTML(cheetah));
```

```javascript
/*
 * Programming Quiz: Build an HTML Fragment (1-2)
 */

const cheetah = {
    name: 'Cheetah',
    scientificName: 'Acinonyx jubatus',
    lifespan: '10-12 years',
    speed: '68-75 mph',
    diet: 'carnivore',
    summary: 'Fastest mammal on land, the cheetah can reach speeds of 60 or perhaps even 70 miles (97 or 113 kilometers) an hour over short distances. It usually chases its prey at only about half that speed, however. After a chase, a cheetah needs half an hour to catch its breath before it can eat.',
    fact: 'Cheetahs have “tear marks” that run from the inside corners of their eyes down to the outside edges of their mouth.'
};

// creates an animal trading card
function createAnimalTradingCardHTML(animal) {
    const cardHTML = `<div class="card">
        <h3 class="name">${animal.name}</h3>
        <img src="${animal.name}.jpg" alt="${animal.name}" class="picture">
        <div class="description">
            <p class="fact">${animal.fact}</p>
            <ul class="details">
                <li><span class="bold">Scientific Name</span>: ${animal.scientificName}</li>
                <li><span class="bold">Average Lifespan</span>: ${animal.lifespan}</li>
                <li><span class="bold">Average Speed</span>: ${animal.speed}</li>
                <li><span class="bold">Diet</span>: ${animal.diet}</li>
            </ul>
            <p class="brief">${animal.summary}</p>
        </div>
    </div>`;

    return cardHTML;
}

console.log(createAnimalTradingCardHTML(cheetah));
```

### Destructuring

In ES6, you can extract data from arrays and objects into distinct variables using destructuring.

This probably sounds like something you’ve done before, for example, look at the two code snippets below that extract data using pre-ES6 techniques:

```javascript
const point = [10, 25, -34];

const x = point[0];
const y = point[1];
const z = point[2];

console.log(x, y, z);
```

The example above shows extracting values from an array.

```javascript
const gemstone = {
  type: 'quartz',
  color: 'rose',
  karat: 21.29
};

const type = gemstone.type;
const color = gemstone.color;
const karat = gemstone.karat;

console.log(type, color, karat);
```

And this example shows extracting values from an object.

Both are pretty straightforward, however, neither of these examples are actually using destructuring.

Destructuring borrows inspiration from languages like Perl and Python by allowing you to specify the elements you want to extract from an array or object on the left side of an assignment. It sounds a little weird, but you can actually achieve the same result as before, but with much less code; and it's still easy to understand.

Destructuring values from an array

```javascript
const point = [10, 25, -34];

const [x, y, z] = point;

console.log(x, y, z);

```

In this example, the brackets [ ] represent the array being destructured and x, y, and z represent the variables where you want to store the values from the array. Notice how you don’t have to specify the indexes for where to extract the values from because the indexes are implied.

TIP: You can also ignore values when destructuring arrays. For example, const [x, , z] = point; ignores the y coordinate and discards it.

Destructuring values from an object

```javascript
const gemstone = {
  type: 'quartz',
  color: 'rose',
  karat: 21.29
};

const {type, color, karat} = gemstone;

console.log(type, color, karat);
```

In this example, the curly braces { } represent the object being destructured and type, color, and karat represent the variables where you want to store the properties from the object. Notice how you don’t have to specify the property from where to extract the values. Because gemstone has a property named type, the value is automatically stored in the type variable. Similarly, gemstone has a color property, so the value of color automatically gets stored in the color variable. And it's the same with karat.

> TIP: You can also specify the values you want to select when destructuring an object. For example, let {color} = gemstone; will only select the color property from the gemstone object.

What do you expect to be returned from calling getArea()?

```javascript
const circle = {
  radius: 10,
  color: 'orange',
  getArea: function() {
    return Math.PI * this.radius * this.radius;
  },
  getCircumference: function() {
    return 2 * Math.PI * this.radius;
  }
};

let {radius, getArea, getCircumference} = circle;
```

Use array destructuring to pull out the three colors from the array of things and store them into the variables one, two, and three.

```javascript
/*
 * Programming Quiz: Destructuring Arrays
 *
 * Use destructuring to initialize the variables `one`, `two`, and `three`
 * with the colors from the `things` array.
 */

const things = ['red', 'basketball', 'paperclip', 'green', 'computer', 'earth', 'udacity', 'blue', 'dogs'];

const [one, , , two, , , , three] = things;

const colors = `List of Colors
1. ${one}
2. ${two}
3. ${three}`;

console.log(colors);
```

## the Document Object Model -- The DOM

```javascript
document.getElementById('callout');

document.getElementsByClassName();

document.getElementsByTagName();
```

## Advanced JavaScript

### Array.unshift()

The unshift() method adds one or more elements to the beginning of an array and returns the new length of the array.

```javascript
var array1 = [1, 2, 3];

console.log(array1.unshift(4, 5));
// expected output: 5

console.log(array1);
// expected output: Array [4, 5, 1, 2, 3]

var arr = [1, 2];

arr.unshift(0); // result of call is 3, the new array length
// arr is [0, 1, 2]

arr.unshift(-2, -1); // = 5
// arr is [-2, -1, 0, 1, 2]

arr.unshift([-3]);
// arr is [[-3], -2, -1, 0, 1, 2]
```

### Array.shift()

The shift() method removes the first element from an array and returns that removed element. This method changes the length of the array.

```javascript
var array1 = [1, 2, 3];

var firstElement = array1.shift();

console.log(array1);
// expected output: Array [2, 3]

console.log(firstElement);
// expected output: 1


// Removing an element from an array
var myFish = ['angel', 'clown', 'mandarin', 'surgeon'];

console.log('myFish before:', JSON.stringify(myFish));
// myFish before: ['angel', 'clown', 'mandarin', 'surgeon']

var shifted = myFish.shift();

console.log('myFish after:', myFish);
// myFish after: ['clown', 'mandarin', 'surgeon']

console.log('Removed this element:', shifted);
// Removed this element: angel

// Using shift() method in while loop
var names = ["Andrew", "Edward", "Paul", "Chris" ,"John"];

while( (i = names.shift()) !== undefined ) {
    console.log(i);
}
// Andrew, Edward, Paul, Chris, John
```

### Array.concat()

The concat() method is used to merge two or more arrays. This method does not change the existing arrays, but instead returns a new array.

```javascript
var array1 = ['a', 'b', 'c'];
var array2 = ['d', 'e', 'f'];

console.log(array1.concat(array2));
// expected output: Array ["a", "b", "c", "d", "e", "f"]
```

Concatenating two arrays

```javascript
var alpha = ['a', 'b', 'c'];
var numeric = [1, 2, 3];

alpha.concat(numeric);
// result in ['a', 'b', 'c', 1, 2, 3]
```

Concatenating three arrays

```javascript
var num1 = [1, 2, 3],
    num2 = [4, 5, 6],
    num3 = [7, 8, 9];

var nums = num1.concat(num2, num3);

console.log(nums);
// results in [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

Concatenating values to an array

```javascript
var alpha = ['a', 'b', 'c'];

var alphaNumeric = alpha.concat(1, [2, 3]);

console.log(alphaNumeric);
// results in ['a', 'b', 'c', 1, 2, 3]
```

Concatenating nested arrays

```javascript
var num1 = [[1]];
var num2 = [2, [3]];

var nums = num1.concat(num2);

console.log(nums);
// results in [[1], 2, [3]]

// modify the first element of num1
num1[0].push(4);

console.log(nums);
// results in [[1, 4], 2, [3]]
```

### parseInt

The parseInt() function parses a string argument and returns an integer of the specified radix (the base in mathematical numeral systems).

```javascript
function roughScale(x, base) {
  var parsed = parseInt(x, base);
  if (isNaN(parsed)) { return 0 }
  return parsed * 100;
}

console.log(roughScale(' 0xF', 16));
// expected output: 1500

console.log(roughScale('321', 2));
// expected output: 0
```

The following examples all return 15:

```javascript
parseInt(' 0xF', 16);
parseInt(' F', 16);
parseInt('17', 8);
parseInt(021, 8);
parseInt('015', 10);   // parseInt(015, 10); will return 15
parseInt(15.99, 10);
parseInt('15,123', 10);
parseInt('FXX123', 16);
parseInt('1111', 2);
parseInt('15 * 3', 10);
parseInt('15e2', 10);
parseInt('15px', 10);
parseInt('12', 13);
```

The following examples all return NaN:

```javascript
parseInt('Hello', 8); // Not a number at all
parseInt('546', 2);   // Digits are not valid for binary representations
```

The following examples all return -15:

```javascript
parseInt('-F', 16);
parseInt('-0F', 16);
parseInt('-0XF', 16);
parseInt(-15.1, 10);
parseInt(' -17', 8);
parseInt(' -15', 10);
parseInt('-1111', 2);
parseInt('-15e1', 10);
parseInt('-12', 13);
```

The following examples all return 4:

```javascript
parseInt(4.7, 10);
parseInt(4.7 * 1e22, 10); // Very large number becomes 4
parseInt(0.00000000000434, 10); // Very small number becomes 4
```

The following example returns 224:

```javascript
parseInt('0e0', 16);
```

### Timing Events

```javascript
setTimeout
```

### toUpperCase method

### Bitwise operators

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators

https://baike.baidu.com/item/%E4%BD%8D%E8%BF%90%E7%AE%97/6888804?fr=aladdin

https://www.cnblogs.com/xljzlw/p/4231354.html

### Arguments object

https://developer.mozilla.org/en-US/docs/Web/JavaScript

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply

### regex

http://www.cnblogs.com/-ShiL/archive/2012/04/06/Star201204061009.html
