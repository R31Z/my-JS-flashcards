# JavaScript Questions and Answers.

## 1. What happens when you don’t declare a variable in Javascript?

If you don’t explicitly declare a variable, you risk creating an implied global variable. This is a problem, as you will be unable to create multiple instances of that object, as each new instance will overwrite the data from the last.
In general, global variables should be used only in very specific situations and are typically not recommended, as they can lead to a lot of odd side effects that may be difficult to track down.

## 2. What will the code below output? Explain your answer.

    console.log(0.1 + 0.2); 

    console.log(0.1 + 0.2 == 0.3);
  
An educated answer to this question would simply be: “You can’t be sure. it might print out “0.3” and “true”, or it might not. 
Numbers in JavaScript are all treated with floating point precision, and as such, may not always yield the expected results.” 
The example provided above is classic case that demonstrates this issue. 

Surprisingly, it will print out:

    0.30000000000000004 false

## 3. Write a simple function (less than 80 characters) that returns a boolean indicating whether or not a string is a palindrome.

The following one line function will return true if str is a palindrome; otherwise, it returns false.

      function isPalindrome(str) {
      str = str.replace(/\W/g, '').toLowerCase();
      return (str == str.split('').reverse().join(''));
      }
  
For example:

      console.log(isPalindrome("level")); // logs 'true'
      console.log(isPalindrome("levels")); // logs 'false'
      console.log(isPalindrome("A car, a man, a maraca")); // logs 'true'
    
## 4.a

    (function(){
        return typeof arguments;
    })();
    
Answer a: 
The answer is "object"; the arguments object accessible in a function is, well, an object. 
There are two things to watch out for here:
Arguments is not an array. It is an array-like object. 
You can thus access its elements with square brackets and integer indices, 
but methods usually available on an array such as push do not exist on arguments.

Even if arguments were a true array, the answer would still be "object". 
The typeof operator returns "object" when given an array, because arrays are objects too.
      
## 4.b

    var f = function g(){ return 44; };
    typeof g(); 
            
Answer b:
The answer is that an error will occur.
This is because function g(){ return 44; } is a function expression (a named one, in fact), not a function declaration.      The function is actually bound to the variable f, not g. 

Specifying an identifier in a function expression does have its use though: stack traces are clearer instead of being        littered with nameless functions, and you can have an anonymous function recursively call itself without using     
arguments.callee. kangax has a very detailed post on function expressions.
            
 ## 5. What would be the result? 3+2+"7"
      
  Answer: 
  
      Since 3 and 2 are integers, they will be added numerically. 
      And since 7 is a string, its concatenation will be done. So the result would be 57.
      
## 6. In what order will the numbers 1-4 be logged to the console when the code below is executed? Why?
(function() {
console.log(1); 
setTimeout(function(){console.log(2)}, 1000); 
setTimeout(function(){console.log(3)}, 0); 
console.log(4);
})();

Answer: The values will be logged in the following order:
    
    1 4 3 2 

Let’s first explain the parts of this that are presumably more obvious:
1 and 4 are displayed first since they are logged by simple calls to console.log() without any delay
2 is displayed after 3 because 2 is being logged after a delay of 1000 msecs (i.e., 1 second) whereas 3 is being logged after a delay of 0 msecs.

OK, fine. But if 3 is being logged after a delay of 0 msecs, doesn’t that mean that it is being logged right away? And, if so, shouldn’t it be logged before 4, since 4 is being logged by a later line of code?

The answer has to do with properly understanding JavaScript events and timing.

The browser has an event loop which checks the event queue and processes pending events. For example, if an event happens in the background (e.g., a script onload event) while the browser is busy (e.g., processing an onclick), the event gets appended to the queue. When the onclick handler is complete, the queue is checked and the event is then handled (e.g., the onload script is executed). Similarly, setTimeout() also puts execution of its referenced function into the event queue if the browser is busy.

