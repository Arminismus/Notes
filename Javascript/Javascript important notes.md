```javascript
console.log("hello world!")
```

#flashcards
How do you write a variable scoped to the function body in Javascript? 
?
```javascript
var name = value;
```
<!--SR:!2023-05-23,8,250-->

How do you define variables only in the current `{}` scope?
?
```javascript
let name = value;
```
<!--SR:!2023-05-25,10,250-->

How to increment a variable in javacript?
?
```javascript
myVar++;
```
<!--SR:!2023-05-25,10,250-->

How can we find the length of a string in Javascript?
?
```javascript
string.length;
```
<!--SR:!2023-05-22,7,250-->

Strings are {{immutable}} in Javascript. They {{cannot}} be changed.
<!--SR:!2023-05-23,8,250!2023-05-24,9,250-->

How can we push items to the array in Javascript?
?
```javascript
ourArray.push(item);
```
<!--SR:!2023-05-21,6,250-->

Remove an item from the beginning of an array?
?
```javascript
ourArray.shift();
```
<!--SR:!2023-05-23,8,250-->

Add an item to the beginning of an array?
?
```javascript
ourArray.unshift("hello");
```
<!--SR:!2023-05-21,4,230-->


How to define a global variable from inside a function?
?
By removing the var keyword:
```javascript
myVariable = value;
```
<!--SR:!2023-05-21,6,250-->


What does this piece of code return?
```javascript
console.log(3 === '3');
console.log(3 =='3');
```
?
```console
false
true
```
<!--SR:!2023-05-22,7,250-->

What does this piece of code return?
```javascript
console.log(99 != '99');
console.log(99 !== '99');
```
?
```console
false
true
```
<!--SR:!2023-05-24,9,250-->

Write an else if statement in Javascript?
?
```javascript
if (condition){
	// your code
} else if (newCondition){
	// your code
};
```
<!--SR:!2023-05-24,8,250-->


Write a switch statement in Javascipt?
?
```javascript
//val is the input to the switch statement
switch(val){
	case 1:
		answer = "alpha";
		break;
	case 2:
		answer = "beta";
		break;
	
	default: 
		answer = "stuff";
		break;
};
```
<!--SR:!2023-05-26,10,250-->

Write a switch statement in Javascript that does the same action for `val = 1` and `val = 2`.
?
```javascript
switch(val){
	case 1:
	case 2:
		answer = "hello"
		break;
	case 3:
		answer = "bye"
		break;
};
```
<!--SR:!2023-05-25,9,250-->


Write a javascript object that is about a user profile?
?
```javascript
var obj = {
	"name":"Skylar",
	"house":false,
	"friends":10,
	"wives":["Samantha","Autumn","Felicity"]
};
```
<!--SR:!2023-05-26,10,250-->


Access the `hat` property of the object `man` in javascript?
?
```javascript
console.log(man.hat);
//or
console.log(man["hat"]);
```
<!--SR:!2023-05-22,6,250-->

Delete the property `bark` from javascript object `myDog`.
?
```javascript
delete myDog.bark;
```
<!--SR:!2023-05-26,10,250-->


Check if a javascript object `man` has a property `bark` ?
?
```javascript
console.log(man.hasOwnProperty('bark'));
```
<!--SR:!2023-05-24,8,250-->

Write a for loop in javascript?
?
```javascript
for (var i = 0; i < 5; i++){
	console.log(i)
};
```
<!--SR:!2023-05-23,7,250-->

Write a do while loop in javascript?
?
```javascript
do {
	//thing to do
} while(condition);
```
<!--SR:!2023-05-22,6,250-->

Convert an integer to string in Javascript?
?
```javascript
console.log(parseInt('2')) ;
```
<!--SR:!2023-05-19,2,230-->

Use the ternary if-else operator in javascript?
?
```javascript
a > b ? console.log("a is bigger") : console.log("b is bigger");
```
<!--SR:!2023-05-26,10,250-->

Which keyword does not allow a variable to be redeclared?
?
The `let` and `const` keywords. `const` also doesn't allow reassignment.
<!--SR:!2023-05-25,9,250-->

Write a javascript date object for today?
?
```javascript
const date = new Date('2023-10-1');
```
<!--SR:!2023-05-21,4,249-->


What value is stored in x in javascript?

```javascript
let x = 16 + 4 + "Volvo";
```
?
```
20Volvo
```
<!--SR:!2023-05-23,5,249-->

