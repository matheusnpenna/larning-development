# Course Deep Javascript Foundations from Frontend Masters

````
The most reason of bug appear in projects is the difference between the developer 
think the code will do and what the computer really do. 
````
# This is my notations

# Intro Example: What gonna really do the ++ operator
````
    - this:
        let x = "5";
        ++x;
    - is the same of: 
        let x = "5";
        x = parseInt(x);
        x = x + 1; or 
    - this:
        let x = "5";
        x++;
    - is the same of: 
        let x = "5";
        function afterPlusPlus (val) {
            let old_value = Number(val);
            x = old_value + 1;
            return old_value;
        }
        afterPlusPlus();
````
# Javascript is based inside 3 cores, or 3 pilares
````
    - Types
        - Primitive types
        - Abstract Operations
        - Coercion
        - Equality
        - Typescript, Flow, etc.
    - Scope
        - Nested Scope
        - Hoisting
        - Closure
        - Modules
    - Objects (Oriented)
        - this
        - class {}
        - Prototypes
        - OO vs OLOO
````
# Primitive Types
````
     - Primitive types: "In Javascript, everything is an object" -> This sentence is FALSE!
     - Haha for example, "false" isn't an object rsrs
     - Some values in Javascript can behave as objects, but that does not make them objects
     - ECMScript value primitive types are: 
        - Undefined, Null, Boolean, String, Symbol, Number and Objects.
     - ECMAScript other values that may behave like types
        - undeclared (Values that not been declared yet)
        - Null (Spec of JS call as a type, but null is a not válid value)
        - function (Spec refers as a subtype of Object type, too named as callable Object)
        - Arrays (Have especific behaviors but like a function, not is a type, is a subtype of Object)
        - Bigint (Or Large integer, is a new feature in three stage but isn't in spec yet[Mar, 2021])
    - But what types is really objects?
        - Objects:
            - Object
            - function
            - array
        - Not Obejects:
            - undefined
            - string
            - number
            - boolean
            - symbol
            - null
            - bigint
    - In Javascript, variables don't have types. It is the values themselves that have types.
````
# Typeof Operator
````
    - If an variable is declared without initiated yet, they have a undefined value. The correct thought about the undefined type is, undefined is a value that not was been initiated ou attributed yet
    - The typeof operator is guaranteed the aways only return string.
    - If I make this, I will have these returns;
        var x = null;
        typeof x; // "object"
        x = function();
        typeof x; // "function"
        x = [1,2,3];
        typeof x; // "object"
        
````
# undefined vs undeclared vs unitialized (aka TDZ)
````
    - typeof operator not catch the undeclared type, because the type of can be referenced to a variable that not be declared yet and not throw an error, will considerate value as undefined;
````


# Nan & isNaN
````
    - NaN is a especial value created to indicated invalid number, resulted of 
    - An test to guarantee that number is valid is:
        Number.isNaN(x) // true or false
````

# Negative 0
````
    - Negative 0 doesn't exist in real world, but exist in programming and if I make:
        var v = -0;
        v === 0; // result is true
        but
        v === -0; // result is true
    - The best way to check if is an negative 0 is use Object.is like:
        var v = -0;
        Object.is(v, 0); // result false
        Object.is(v, -0); // result true
````