When a value of zero is passed as the second argument to setTimeout(), it attempts to execute the specified function “as soon as possible”. Specifically, execution of the function is placed on the event queue to occur on the next timer tick. Note, though, that this is notimmediate; the function is not executed until the next tick. That’s why in the above example, the call to console.log(4) occurs before the call to console.log(3) (since the call to console.log(3) is invoked via setTimeout, so it is slightly delayed). 

## 7. What is the output of "10"+20+30?
102030 because after a string all the + will be treated as string concatenation operator (not binary +).

## 8 Difference between Client side JavaScript and Server side JavaScript?
Client side JavaScript comprises the basic language and predefined objects which are relevant to running java script in a browser. The client side JavaScript is embedded directly by in the HTML pages. This script is interpreted by the browser at run time.

Server side JavaScript also resembles like client side java script. It has relevant java script which is to run in a server. The server side JavaScript are deployed only after compilation.

## 9. What are the advantages of using JavaScript?

Lightweight: 
JavaScript can be executed within the user’s browser without having to communicate with the server, saving on bandwidth.

Versatile: 
JavaScript supports multiple programming paradigms—object-oriented, imperative, and functional programming and can be used on both front-end and server-side technologies.

Sleek Interactivity: 
Because tasks can be completed within the browser without communicating with the server, JavaScript can create a smooth “desktop-like” experience for the end user.

Rich Interfaces: 
From drag-and-drop blocks to stylized sliders, there are numerous ways that JavaScript can be used to enhance a website’s UI/UX.

Prototypal Inheritance: 
Objects can inherit from other objects, which makes JavaScript so simple, powerful, and great for dynamic applications.

## 10. What are the disadvantages of using JavaScript?

Experienced coders won’t just be able to rave about their favorite language’s strengths—they will also be able to talk about its weaknesses. JavaScript’s main weakness is security. Look for answers on how it can be exploited. A secondary weakness is JavaScript’s ubiquity and versatility—it can be a double-edged sword in that there’s a lot of room for programming quirks that can lead to inconsistent performance across different platforms.

## 11. What’s An Object In JavaScrpt And How Do We Create Them?

A JavaScript object is an entity having state and behavior (properties and method). Since JavaScript is an object-based language, it treats everything as an object.

JavaScript is a template-based language not class based. It supports to create the object directly, there is no need to define a class for this.

JavaScript supports following three ways to create objects.

### 1. By Object Literal.

The syntax of creating an object using object literal is as follows.
           
    object={property1:value1, property2:value2.....propertyN:valueN}
    
Here, property and value are separated by “:”.

Let’s take an example of creating an object using object literal technique.

    <script> 

    std={id:1114, name:"Albert Einstein", subject:"Physics"} 

    document.write(std.id+" "+std.name+" "+std.subject); 

    </script> 
    
### 2. By Creating An Instance Of The Object (Using New Keyword).

The syntax of creating an object directly is as follows.
     
    var objectname=new Object();
    
Here, the new keyword is used to create the object.
Let’s take an example of creating an object directly.
   
    <script> 

    var std=new Object(); 

    std.id=1114; 

    std.name="Albert Einstein"; 

    std.subject="Physics"; 

    document.write(std.id+" "+std.name+" "+std.subject); 

    </script>

### 3. By Using An Object Constructor.

In this method, we create a function with arguments. The value of each of these arguments can be assigned to the current object by using this keyword.

This keyword refers to the current object.
Let’s take an example of creating an object using object constructor technique.

    <script> 

    function std(id,name,subject){ 

    this.id=id; 

    this.name=name; 

    this.subject=subject; 

    } 

    s=new std(1114,"Albert Einstein","Physics"); 

    document.write(s.id+" "+s.name+" "+s.subject); 

    </script>
  
## 12. What Is Scope In JavaScript?

The scope determines the accessibility of variables, objects, and functions in particular part of your code.

In JavaScript, the scope is of two types.

### 1. Global Scope.

