/******************************************************************************************* *                                         TYPES                                           * *******************************************************************************************/
//strings
let firstTime: String = "Hello world"
//ints & Doubles
let minValue: Int = -42
var temporary: Double = 55.89
//BOOLEANS
let swiftBool: Bool = true

//string interpolation to print
let name: String = "Turi"
print("Hello \(name)!")

//using string interpolation to combine strings
let hello: String = "Hello,"
var greeting: String = "\(hello) \(name)."
print("\(greeting)")

//using string concatenation
let question: String = "How are you?"
print("\(greeting) \(question)")


/******************************************************************************************* *                                       COLLECTIONS                                       * *******************************************************************************************/
//ARRAYS - all values must be of same type
var prevBillAmounts: [Double] = [10.2,21.35,15.54]
//we use var for arrays when we want to append to change value within. ALso notice how the type is between brackets.

//ARRAY OPERATIONS
prevBillAmounts.append(52.45)
let count: Int = prevBillAmounts.count
let first: Double = prevBillAmounts[0]

//DICTIONARIES 
//Key type: Value type
var people: [String: Int] = [
                        "Bob": 32,
                        "Cindy": 25
                            ]
//look up
//notice ~ we don't actually need to type cast if were cathing avalue from an already initialized variable
//- so for the prev array operations we didnt actually have to declare the types
let bobsAge = people["Bob"]
//adding key value pairs
people["Dan"] = 56


/******************************************************************************************* *                                       Optionals ?? !!                                   * *******************************************************************************************/

/* Optionals are Schrodingers Variable 
   - Placing a ? after varible to make varible optional which allows the variable to live in one of two states:
 1. There is a value and it equals x
 2. There isn't a value at all*/
let input: String = "123"
let optionalConvertedInput: Int? = Int(input)

//Conversion succeeds so optional converted is a value
let input2: String = "123abc"
let optionalConvertedInput2: Int? = Int(input2)
//conversion fails isnce input isnt fully an int. NO optionalConvertedInput exists

//HOW DO WE USE OPTIONALS??   
//Since these variables can either exist or not we hace to first check that they are not nil before using them

if let convertedInput = optionalConvertedInput{
    print("\(convertedInput)")
}else {
    let convertedInput: Any = input
}

//   OPTIONALS IN STRING INTERPOLATION    
// when we print optionals 
let maybeString: String? = "value"
print("\(maybeString)") //leaves optional wrapper 
print("\(maybeString!)") //unwraps value and prints "value"
print("\(optionalConvertedInput2)") //prints nill since constant doesnt exist

/******************************************************************************************* *                                      Functions                                          * *******************************************************************************************/
// All parameters need a name and type. Functions indicate the return type following "->"
func sayHello(personName: String) -> String {
    //    implicitly returns when there is single statement
    "Hello \(personName)!"
}
//Swift functions can't just take in values. We need to indicate what local parameter the value belongs to.
greeting = sayHello(personName: "Bob")
print("\(greeting)")

/****** EXTERNAL VS LOCAL PARAMETERS ******
    When calling a function swift does not use positional arguments but instead uses labels.
    this is where external and local parameters come into play. The local parameter is the internal name of the variable/constant used in the function. The external name is the label associated with the local parameter that we assign to each passed value when calling the function
    - EXTERNAL: parameter name used to label arguments passed to function call
    - LOCAL: name used in implementation of the function */
//      External  Local    External  Local
//            ^     ^            ^    ^
func sayHello(p1 person: String, p2 anotherPerson: String) -> String {
    "Hello \(person) and \(anotherPerson)!"
}
greeting = sayHello(p1: "EG", p2: "Juan")
print("\(greeting)")


/******************************************************************************************** *                                    CONTROL FLOW                                          *
 ********************************************************************************************/
// IF STATEMENT
// if statements in swift are just like they are in c
let temp: Int = 90
if temp <= 32 {
    print("It's very cold. Consider wearing a scarf")
}else if temp >= 86{
    print("Hot day today. Don't forget to apply sunscreen.")
}else{
    print("It's not that cold. Pants and a tshirt is good")
}

/****** LOOPS ******
     2 types of loops:
 1. for loops: your basic c for loop
 2. for-in loops: python style for loop */
for num in 0..<3{ //0-2 inclusive
    print("\(num)")
}
//we can use the _ placeholder to simply iterate a number of times
for _ in 0..<3{
    print("Hello")
}
let names = ["juan","jorge","joel"]
for (index, value) in names.enumerated() {
    print("Item \(index+1): \(value)")
}

/******************************************************************************************** *                                        CLASSES                                           *
 ********************************************************************************************/
// Classes allow us to define properties and methods which add functionality to ur classes 
// They are called like functions where the parameters are used to initialize the object
class Person {
    //********** DESIGNATED INITIALIZER **********
    // Every class must have at least one designated initalizer. Can have > 1
    // Initializers ensure new instances of a class are correctly initialized before they're used
    // They are like the function decleration of a class. This is how we will create new instances of the class. Passing in parameters
    init(firstName: String, lastName: String){
        //initialize members (created later)
        // SELF - self refers to the current instance. Very meta
        self.firstName = firstName
        self.lastName = lastName
        // Increment type property each time a new person is created
        Person.numberOfPeople+=1
    }
    
    //********** PROPERTIES **********
    //1.  {{{Stored Property}}}
    //    Stored as part of current instance of class. Meaning it there are individual property values belonging to each instance. Hence why we use var as the property changes for each instance.
    var firstName: String
    var lastName: String
    
    //2.  {{{Computed Property}}}
    //    Values derived from other stored values (stored properties)
    //    !!! All computer properties are get-only meaning we can't use "=" we have to use         get{value}
    var fullName: String{
       get{ 
            "\(firstName) \(lastName)"
       }
        //fullName = "\(firstName) \(lastName)" No no
    }
    
    //3.  {{{Type Property}}}
    //    Single instance for all instances of the class. The value is the global to all     instances of same type (in this case Person)
    static var numberOfPeople = 0
    
    //********** METHODS **********
    //    {{{Instance Method}}}
    //    Instance methods are based off a value of the instance. These are called on an instance hence the use of self.
    //    This means you need to create an instance first before calling the instance method
    func greet() {
        print("Hello \(self.firstName)")
        //making the current instance refer to itself using self
    }
    //    {{{Type Method}}}
    //    Type methods are based off of type properties. These are called on objects with a certain type.
    // you can call type methods without instantiatinng first
    class func printNumberOfPeople(){
        print("Number of people = \(Person.numberOfPeople)")
    }
    
    
}

// ...... Using the Person Class ......
//create instance of person class
let jorge = Person(firstName: "Bob", lastName: "Gonzalez")
//call instance method ~ notice how we needed to create instance jorge first
jorge.greet()
//Accesing properties
print("My best friends first name is: \(jorge.firstName)")
print("My best friends full name is: \(jorge.fullName)")
//call type method
//notice we dont need to call it on a specific instance
Person.printNumberOfPeople()



