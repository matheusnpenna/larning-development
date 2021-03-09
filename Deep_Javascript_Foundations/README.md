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
# Types
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
````