A variable defined outside a function comes under the Global scope. Variables defined inside the Global scope are accessible from any part of the code. Let’s see an example.
        
        var name = 'TechBeamers';

        console.log(name); // logs 'TechBeamers'

        function logName() {

        console.log(name); // 'name' is accessible here and everywhere else

        }

        logName(); // logs 'TechBeamers'
        
### 2. Local Scope.

Variables defined inside a function comes under the Local scope. Different functions can use a variable with the same name. It is because these variables are strictly bound to the function that defines it (each having different scopes) and is not accessible in other functions. Let’s see an example.

    // Global Scope

    function sampleFunction() {

        // Local Scope #1

        function sample2Function() {

            // Local Scope #2

        }
    }

    // Global Scope

    function sample3Function() {

        // Local Scope #3

    }

    // Global Scope
## 13. What Is <This> In JavaScript?

All the prime languages use ‘this’ keyword to refer to an object that is currently instantiated by the class. However, in JavaScript, ‘this’ refers to an object which ‘owns’ the method. Though this varies, with how a function call happens.

Global Scope.

If no object is currently available, then ‘this’ represents the global object. In a web browser, ‘window’ is the top-level object which represents the document, location, history and a few other useful properties and methods. Let’s take a sample code.

    window.Obj= "I represent the window object";

    alert(window.Obj);

    alert(this.Obj); // I'm the window object

    alert(window === this); // true
    
 ### The Scenario Of A Function Call.

In the case of a function call, ‘this’ refers to the global object.

    window.Obj = "I represent the window object";

    function TestFunction() {

        alert(this.Obj); // I'm the window object

        alert(window === this); // true

    }

    TestFunction();
    
### Call Object Methods.

When an object constructor or any of its methods gets called, ‘this’ refers to an instance of an object. It is similar to any class-based language.

    window.Obj = "I'm the window object";

    function TestFunction() {

        this.Obj = "I'm the Test object";

        this.Verify1 = function() {

            alert(this.Obj); // I'm the Test object

        };

    }

    TestFunction.prototype.Verify2 = function() {

        alert(this.Obj); // I'm the Test object

    };

    var tf= new TestFunction();

    tf.Verify1();

    tf.Verify2();
    
## 14. What Is Prototype Property In JavaScript?

Every JavaScript function has a prototype property (by default this property is null), that is mainly used for implementing inheritance. We add methods and properties to a function’s prototype so that it becomes available to instances of that function. Let’s take an example that calculates the perimeter of a rectangle.

    function Rectangle(x, y) {

        this.x = x;

        this.y = y;

    }

    Rectangle.prototype.perimeter = function() {

       return 2 * (this.x + this.y);

    }

    var rect = new Rectangle(4, 2);

    console.log(rect.perimeter()); // outputs '12'
    
## 15. What Is Closure In JavaScript?

A closure is a JavaScript function defined inside another function. And that’s why it gets a special privilege to access three types of scope which are as follows.

- Internal Scope i.e. the variables defined between its curly brackets.
- Outer Function Scope i.e. the variables of the enclosing function.
- Global Scope i.e. variables defined as globals.

Please note that a closure can not only access the outer function variables but also see its parameters. But it can’t call the outer function’s arguments object. However, it can directly call the outer function’s parameters.

Here is a code example describing closure by adding a function inside another function.

    function outerFunc(arg1, arg2) {
    var param = "I'm closure. ";

    // Inner function accessing outer function variables and parameters
    function innerFunc() { 
     return arg1 + arg2 + " " + param;
    }
        return innerFunc();
    }

    outerFunc("arg1", "arg2");
## 16. What Is Prototypal Inheritance In JavaScript?

Most of the Object Oriented languages support classes and objects. Here, Classes inherit from other classes.

In JavaScript, the inheritance is prototype-based. This means that there are no classes. Instead, there is an object that inherits from another object.

JavaScript provides three different types of Prototypal Inheritance.

### 1. Delegation (I.E. The Prototype Chain).

A delegate prototype is an object that serves as a base for another object. When you inherit from a delegate prototype, the new object gets a reference to the prototype.

When we try to access any property, it first checks in the properties owned by the object. If that property does not exist there, it checks in the ‘[[Prototype]]’ and so on. If that property does not exist there, it checks in the ‘[[Prototype]]’ and so on. Gradually, it moves up the prototype chain, until it reaches the <Object.prototype> i.e. the root delegate for most of the objects.

### 2. Concatenative Inheritance (I.E. Mixins, Object.Assign()).

It is the process of inheriting the features of one object to another by copying the source objects properties. JavaScript calls these source prototypes by the name mixins. This process makes use of the JavaScript method Object.assign(). However, before ES6, the <.extend()> method was used.

### 3. Functional (Not To Be Confused With Functional Programming).

In JavaScript, a function can create an object. It’s not necessary to be a constructor(or a class). It is called a factory function. Functional inheritance produces an object from a factory and also extends it, by assigning properties.

Every type of Prototypal Inheritance supports a separate set of use-cases, applicable to it. All of them are equally useful in their ability to enable composition. It provides has-a, uses-a, or can-do relationship as compared to the is-a relationship created with class inheritance.

## 17. Why Is “Self” Needed Instead Of “This” In JavaScript?

Inner functions in JavaScript have access to all of the variables defined in the outer function. However, “this” variable is an exception. Since the nested function is just a regular function and not an object method, it’s “this” refers to the global namespace. To make it more clear, let’s look at the following example.

    var aProperty = 'global';

    var myObject = {

      outerFun: function() {

        this.aProperty = 'local';

        setTimeout(function() {

          console.log(this.aProperty); // outputs 'global'

        }, 1);

      }

    };
    
Thus, we see that inside “setTimeout” function, “this” refers to the global object. We need a way to get a reference to the object, that is available inside the nested function. We assign the object from “this”, to another(non-special) variable, “self”. It is not a special variable and hence cannot be overwritten by other functions(like “this”). Thus on using “self” inside the inner function, we can refer to the local object. Following is the sample code.

    var myObject = {

      outerFun: function() {

        var self = this;

        this.aProperty = 'local';

        setTimeout(function() {

          console.log(self.aProperty); // outputs 'local'

        }, 1);

      }

    };

## 18. What Is An Anonymous Function And When Should You Use It?

Anonymous functions are functions that are dynamically declared at runtime. They’re called anonymous functions because they don’t have a name like normal functions.

We use function operator to declare an anonymous function, instead of the function declaration. Also, function operator can be used to create a new function, wherever it’s valid to put an expression. For example, we declare a new function to be supplied as an argument to a function call or to assign a property of another object.

Here’s a typical example of a named function.

    function testFunction()
    {

       alert("Welcome!!");
    }

    testFunction();
    
Here’s the same example created as an anonymous function.

    var testFunction= function()
    {

      alert("Zoom! Zoom! Zoom!");
    }

    flyToTheMoon();

Following are the key usage of anonymous functions.

Code brevity.
  Use them in
    Callbacks, and
    Event handlers.
Scope management.
  They are useful in the following scenario.
    To create temporary/private scope.
    In Closures and Recursions.
## 19. What Is The Difference Between “==” And “===”?

These are the operators provided by JavaScript – strict equality and Type converting equality.

Strict equality (===) returns true if the values which it is going to compare have the same data type. Taking an example, “2” will not be equal to 2  i.e. (“2″===2) will return false.

Secondly, Type converting equality (==), automatically converts the variable to value irrespective of the data type. Taking an example, here “2” will be equal to 2  i.e. (“2″===2) will return true.

Summarizing it, double equal (==) is an autotype converting equality operator while three equals (===) is a strict equality operator, i.e. it will not convert values automatically.

## 20. What are the Values and Types in JavaScript?

As we asserted in Chapter 1, JavaScript has typed values, not typed variables. The following built-in types are available:

string
number
boolean
null and undefined
object
symbol (new to ES6)

JavaScript provides a typeof operator that can examine a value and tell you what type it is:

var a;
typeof a;				// "undefined"

a = "hello world";
typeof a;				// "string"

a = 42;
typeof a;				// "number"

a = true;
typeof a;				// "boolean"

a = null;
typeof a;				// "object" -- weird, bug

a = undefined;
typeof a;				// "undefined"

a = { b: "c" };
typeof a;				// "object"
The return value from the typeof operator is always one of six (seven as of ES6! - the "symbol" type) string values. That is, typeof "abc" returns "string", not string.

Notice how in this snippet the a variable holds every different type of value, and that despite appearances, typeof a is not asking for the "type of a", but rather for the "type of the value currently in a." Only values have types in JavaScript; variables are just simple containers for those values.

typeof null is an interesting case, because it errantly returns "object", when you'd expect it to return "null".

Warning: This is a long-standing bug in JS, but one that is likely never going to be fixed. Too much code on the Web relies on the bug and thus fixing it would cause a lot more bugs!

Also, note a = undefined. We're explicitly setting a to the undefined value, but that is behaviorally no different from a variable that has no value set yet, like with the var a; line at the top of the snippet. A variable can get to this "undefined" value state in several different ways, including functions that return no values and usage of the void operator.

## 21. What Are The Different Ways To Create An Array In JavaScript?

There are two main ways to create an array in JavaScript.

### 1. Using An Array Initializer (Array Literal).

The array initializer (array literal) syntax is simple. It is a comma-separated list of values in square brackets.

Let’s see some examples.

    var myArray1 = [1,2,3,4,5]      // an array with 5 elements
    var myArray2 = [5]              // an array with 1 element
    var myArray3 = [true,'Hi',[7]]  // element types need not be the same.

### 2. Using The Array Constructor.

The Array constructor method has three different syntaxes. If we call the constructor with two or more arguments, it declares an array with array elements also initialized. If we provide only one argument to the Array constructor, it refers to the length of the new array with, elements not initialized. Lastly, the constructor without any argument creates an array with its length set to zero with elements not initialized.

Let’s see some examples.

    var myArray4 = new Array(1,2,3,4,5)  // an array with 5 elements
    var myArray5 = new Array(20)        // an empty array of length 20
    var myArray6 = new Array()           // an empty array of length 0
    
## 22. Enumerate the differences between Java and JavaScript?
Java is a complete programming language. In contrast, JavaScript is a coded program that can be introduced to HTML pages. These two languages are not at all inter-dependent and are designed for the different intent.  Java is an object – oriented programming (OOPS) or structured programming language like C++ or C whereas JavaScript is a client-side scripting language and it is said to be unstructured programming.

## 23. What is negative infinity?
Negative Infinity is a number in JavaScript which can be derived by dividing negative number by zero.

## 24. What Are The Different Objects Used In JavaScript?
JavaScript uses a hierarchical structure, applicable to all the objects created in a document. Following are the objects, used in JavaScript that shows the relationship of one object to another.
### Window Object.
It is the topmost object in the hierarchy. It refers to the content area of the browser window that consists of HTML documents. Each frame is also a window that has some actions inside it.
### Document Object.
A Document object represents the HTML document that the window will display. It has various properties that refer to other objects, which allow access to and modification of content in the document.
### Form Object.
A form object is used to take user data as input for processing. It corresponds to an HTML input form constructed with the <FORM>…</FORM> tag.
## 25. What Is Strict Mode In JavaScript?
Strict Mode imposes a layer of constraint on JavaScript. It provides following enhancements.
<ul>
    <li>JavaScript will throw an error if we try to use the elements of a deprecated language.</li>
    <li>To use a variable, it has become mandatory to declare it.</li>
    <li>It disallows duplicate property and parameter names.</li>
    <li>The eval() method is safer to use, but still considered evil in some cases.</li>
    <li>It deprecates the “with” statement.</li>
    <li>JavaScript will throw an error if we try to assign a value to a read-only property.</li>
    <li>It decreases the global namespace pollution.</li>
  </ul>
To enable strict mode, we have to add, “use strict” directive to the code. The physical location of the “strict” directive determines its scope. If used at the beginning of the js file, its scope is global. However, if we declare strict mode at the first line in the function block, its scope restricts to that function only.

## 26. What Are Event Handlers In JavaScript And How To Use Them?
JavaScript event handlers are functions that bind to a specific HTML DOM event. And events are the part of HTML document object model (DOM). An event can take place in one of the following cases.

Due to user actions on a web page.
    
    <onclick()>, <onmouseover()>, <onkeydown()>
    
Whenever the DOM receives an event, it calls the JavaScript event handler function bind to the event. To use a handler function, we can assign it to the desired event as an attribute of the target HTML element. Please follow the below example.

    <HTML>
 
    <BODY>

    <FORM>

    <INPUT TYPE=”button” VALUE=”Test” onClick=”window.alert ('Event Handler')”>

    </FORM>

    </BODY>

    </HTML>
## 27. What Does A JavaScript Function Result When It Has No Return Statement?
If a function doesn’t use the return statement, then it returns undefined as the return value.
However, the browser won’t print anything in its console as it ignores if the expression returns an undefined value. But if we explicitly call such a function inside the console.log() method, then it’ll print exact value.
     
    function test(){}
 
    console.log(test()); // will print 'undefined'
## 28. What Is EncodeURI() Function?
The encodeURI() function is used to encode a URI. This function encodes all special characters, except these < , / ? : @ & = + $ #>.
Let’s See An Example.

    var uri="http://www.techbeamers.com/how to make a website using javaScript";
    var encodedURI = encodeURI(uri);
    console.log(encodedURI);
    
 Output

     http://www.somedomain.com/how%20to%20make%20a%20website%20using%20javaScript
    
We see that JavaScript encodes the space between the words in the <uri> variable as <%20>. Thus, the encodeURI function is used to encode special reserved characters and other non-ASCII characters in the URI.
    
## 29. How Does The <Array()> Differ From <[]> While Creating A JavaScript Array?
Both the <Array()> and <[]> works almost the same in JavaScript.

If we use them as is (i.e. without any argument) to create an array object, then they will result in an array object of zero length. Also, if we pass a string or a list of strings as arguments, even then result will be similar.

However, they differ when the input argument is of integer type. In that case, the <Array(n)> statement will create an uninitialized array of size of n. Whereas, the <[n]> statement will create an array of size <1> and assign <n> as value to the first element.

## 30. What will the code below output to the console and why?

    (function(){
       var a = b = 3;
    })();

    console.log("a defined? " + (typeof a !== 'undefined'));
    console.log("b defined? " + (typeof b !== 'undefined'));
    
Since both a and b are defined within the enclosing scope of the function, and since the line they are on begins with the var keyword, most JavaScript developers would expect typeof a and typeof b to both be undefined in the above example.

However, that is not the case. The issue here is that most developers incorrectly understand the statement var a = b = 3; to be shorthand for:

    var b = 3;
    var a = b;
    
But in fact, var a = b = 3; is actually shorthand for:

    b = 3;
    var a = b;
    
As a result (if you are not using strict mode), the output of the code snippet would be:

    a defined? false
    b defined? true

But how can b be defined outside of the scope of the enclosing function? Well, since the statement var a = b = 3; is shorthand for the statements b = 3; and var a = b;, b ends up being a global variable (since it is not preceded by the var keyword) and is therefore still in scope even outside of the enclosing function.

Note that, in strict mode (i.e., with use strict), the statement var a = b = 3; will generate a runtime error of ReferenceError: b is not defined, thereby avoiding any headfakes/bugs that might othewise result. (Yet another prime example of why you should use use strict as a matter of course in your code!)

## 31. What are different types of error in JavaScript?

Syntax Error: – Syntax Errors are those errors which occur when you break the rules defined in JavaScript while creating a program. This error occurs while loading a web page.

Runtime Error: – Runtime error informs the programmer that there is a problem with a script while loading. You can see runtime errors in a browser. It specifies the line number in the alert box so that you can easily search that error in Script. Due to the use of improper command the runtime error occurs. 

Logical Error: – Logical Error is the type e of error in which you don’t get an expected result as required. This error is also known as a bug.

## 32. How Does Variable Hoisting Take Place In JavaScript?
In JavaScript, variable declarations are the first piece of code that executes irrespective of their location. Hence, it doesn’t matter whether we declare a variable at the top or anywhere else. This functionality which moves the declaration to the top either inside a function or in the global code is known as hoisting.

    out = 2;
 
    var out;
 
    function myfunc() {
 
      var in = "inside"
 
    // some code
 
    }
 
    // ...
    
JavaScript will interpret the above in the following manner.

    var out;
 
    out = 2;
 
    function myfunc() {
 
        var in;
 
    // some code
 
      in = "inside";
 
    }
## 33. How Will You Replace All Occurrences Of A String In JavaScript?
We can use String’s <replace()> method to substitute any string. There are following two ways to use this method.
Pass The Input String As A Regular Expression.

    str = "ghktestlllltest-sdds"
    str = str.replace(/test/g, '');
    alert(str)
    
### Use RegExp Class To Create A Regular Expression And Pass It.

    String.prototype.replaceAll = function(find, replace) {

        var target = this;

        return target.replace(new RegExp(find, 'g'), replace);

    };

    str = "ghktestlllltest-sdds"

    str = str.replaceAll('test', '');

    alert(str)
## 34. What is arguments object in JavaScript?
JavaScript variable arguments represents the arguments passed to a function.
## 35.  Is it possible to break JavaScript Code into several lines?
Breaking within a string statement can be done by the use of a backslash, ‘\’, at the end of the first line

Example:

    document.write("This is \a program");
## 36.  What are undeclared and undefined variables?
Undeclared variables are those that do not exist in a program and are not declared. If the program tries to read the value of an undeclared variable, then a runtime error is encountered.

Undefined variables are those that are declared in the program but have not been given any value. If the program tries to read the value of an undefined variable, an undefined value is returned.
## 37. What is a prompt box?
A prompt box is a box which allows the user to enter input by providing a text box.  Label and box will be provided to enter the text or number.
## 38. What will the following code output to the console:
console.log((function f(n){return ((n > 1) ? n * f(n-1) : n)})(10));

The code will output the value of 10 factorial (i.e., 10!, or 3,628,800).

Here’s why:

The named function f() calls itself recursively, until it gets down to calling f(1) which simply returns 1. Here, therefore, is what this does:

    f(1): returns n, which is 1
    f(2): returns 2 * f(1), which is 2
    f(3): returns 3 * f(2), which is 6
    f(4): returns 4 * f(3), which is 24
    f(5): returns 5 * f(4), which is 120
    f(6): returns 6 * f(5), which is 720
    f(7): returns 7 * f(6), which is 5040
    f(8): returns 8 * f(7), which is 40320
    f(9): returns 9 * f(8), which is 362880
    f(10): returns 10 * f(9), which is 3628800
## 39. Which keyword is used to print the text in the screen?
document.write(“Welcome”) is used to print the text – Welcome in the screen.
## 40. What is ‘this’ keyword in JavaScript?
‘This’ keyword refers to the object from where it was called.
## 41. How many types of functions JavaScript supports?
A function in JavaScript can be either named or anonymous.
## 42. Which built-in method returns the character at the specified index?
charAt() method returns the character at the specified index.
## 43. Which built-in method combines the text of two strings and returns a new string?
concat() method returns the character at the specified index.
## 44. Which built-in method calls a function for each element in the array?
forEach() method calls a function for each element in the array.
## 45. Which built-in method returns the index within the calling String object of the first occurrence of the specified value?
indexOf() method returns the index within the calling String object of the first occurrence of the specified value, or −1 if not found.
## 46. Which built-in method returns the length of the string?
length() method returns the length of the string.
## 47. Which built-in method removes the last element from an array and returns that element?
pop() method removes the last element from an array and returns that element.
## 48. What is Date object in JavaScript?
The Date object is a datatype built into the JavaScript language. Date objects are created with the new Date( ).

Once a Date object is created, a number of methods allow you to operate on it. Most methods simply allow you to get and set the year, month, day, hour, minute, second, and millisecond fields of the object, using either local time or UTC (universal, or GMT) time.
## 49. What Is An Asynchronous Programming? Why Is It Important In JavaScript?
In Asynchronous programming, the engine runs in an event loop. On encountering a blocking operation, a request gets fired and the code keeps running without blocking for the result. When its execution completes, and the response is ready, it fires an interrupt, which causes an event handler to be run, where the control flow continues. In this way, a single program thread can handle many concurrent operations in an asynchronous programming.

The user interface is asynchronous by nature and spends most of the time, waiting for user input to interrupt the event loop and trigger event handlers. Node is asynchronous by default. It means that the server works by waiting for a network request in a loop. Thus, it accepts more incoming requests, while the first one is getting handled.

It is important in JavaScript because it’s suitable for user interface code and beneficial for maintaining the performance on the server.
## 50. Assuming d is an “empty” object in scope, what is accomplished using the following code?
    
    [ 'zebra', 'horse' ].forEach(function(k) {
	d[k] = undefined;
    });
## 51. What will be the output of the code below?

	var y = 1;
	  if (function f(){}) {
	    y += typeof f;
	  }
	  console.log(y);
The output would be 1undefined. The if condition statement evaluates using eval, so eval(function f(){}) returns function f(){} (which is true). Therefore, inside the if statement, executing typeof f returns undefined because the if statement code executes at run time, and the statement inside the if condition is evaluated during run time.

	var k = 1;
	  if (1) {
	    eval(function foo(){});
	    k += typeof foo;
	  }
	  console.log(k); 
The code above will also output 1undefined.

	var k = 1;
	  if (1) {
	    function foo(){};
	    k += typeof foo;
	  }
	  console.log(k); // output 1function
## 52. Truthy isn't Equal to true
Question: As [] is true, []==true should also be true. right?

Answer: You are right about first part, [], empty array is an object and object is always truthy. Hence, if you use if([]){console.log('its true')} you will see the log.

However, special case about == (double equal) is that it will do some implicit coercion.

Since left and right side of the equality are two different types, JavaScript can't compare them directly . Hence, under the hood, JavaScript will convert them to compare. first right side of the equality will be cooereced to a number and number of true would be 1.

After that, JavaScript implementation will try to convert [] by usingtoPrimitive (of JavaScript implementation). since [].valueOf is not primitive will use toString and will get ""

Now you are comparing "" == 1 and still left and right is not same type. Hence left side will be converted again to a number and empty string will be 0.

Finally, they are of same type, you are comparing 0 === 1 which will be false.
## 53. How can you get the total number of arguments passed to a function?
Using arguments.length property, we can get the total number of arguments passed to a function. For example:

	function func(x){
	   console.log(typeof x, arguments.length);
	}
	func();                //==> "undefined", 0
	func(1);               //==> "number", 1
	func("1", "2", "3");   //==> "string", 3
	
## 54. window vs document
Question: Is there any difference between window and document?

Answer: Yes. JavaScript has a global object and everything runs under it. window is that global object that holds global variables, global functions, location, history everything is under it. Besides, setTimeout, ajax call (XMLHttpRequest), console or localStorage are part of window.

document is also under window. document is a property of the window object. document represents the DOM and DOM is the object oriented representation of the html markup you have written. All the nodes are part of document. Hence you can use getElementById or addEventListener on document. These methods are not present in the window object.

	window.document === document; //true
	window.getElementById; //undefined
	document.getElementById; //function getElementById() { [native code] }
      
## 55. What would following code return?

console.log(typeof typeof 1);

Answer: string

	typeof 1 will return "number" and typeof "number" will return string.

## 56. What are different types of Popup boxes available in Javascript?

In Javascript there are 3 types of Popup Boxes are available, they are

	1. Alert
	2. Confirm
	3. Prompt
