# Swift Syntax Quick Look Up
# This does not contain answers to coding questions!


# Data Structures

*Important data structures for LeetCode*

//TODO:
- Replace the images with accurate representations of time complexities and stuff for swift foos
- Compare to libraries as im sure some of this can be further simplified through certain libraries
-     - Look into Swift Collections if there a need for BitSet, BitArray, OrderedSet, OrderedDictionary, TreeSet, or TreeDictionary comes up

## CGFloat 
```Swift
Overview of CGFloat
- Definition: CGFloat is a floating-point type used in Apple frameworks like UIKit, AppKit, and CoreGraphics.
- Purpose: It is designed to work efficiently with hardware and graphics APIs, especially when interfacing with CoreGraphics or Quartz 2D.

/*
If you're only working in Swift without Apple-specific frameworks, Double is sufficient.
Modern Apple platforms are mostly 64-bit, so CGFloat is effectively a Double in these cases.
This makes it easier to transition between CGFloat and Double for modern development.
*/

// Instantiating
let myValue: CGFloat = 10.5

let fromDouble = CGFloat(3.14) // From Double
let fromInt = CGFloat(42)     // From Int

let pi: CGFloat = .pi  // Common constant


// Basic Arithmetic:
let width: CGFloat = 100.0
let height: CGFloat = 50.0
let area = width * height

// Drawing in CoreGraphics:
let rect = CGRect(x: CGFloat(10), y: CGFloat(20), width: CGFloat(100), height: CGFloat(50))

// Working with UI Elements:
let view = UIView(frame: CGRect(x: 0, y: 0, width: 200, height: 100))
view.layer.cornerRadius = CGFloat(10.0)

// Trigonometric Calculations:
let angle: CGFloat = .pi / 4
let sinValue = sin(angle)

```

## BinaryInteger (Int, UInt, Int8)
```Swift
// Sugar for i % 2 == 0 for even numbers
i.isMultiple(of: 2)
(x + y).isMultiple(of: 2)
```

## Flow of control
```Swift
// 1. If Statements
let number = 10
if number > 5 {
    print("Number is greater than 5")
} else if number == 5 {
    print("Number is equal to 5")
} else {
    print("Number is less than 5")
}

var tool = true
tool.toggle() //false

// 2. Switch Statements
let grade = "A"
switch grade {
case "A":
    print("Excellent")
case "B", "C":
    print("Good")
case "D":
    print("Pass")
default:
    print("Fail")
}
// Note: Swift's switch statements must be exhaustive or have a default case.

// 3. For Loops
// For loop with a range
for i in 1...5 { // Closed range (includes both ends)
    print(i) // Output: 1, 2, 3, 4, 5
}

//without a closed range
for i in 0..<5 {
    print(i)
}

// Loop through an array
let numbers = [10, 20, 30]
for number in numbers {
    print(number)
}

// besides if true { continue } we can also do this to nicely skip the first part
var thisVar = nums[0] // already setting this up so we can skip the first part
for n in nums.dropFirst() {    
    // do stuff starting on the seconds loop 
}
nums.enumerated().dropFirst() //we can do this if we want enumerated. NOTE: if you put dropFirst().enumerated() aka reverse which goes first, the indexs will be off
array.dropLast() //this is also a thing...

// Using stride to create steps
for i in stride(from: 0, through: 10, by: 2) { // Includes 10
    print(i) // Output: 0, 2, 4, 6, 8, 10
}
//backwards way 1:
for i in stride(from: 10, to: 0, by: -1) {
    print(i) // Prints 10, 9, 8, ..., 1
}
//backwards way 2:
for i in stride(from: 10, through: 1, by: -1) {
    print(i) // Prints 10, 9, 8, ..., 1
}


// 4. While Loops
var count = 0
while count < 5 {
    print(count)
    count += 1
}

// 5. Repeat-While Loop
var x = 0
repeat {
    print(x)
    x += 1
} while x < 5
// Executes the loop body at least once before checking the condition

// 6. Early Exit with guard
func checkAge(age: Int) {
    guard age >= 18 else {
        print("You must be at least 18")
        return
    }
    print("Welcome!")
}
// Use guard to handle conditions that must be true for the code to continue

// 7. Break and Continue
// Break: Exits the loop immediately
for i in 1...5 {
    if i == 3 {
        break // Loop stops at 3
    }
    print(i) // Output: 1, 2
}

// Continue: Skips to the next iteration of the loop
for i in 1...5 {
    if i == 3 {
        continue // Skip 3
    }
    print(i) // Output: 1, 2, 4, 5
}

//enumerate
let fruits = ["Apple", "Banana", "Cherry"]

// Using enumerated() to get both the index and the element
for (index, fruit) in fruits.enumerated() {
    print("Item \(index): \(fruit)")
}
// Output:
// Item 0: Apple
// Item 1: Banana
// Item 2: Cherry

// to avoid forcing the optional
if let matchIndex = tracker[match] {
    return [i, matchIndex]
}

// using zip in a loop
// If s = "abc" and t = "def", then zip(s, t) will create a sequence of tuples: [(a, d), (b, e), (c, f)]
for (c1,c2) in zip(s, t) {
    dict[c1, default: 0] += 1
    dict[c2, default: 0] -= 1
}

// How to use zip to put variables together in array where elements are tuples
positions = [1, 2, 3, 4]
speeds = [10, 20, 30, 40]

# Use zip to combine positions and speeds
position_speed_pairs = list(zip(positions, speeds))

// How to use zip to put variables together in array where elements are tuples (named)
let arrayTup: [(pos: Int, speed: Int)] = zip(positions, speeds).map { (pos: $0, speed: $1) }

// Access elements by name
print(arrayTup[0].pos)    // Output: 1
print(arrayTup[0].speed)  // Output: 10

// Reference Check Equality Identity Operators (=== and !==)
```

## Higher order functions
```Swift
Higher-order functions are functions that either take other functions as parameters or return functions as resutls. They allow for a functional programming approach, making code more concise and expressive, especially when working with collections.

Swift provides several built-in higher order functions for collections:
1. map: Transforms each elemnts of a collection using a closure and returns a new collection
let number = [1,2,3,4]
let doubled = numbers.map { $0 * 2 } // 2,4,6,8

To change the type with map we can do things like:
let isPostiveIndex = nums.map { $0 > 0 }
// or
let isPostiveIndex = nums.map { num -> Bool in num > 0 } // This is the same but more explicit
// or if we were doing something multiline:
let isPostiveIndex = nums.map { num -> Bool in // The explicit return is not necessary
                                if num > 1 {
                                    return true
                                }
                                else if (...) {...}
                                return ...
                    }

2. filter: Filters elements of a collection based on a condition provided in a closure (white list)
let numbers = [1, 2, 3, 4]
let evenNumbers = numbers.filter { $0 % 2 == 0 }  // [2, 4]

3. reduce: Combines all elements of a collection into a single value, starting with an initial value
let numbers = [1, 2, 3, 4]
let sum = numbers.reduce(0) { $0 + $1 }  // 10

4. flatMap: Transforms each element into a new collection and flatterns the result into a single level collection
let nestedArray = [[1, 2], [3, 4]]
let flatArray = nestedArray.flatMap { $0 }  // [1, 2, 3, 4]

5. compactMap: Similar to map, but removes any nil values from the result
let numbers = ["1", "2", "three"]
let validNumbers = numbers.compactMap { Int($0) }  // [1, 2]

6. forEach: Iterates over each element in the collection, similar to a for-in loop but without returning a value
let numbers = [1, 2, 3]
numbers.forEach { print($0) }

What is a closure in swift?

A closure is a self-contained block of code that can capture and store references to variables and constants from its surrounding context. This "capture" behavior allows closures to "close over" those values, meaning they retain the values or references to the variables from the scope in which they were created, even when used outside of that scope. ey have a concise syntax that make them useful for higher order functions.

Closures are often used in situations where you want to pass a block of code as a parameter, such as for completion handlers, callbacks, asynch operations, or transforming data.

Practical Uses:
1. Asynchronous Operations and Callbacks: Closures are often used in networking or database calls as completion handlers:
func fetchData(completion: @escaping (String) -> Void) {
    // Simulate async work
    DispatchQueue.main.asyncAfter(deadline: .now() + 1) {
        completion("Data fetched")
    }
}

fetchData { data in
    print(data)  // Output: Data fetched
}

2. Capture LIst and Avoiding Retain Cycles: Closures in Swift can sometimes create retain cycles if they strongly reference selt within the closure's body. Swift's [weak self] capture list allows you to break this cycle:
someObject.someMethod { [weak self] result in
    self?.handle(result)
}

3. Higher order foos
```

## Strings
// Substring vs string
A Substring is a lightweight view into a String and avoids extra memory allocation
- Use Substring when you need to read the string and no modify it
- Use String when you need to change the the data or make a copy to store it

```Swift
// .count is O(n) unlike for arrays it's O(1)

// ** split Function **
let text = "Swift is a fun programming language"
let words = text.split(separator: " ") //This is a list of substrings! I want a list of strings
print(words)
// Output: ["Swift", "is", "a", "fun", "programming", "language"]

let words = text.split(separator: " ").map { String($0) } // a list of strings


// convert string to list
let s = "abcd"
let characters = Array(s)
print(characters)
// This will be an array of characters: ['a', 'b', 'c', 'd']

String(s.sorted()) // this can converst array of characters to string

let s = "Hello"
let sStrings = s.map { String($0) } // This will be an array of strings: ["H", "e", "l", "l", "o"]


//# ** count Function **
//# returns the number of occurrences of a substring in the given string.
let message = "python is popular programming language"
let count = message.filter { $0 == "p" }.count
print("Number of occurrence of p:", count)
// Output: Number of occurrence of p: 4

//# The isnumeric() method returns True if all characters in a string are numeric characters. If not, it returns False.
let s = "1242323"
let isNumeric = s.allSatisfy { $0.isNumber }
print(isNumeric) // Output: true

// The returns the index of first occurrence of the substring (if found). If not found, it returns -1.
// check the index of 'fun'
let message = "python is a fun programming language"
if let index = message.range(of: "fun")?.lowerBound {
    print(message.distance(from: message.startIndex, to: index))
} else {
    print(-1)
}
// Output: 12
// More info on range and lowerBound for finding the 'index':
/*
In Swift, the line if let index = message.range(of: "fun")?.lowerBound { ... } works by using the range(of:) method to search for a substring within a string. Here’s how each part works:

message.range(of: "fun"): The range(of:) method on a string searches for the first occurrence of the specified substring (in this case, "fun") within message. If the substring is found, range(of:) returns an Optional Range<String.Index> that represents the range of the substring within message. If the substring is not found, range(of:) returns nil.

?.lowerBound: This part is using optional chaining (?) on the range returned by range(of:). If range(of:) finds a match, then .lowerBound accesses the starting index of that range. lowerBound represents the starting point (or first character) of the range where "fun" is found. If range(of:) returns nil, this whole expression evaluates to nil, and the if let statement will not execute.

Example: If message is "Have fun learning Swift!", then message.range(of: "fun") finds "fun" at index 5 in the string. The range for "fun" is from index 5 to index 8, so .lowerBound gives the starting index, which is 5.
*/


# returns True if all characters in the string are alphanumeric (either alphabets or numbers). If not, it returns False.
let name = "M3onicaGell22er"
let isAlphanumeric = name.allSatisfy { $0.isLetter || $0.isNumber }
print(isAlphanumeric)
// Output: true

# returns True if all characters in the string are alphabets. If not, it returns False
let name = "Monica"
let isAlpha = name.allSatisfy { $0.isLetter }
print(isAlpha)
// Output: true

# other important functions
let string = "  Hello, World!  "
let strippedString = string.trimmingCharacters(in: .whitespaces) #returns a copy of the string by removing both the leading and the trailing characters (based on the string argument passed).

let uppercasedString = string.uppercased()

let lowercasedString = string.lowercased() 
let isLower = string.allSatisfy { $0.isLowercase } 
let isDigit = string.allSatisfy { $0.isNumber }
let isUpper = string.allSatisfy { $0.isUppercase }

//Sorting a string:
let originalString = "swift programming"
let sortedString = String(originalString.sorted())
print(sortedString)  // Output: "gimmnoprrrssttw"

//Case Sensitivity: By default, the sorting is case-sensitive, meaning uppercase letters will be sorted before lowercase letters. If you want a case-insensitive sort, you can use a custom sorting closure:
let sortedStringCaseInsensitive = String(originalString.sorted { 
    $0.lowercased() < $1.lowercased() 
})
print(sortedStringCaseInsensitive)  // Output: " ggiimmnnooprrrsstw"


//String slicing:
// 1. Slicing with Start and Stop Indices: You can use index(_:offsetBy:) and substring(with:) methods to extract substrings.
let str = "Hello, Swift Programming"
let startIndex = str.index(str.startIndex, offsetBy: 7) // 'S'
let endIndex = str.index(str.startIndex, offsetBy: 12) // // This points to the space after 't'

let substring = str[startIndex..<endIndex] // "Swift"
print(substring)  // Output: "Swift"

// OR DO THIS
let str = "Hello, Swift Programming"

// Drop the first 7 characters to skip "Hello, "
// Then take the next 5 characters to get "Swift"
let substring = str.dropFirst(7).prefix(5)

print(substring)  // Output: "Swift"

// 2. Slicing from Start to End:
let substringFromStart = str[startIndex...] // "Swift Programming"
print(substringFromStart)  // Output: "Swift Programming"

// 3. Full Copy of the String
let copyOfString = str // Copies the entire string

// 4. Using a Step Value
let step = 2
let stepSlice = String(str.enumerated().compactMap { index, character in
    index % step == 0 ? character : nil
})
print(stepSlice)  // Output "Hlo wf rgamn"

// 5. Getting the Last Item
let lastTwoChars = String(str.suffix(1)) //.suffix(Int) by itself is a substring
//if u want a char...
let lastChar = str.last // Optional("g")

// 6. Getting the Last Two Items
let lastTwoChars = String(str.suffix(2)) // "ng"
print(lastTwoChars) // Output: "ng"

// 7. Everything Except the Last Two Items
let everythingExceptLastTwo = String(str.prefix(str.count - 2)) // "Hello, Swift Programm"
print(everythingExceptLastTwo) // Output: "Hello, Swift Programm"

// Reversing a string:
let originalString = "Hello, Swift!"
let reversedString = String(originalString.reversed())
print(reversedString)  // Output: "!tfiwS ,olleH"

```

## Arrays

> TODO: Time complexity info here

```swift
1. Ways to instantiate arrays
var emptyArray1: [Int] = []
var emptyArray2 = [String]()  // Type inferred as [String]
var zeros = Array(repeating: 0, count: 5)  // [0, 0, 0, 0, 0]
var emptyStrings = Array(repeating: "", count: 3)  // ["", "", ""]
var numbers = [1, 2, 3, 4, 5]
var fruits = ["Apple", "Banana", "Orange"]

var originalArray = [1, 2, 3, 4]
var copiedArray = originalArray  // A reference copy
var subArray = Array(originalArray.prefix(2))  // [1, 2]

var squares = (1...5).map { $0 * $0 }  // [1, 4, 9, 16, 25]

var set = Set([1, 2, 3, 4])
var arrayFromSet = Array(set)  // Converts set to array

var string = "Hello"
var characters = Array(string)  // ["H", "e", "l", "l", "o"]
var dict = ["a": 1, "b": 2]
var keys = Array(dict.keys)  // ["a", "b"]
var values = Array(dict.values)  // [1, 2]

var array = [Int]()
array.append(10)  // [10]
array += [20, 30]  // [10, 20, 30]

var optionalArray: [Int?] = [1, nil, 3, 4]  // [1, nil, 3, 4]

let arrayFromAnotherArray = Array(contentsOf: [1, 2, 3])  // [1, 2, 3]

var nums = [1, 2, 3]
print(nums.count) //3

// Find the index of the first occurrence of an element
if let index = nums.firstIndex(of: 1) {
    print("Index of 1 is \(index)") //is 0
}

// Append an element to the end of the array
nums.append(1) // [1, 2, 3, 1]

// Insert an element at a specific index
nums.insert(10, at: 0) // [10, 1, 2, 3, 1]

// Remove the first occurrence of an element
if let index = nums.firstIndex(of: 3) {
    nums.remove(at: index) // [10, 1, 2, 1]
}

// Create a copy of the array
let numsCopy = nums // [10, 1, 2, 1]

// Count the number of occurrences of an element
let countOfOnes = nums.filter { $0 == 1 }.count // returns 2

// Extend the array with another array (concatenate two arrays)
let someOtherList = [4, 5, 6]
nums.append(contentsOf: someOtherList) // [10, 1, 2, 1, 4, 5, 6]
// if you just want to make a new copy:
let combinedArray = array1 + array2

// Pop the last element from the array
let lastElement = nums.popLast() // Removes and returns 6

// Reverse the array in place
nums.reverse() // [5, 4, 1, 2, 1, 10]

// Sort the array in place (ascending order)
nums.sort() // [1, 1, 2, 4, 5, 10]

// Creating an array with repeated elements (similar to list multiplication in Python)
let list1 = Array(repeating: 1, count: 5) // [1, 1, 1, 1, 1]

// swap:
nums.swapAt(0, 1) //swaps stuff in these indices
```

## Matrices
```Swift
let matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

// To make it more generic and handle matrices of any size
let transposedMatrix = matrix[0].indices.map { colIndex in
    matrix.map { entireRow in entireRow[colIndex] }
}

// flatten a 3x3 matrix into a one-dimensional array in Swift
let matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

let flattened = matrix.flatMap { $0 } // Output: [1, 2, 3, 4, 5, 6, 7, 8, 9]

// flattening to get a certain block of the matrix using start and end rows and columns
let block = board[rStart...rEnd].flatMap {
    $0[cStart...cEnd]
}.filter{$0 != "."}
```


List slicing 

```Swift
let a = [1, 2, 3, 4, 5, 6, 7, 8, 9]
//Items from start through stop-1:
let slice1 = a[2..<5]  // [3, 4, 5] //REMEMBER: convert back into an Array()
//Items from start through stop
let slicedArray = arr[1...3]
//Items from start through the end of the array:
let slice2 = a[2...]  // [3, 4, 5, 6, 7, 8, 9]
//Items from the beginning through stop-1:
let slice3 = a[..<5]  // [1, 2, 3, 4, 5]
//Copy of the whole array:
let slice4 = a[0...]  // [1, 2, 3, 4, 5, 6, 7, 8, 9]

// This will give you every second element in the array: [1, 3, 5, 7, 9]
let slicedWithStep = stride(from: 0, to: a.count, by: 2).map { a[$0] }

//last item in the array
let a = [1, 2, 3, 4, 5]
if let lastItem = a.last {
    print(lastItem)  // Output: 5
}
let lastTwoItems = Array(a.suffix(2))
print(lastTwoItems)  // Output: [4, 5]
let everythingExceptLastTwo = Array(a.dropLast(2))
print(everythingExceptLastTwo)  // Output: [1, 2, 3]

Mutable Methods (In-place)
removeLast(k): Removes the last element in the collection. O(1) for arrays (amortized), O(n) for strings due to Copy-on-Write.
removeFirst(k): Removes the first element in the collection. O(n) for arrays (shifting), O(n) for strings due to Copy-on-Write.
removeSubrange(): Removes a range of elements from the collection. O(n) for shifting elements in arrays.
Non-Mutating Methods (Creates New Collections)
dropLast(k): Returns a new collection without the last element(s). O(k), where k is the number of elements dropped.
dropFirst(k): Returns a new collection without the first element(s). O(k), where k is the number of elements dropped.
prefix(k): Returns the first n elements from the collection. O(n), where n is the number of elements.
suffix(k): Returns the last n elements from the collection. O(n), where n is the number of elements.
prefix(while:): Returns elements from the start until a condition is no longer met. O(n), where n is the number of elements.
suffix(while:): Returns elements from the end until a condition is no longer met. O(n), where n is the number of elements.

```

## Linked Lists
```Swift
//TODO fill this section with useful tips and swift syntax

//This may be useful for swapping without needing to make temporary values:
var a = 5
var b = 10
swap(&a, &b)
print(a) // 10
print(b) // 5
```

## Dictionary

> Dictionaries are used to store data values in key:value pairs. *Info about **collections.Counter()** available below.*
> 
- *Operations Time Complexities*
    
    ![Untitled](https://user-images.githubusercontent.com/47276307/172330107-e68e3228-1c76-4bfb-bb38-04d18f94d5b9.jpg)
    

```Swift
// 1. Create a dictionary
var dict: [String: Int] = ["a": 1, "b": 2, "c": 3]

// 2. Returns an array of keys of the dictionary
let keys = Array(dict.keys) // Output: ["a", "b", "c"]

// 3. Returns an array of values of the dictionary
let values = Array(dict.values) // Output: [1, 2, 3]

// 4. Returns value for any corresponding key
let valueA = dict["a"] // Output: Optional(1)

// 5. Returns an array of key-value pairs as tuples
let items = Array(dict) // Output: [("a", 1), ("b", 2), ("c", 3)]

// 6. Returns a copy of the dictionary
let dictCopy = dict // Output: ["a": 1, "b": 2, "c": 3]

// 7. Pops key-value pair with that key
dict.removeValue(forKey: "a") // Removes the pair with key "a"

// 8. Removes and returns the most recent pair added (in Swift, you usually have to keep track of insertion order)
// I think we can only do this in an ordered dictionary
let lastItem = dict.removeLast() // Removes and returns the last key-value pair (if maintaining order is required)

// 9. Sets the value for the key, if key exists; else, it adds the key with the default value
let defaultValue = dict["d", default: 4] // If 'd' does not exist, it will return 4 and add 'd': 4

// 10. Inserts or updates the key-value pair in the dictionary
dict["e"] = 5 // Adds 'e' with value 5 or updates it if 'e' exists

// 11. Check if a key is in the dictionary
if dict.keys.contains("key") {
    print("Key exists.")
}

// 12. Sorting the dictionary by keys
let sortedByKeys = dict.sorted(by: { $0.key < $1.key }) // Returns an array of tuples sorted by keys

// 13. Sorting the dictionary by values
let sortedByValues = dict.sorted(by: { $0.value < $1.value }) // Returns an array of tuples sorted by values

// 14. Sorting the dictionary by values in reverse order
let sortedByValuesDesc = dict.sorted(by: { $0.value > $1.value }) // Returns an array of tuples sorted by values in descending order

// 15. Iterate through the dictionary
for (key, value) in dict {
    print("\(key): \(value)") // Prints key-value pairs
}

// 16. Default dict kind of
counts[element, default: 0] += 1

//16.2 keys
// A. Define a dictionary with a tuple as the key (can't do this so here is a work around)
struct Point: Hashable {
    let x: Int
    let y: Int
}
var dict: [Point: String] = [:]
dict[Point(x: 0, y: 0)] = "Origin"
```

## Functional Programming 
```Swift
// 1. .map{expression} allows you to 1 to 1 'map' a each value - it applies a given closure to each element of a collection, returning a new collection where each element is the result of the closure's transformation
// Return a new array containing the squares of each number.
let numbers = [1, 2, 3, 4]
let squares = numbers.map { $0 * $0 } // Output: [1, 4, 9, 16]

// 2. .filter{condition} applies a given closure to each element in a collection and returns a new collection where each element 'passed'
let numbers = [1, 2, 3, 4, 5, 6]
let evens = numbers.filter { $0 % 2 == 0 } // Output: [2, 4, 6]

// 3. .reduce(initialVal, {expression}) allows you to take a collection and returns a cumulative outcome (like sum) of the whole thing
let numbers = [1, 2, 3, 4]
let sum = numbers.reduce(0, { $0 + $1 }) // Output: 10

// 4. Counter with reduce - note: use into: to modify a mutable collection directly
let result = fruits.reduce([:]) { (accumulator, element) in
    // Your logic here, using `accumulator` and `element`
}
// can be done with
let fruits = ["apple", "banana", "apple", "orange", "banana", "apple"]
let fruitCount = fruits.reduce(into: [:]) { counts, fruit in
    counts[fruit, default: 0] += 1
}
//or
let counts = fruits.reduce(into: [:]) { $0[$1, default: 0] += 1 }

// 5. Grouping anagrams
let strs = ["eat", "tea", "tan", "ate", "nat", "bat"]
let groupedAnagrams = Dictionary(grouping: strs, by: { String($0.sorted()) })
// Output: ["aet": ["eat", "tea", "ate"], "ant": ["tan", "nat"], "bat": ["bat"]]

// 6. Fancy sorting (first n elements)
let topK = Array(numbers.sorted(by: >).prefix(k)

// 7. topK
// use reduce to get the counter, then sort by value, map to get only keys, and get the prefix
Array(nums.reduce(into: [:]) {$0[$1, default: 0]+=1}.sorted(by: {$0.value > $1.value}).map{$0.key}.prefix(k))
```

## Sets

> A set is a collection which is unordered, immutable, unindexed, No Duplicates.
> 
- *Operations Time Complexities*
    
    ![Untitled](https://user-images.githubusercontent.com/47276307/172330132-7a785f5f-bbc6-43b9-b82f-794190813787.jpg)
    

```swift
// 1. Initialize a Set in Swift
var set: Set<Int> = [1, 2, 3]
// = Set([1,2,3])
// = Set(arrayLiteral: arr[0]) or = Set[arr[0]]) //for one element

// Hasing work around for tuple
struct Point: Hashable {
    let x: Int
    let y: Int
}
var visited: Set<Point> = [Point(x: 0, y: 0)]

// 2. Add an item to the set
set.insert(4) // Adds 4 to the set

// 3. Remove an item from the set
set.remove(2) // Removes 2 from the set, if it exists

// 4. Safely remove an item using optional handling (like discard)
if let removedItem = set.remove(5) {
    print("Removed \(removedItem)")
} else {
    print("Item not found") // No error thrown if the item does not exist
}

// 5. Pop a random item from the set
if let randomElement = set.popFirst() {
    print("Randomly removed item: \(randomElement)")
}

// 6. Check if two sets have no common elements
let anotherSet: Set<Int> = [5, 6]
let isDisjoint = set.isDisjoint(with: anotherSet) // Returns true if no common elements

// 7. Check if one set is a subset of another
let isSubset = set.isSubset(of: anotherSet) // Returns true if all elements of set are in anotherSet

// 8. Check if one set is a superset of another
let isSuperset = set.isSuperset(of: anotherSet) // Returns true if all elements of anotherSet are in set

// 9. Find the difference between two sets
let differenceSet = set.subtracting(anotherSet) // Elements only in the first set

// 10. Update the set to keep only unique elements not in anotherSet
set.subtract(anotherSet) // Removes common elements directly from set

// 11. Find the intersection of two sets
let intersectionSet = set.intersection(anotherSet) // Returns set with common elements

// 12. Update the set to keep only the intersection of elements
set.formIntersection(anotherSet) // Modifies set to keep only common elements

// 13. Find the symmetric difference (non-common elements) between two sets
let symmetricDifferenceSet = set.symmetricDifference(anotherSet) // Returns non-common elements

// 14. Update the set with the symmetric difference (non-common elements)
set.formSymmetricDifference(anotherSet) // Keeps only non-common elements in the original set

// 15. Union of two sets (combining without duplicates)
let unionSet = set.union(anotherSet) // Combines both sets without duplicates

// 16. Update the original set with another set (equivalent to union)
set.formUnion(anotherSet) // Adds all elements of anotherSet to set without duplicates


```

## Ordered Sets
Kind of like an ordered array and set combined

```swift
import Collections
var orderedSet: OrderedSet = [1, 2, 3, 2, 1]
orderedSet.append(4) //instead of the usual insert we do this unless we insert at a specific location
orderedSet.insert(0, at: 0)
orderedSet.remove(2)
orderedSet.remove(at: 0)
orderedSet.removeFirst()
orderedSet.removeLast()
windowContents.removeSubrange(0...duplicateIndex)
windowContents = windowContents.suffix(from: startPos) //getting everything including starting from startPos
print(orderedSet[1]) // Access elements by index, just like an array
orderedSet.count
orderedSet.contains(3)
if let index = orderedSet.firstIndex(of: 3) {
    print("Index of 3 is \(index)") 
}
for element in orderedSet { //We can itterate normally just like a regular set
    print(element)
}
```

## Tuples

> A [tuple](https://www.scaler.com/topics/python/tuples-in-python/) is a collection which is ordered, unchangeable and can contain duplicate values
> 
- *Operations Time Complexities*
    
    Similar to list
    

```swift
// is not hashable (cant be used in sets or as key in dictionary_)
let tuple = (1, 2, 3, 1)
// or
let tuple: (Type1, Type2, Type3) = (value1, value2, value3)

// Hashing work around
struct Point: Hashable {
    let x: Int
    let y: Int
}
var visited: Set<Point> = [Point(x: 0, y: 0)]

// tuple with named parameters:
let person: (name: String, age: Int) = (name: "kev", age: 28)

// sorting based on multiple parameters
let sortedPeople = people.sorted {
    ($0.age, $0.name) > ($1.age, $1.name)
}
```

## Deque

> A double-ended queue, or deque, has the feature of adding and removing elements from either end.
> 
- *Operations Time Complexities*
    
    ![Untitled](https://user-images.githubusercontent.com/47276307/172330115-78500420-3276-4e45-8ce3-fd668b7eb14e.jpg)
    

```swift

import Foundation
import Collections // Make sure to import the Swift Collections package

// Start with a deque
var queue: Deque<String> = Deque(["name", "age", "DOB"])

// var queue = Deque(arrayLiteral: (Point(x: 0, y: 0), 0))
//    var queue = Deque([(Point(x: 0, y: 0), 0)]) // Another way to write this

// Append an element to the right
queue.append("append_from_right") // O(1)

// Pop from the right
let poppedRight = queue.popLast() // O(1)

// Append an element to the left
queue.prepend("fromLeft") // O(1)

// Pop from the left
let poppedLeft = queue.popFirst() // O(1)

// Find the index of an element (this operation is O(n))
if let index = queue.firstIndex(of: "age") {
    print("Index of 'age': \(index)")
}

// Insert an element at a specific index (O(n))
queue.insert("insertedElement", at: 1) // O(n)

// Remove the first occurrence of an element (O(n))
if let indexToRemove = queue.firstIndex(of: "name") {
    queue.remove(at: indexToRemove) // O(n)
}

// Count of elements (O(1))
let count = queue.count // O(1)

// Reverse the order of elements (O(n))
queue.reverse() // O(n)

// For debugging
print("Queue after operations: \(queue)")


```

## Heap

> As we know the Heap Data Structure is used to implement the Priority Queue ADT. In python we can directly access a Priority Queue implemented using a Heap by using the **Heapq** library/module.
> 
- *Operations Time Complexities*
    
todo
    

```swift
// Create an empty heap
var heap = Heap<Int>()

// Initialize with elements
var heapFromSequence = Heap([5, 3, 8, 1, 2])

print(heap.isEmpty) // true for an empty heap
print(heapFromSequence.count) // Output: 5

print(heapFromSequence.min) // Output: 1
print(heapFromSequence.max) // Output: 8

heapFromSequence.insert(6)
heapFromSequence.insert(contentsOf: [9, 0])
// Now heapFromSequence contains [5, 3, 8, 1, 2, 6, 9, 0]

if let smallest = heapFromSequence.popMin() {
    print(smallest) // Output: 0 (smallest element)
}
if let largest = heapFromSequence.popMax() {
    print(largest) // Output: 9 (largest element)
}

heapFromSequence.replaceMin(with: 4) // Replaces current min with 4
heapFromSequence.replaceMax(with: 10) // Replaces current max with 10

// Reserve space to improve efficiency if you know how many elements you’ll add:
heapFromSequence.reserveCapacity(20)

//To itterate a heap we need to do one of these

// to itterate through a heap
for item in heapFromSequence.unordered {
    print(item)
}

// Accessing elements directly
let elements = heap.elements  // This gives you an unordered array of elements
for element in elements {
    print(element)  // You can iterate over this array
}
```


# Built-in or Library functions

- Functions to iterate over list / other iterable (tuple, dictionaries)
    
    ```Swift
    // is at least one or all true?
    let arr = [1, 2, 3, 4]
    let result = arr.contains { $0 > 2 }  // Checks if any element is greater than 2
    print(result)  // Output: true

    //we can also do
    arr.allSatisfy { } //if we want to check if all true

    
    ***************** import bisect ***********************
    
    ** O(log(n))
    # [ returns the index where the element should be inserted 
    #		such that sorting order is maintained ]
    var sortedArray = [1, 2, 4]
    let insertIndex = binarySearch(sortedArray, for: 3)
    sortedArray.insert(3, at: insertIndex)
    print(sortedArray)  // Output: [1, 2, 3, 4]

    ```
    
- Getting ASCII value of a character
    
    ```Swift
    let character: Character = "A"
    print(character.asciiValue ?? "No ASCII value")  // Output: 65

    let asciiValue: UInt8 = 65
    print(Character(UnicodeScalar(asciiValue)))  // Output: A

    ```
    
## swift-algorithms

```swift
    #Combinations

    A type that computes combinations of a collection’s elements.
    The combinations(ofCount:) method returns a sequence of all the different combinations of a collection’s elements, with each combination in the order of the original collection.
    Useful for subsets type problems

    let numbers2 = [20, 10, 10]
    for combo in numbers2.combinations(ofCount: 2) {
        print(combo)
    }
    // [20, 10]
    // [20, 10]
    // [10, 10]

    // Given a range, the combinations(ofCount:) method returns a sequence of all the different combinations of the given sizes of a collection’s elements in increasing order of size.
    let numbers = [10, 20, 30, 40]
    for combo in numbers.combinations(ofCount: 2...3) {
        print(combo)
    }
    // [10, 20]
    // [10, 30]
    // [10, 40]
    // [20, 30]
    // [20, 40]
    // [30, 40]
    // [10, 20, 30]
    // [10, 20, 40]
    // [10, 30, 40]
    // [20, 30, 40]


    Note:
    Permutations: Order matters, resulting in all possible ordered sequences.
    Combinations: Order does not matter, resulting in unique groups of items without regard to sequence.

    #Permutations
    Methods that compute permutations of a collection’s elements, or of a subset of those elements.
    The permutations(ofCount:) method, when called without the ofCount parameter, returns a sequence of all the different permutations of a collection’s elements

    let numbers = [10, 20, 30]
    for perm in numbers.permutations() {
        print(perm)
    }
    // [10, 20, 30]
    // [10, 30, 20]
    // [20, 10, 30]
    // [20, 30, 10]
    // [30, 10, 20]
    // [30, 20, 10]

    Passing a value for ofCount generates partial permutations, each with the specified number of elements:
    let numbers2 = [20, 10, 10]
    for perm in numbers2.permutations() {
        print(perm)
    }
    // [20, 10, 10]
    // [20, 10, 10]
    // [10, 20, 10]
    // [10, 10, 20]
    // [10, 20, 10]
    // [10, 10, 20]
    
    To generate only unique permutations, use the uniquePermutations(ofCount:) method:
    for perm in numbers2.uniquePermutations() {
        print(perm)
    }
    // [20, 10, 10]
    // [10, 20, 10]
    // [10, 10, 20]
    
    Given a range, the methods return a sequence of all the different permutations of the given sizes of a collection’s elements in increasing order of size.
    let numbers = [10, 20, 30]
    for perm in numbers.permutations(ofCount: 0...) {
        print(perm)
    }
    // []
    // [10]
    // [20]
    // [30]
    // [10, 20]
    // [10, 30]
    // [20, 10]
    // [20, 30]
    // [30, 10]
    // [30, 20]
    // [10, 20, 30]
    // [10, 30, 20]
    // [20, 10, 30]
    // [20, 30, 10]
    // [30, 10, 20]
    // [30, 20, 10]

    #Product
    product can make the code more concise, easier to extend, and potentially more memory efficient. It’s often a good choice when working with Cartesian products, especially if working with large datasets or multiple collections.

    // Using product
    for (x, y) in product(1...3, ["a", "b", "c"]) {
        print(x, y)
    }
    
    // Double loop equivalent
    for x in 1...3 {
        for y in ["a", "b", "c"] {
            print(x, y)
        }
    }

    #Chunked
    Break a collection into nonoverlapping subsequences:
    
    chunked(by:) forms chunks of consecutive elements that pass a binary predicate,
    chunked(on:) forms chunks of consecutive elements that project to equal values,
    chunks(ofCount:) forms chunks of a given size, and
    evenlyChunked(in:) forms a given number of equally-sized chunks.
    
    chunked(by:) uses a binary predicate to test consecutive elements, separating chunks where the predicate returns false. For example, you can chunk a collection into ascending sequences using this method:
    let numbers = [10, 20, 30, 10, 40, 40, 10, 20]
    let chunks = numbers.chunked(by: { $0 <= $1 })
    // [[10, 20, 30], [10, 40, 40], [10, 20]]
    
    The chunked(on:) method, by contrast, takes a projection of each element and separates chunks where the projection of two consecutive elements is not equal. The result includes both the projected value and the subsequence that groups elements with that projected value:
    let names = ["David", "Kyle", "Karoy", "Nate"]
    let chunks = names.chunked(on: \.first!)
    // [("D", ["David"]), ("K", ["Kyle", "Karoy"]), ("N", ["Nate"])]
    
    The chunks(ofCount:) method takes a count parameter (required to be > 0) and separates the collection into chunks of this given count. If the length of the collection is a multiple of the count parameter, all chunks will have the a count equal to the parameter. Otherwise, the last chunk will contain the remaining elements.
    let names = ["David", "Kyle", "Karoy", "Nate"]
    let evenly = names.chunks(ofCount: 2)
    // equivalent to [["David", "Kyle"], ["Karoy", "Nate"]] 
    
    let remaining = names.chunks(ofCount: 3)
    // equivalent to [["David", "Kyle", "Karoy"], ["Nate"]]
    
    The evenlyChunked(in:) method takes a count parameter and divides the collection into count number of equally-sized chunks. If the length of the collection is not a multiple of the count parameter, the chunks at the start will be longer than the chunks at the end.
    
    let evenChunks = (0..<15).evenlyChunked(in: 3)
    // equivalent to [0..<5, 5..<10, 10..<15]
    
    let nearlyEvenChunks = (0..<15).evenlyChunked(in: 4)
    // equivalent to [0..<4, 4..<8, 8..<12, 12..<15]
    When "chunking" a collection, the entire collection is included in the result, unlike the split family of methods, where separators are dropped. Joining the result of a chunking method call results in a collection equivalent to the original.
    
    c.elementsEqual(c.chunked(...).joined())
    // true

# Chain
    Unlike placing two collections in an array and calling joined(), chaining permits different collection types, performs no allocations, and can preserve the shared conformances of the two underlying types.

    Concatenates two collections with the same element type, one after another.
    This operation is available for any two sequences by calling the chain(_:_:) function.
    
    let numbers = chain([10, 20, 30], 1...5)
    // Array(numbers) == [10, 20, 30, 1, 2, 3, 4, 5]
    
    let letters = chain("abcde", "FGHIJ")
    // String(letters) == "abcdeFGHIJ"

# Cycle
    In summary, cycle is a powerful utility for scenarios requiring repeated or infinite sequences. It simplifies handling cyclic behavior and allows you to focus on the logic rather than manually managing sequence boundaries.
    let colors = ["red", "green", "blue"]
    let repeatingColors = colors.cycled().prefix(10)
    
    for color in repeatingColors {
        print(color) // Output will be: red, green, blue, red, green, blue, red, green, blue, red
    }

# Unique
    Removing duplicates while maintaining order, especially in sequences where order matters (e.g., de-duplicating consecutive words in a sentence).
    Maintaining unique consecutive elements only, useful for data compression in sequences.
    
    let numbers = [1, 2, 3, 3, 2, 3, 3, 2, 2, 2, 1]
    
    let unique = numbers.uniqued()
    // Array(unique) == [1, 2, 3]

# Random Sampling
    Operations for randomly selecting k elements without replacement from a sequence or collection.
    
    Use these methods for sampling multiple elements from a collection, optionally maintaining the relative order of the elements. Each method has an overload that takes a RandomNumberGenerator as a parameter.
    
    var source = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
    
    source.randomSample(count: 4)
    // e.g. [30, 10, 70, 50]
    source.randomStableSample(count: 4)
    // e.g. [20, 30, 80, 100]
    
    var rng = SplitMix64(seed: 0)
    source.randomSample(count: 4, using: &rng)

# Indexed //not sure when we would really use this instead of enumerated tbh
enumerated(): Produces a sequence of (offset, element) pairs, where offset is always a zero-based integer. This is helpful when you only need a sequential index (0, 1, 2, …) without needing the original collection’s index type.
Indexed: Pairs each element with its actual index type from the collection (such as Int for arrays or String.Index for strings). This is useful for collections with non-integer or non-sequential indices, such as Dictionary, Set, or String.

Perhaps this is more guaranteed not to cause runtime crashes especially if you mutate an array while looping?

var matchingIndices: Set<Int> = []
for (i, n) in numbers.indexed() {
    if n.isMultiple(of: 20) { 
        matchingIndices.insert(i) 
    }
}

# Partition
    Methods for performing a stable partition on mutable collections, and for finding the partitioning index in an already partitioned collection.
    
    The standard library’s existing partition(by:) method, which re-orders the elements in a collection into two partitions based on a given predicate, doesn’t guarantee stability for either partition. That is, the order of the elements in each partition doesn’t necessarily match their relative order in the original collection. These new methods expand on the existing partition(by:) by providing stability for one or both partitions.
    
    // existing partition(by:) - unstable ordering
    var numbers = [10, 20, 30, 40, 50, 60, 70, 80]
    let p1 = numbers.partition(by: { $0.isMultiple(of: 20) })
    // p1 == 4
    // numbers == [10, 70, 30, 50, 40, 60, 20, 80]
    
    // new stablePartition(by:) - keeps the relative order of both partitions
    numbers = [10, 20, 30, 40, 50, 60, 70, 80]
    let p2 = numbers.stablePartition(by: { $0.isMultiple(of: 20) })
    // p2 == 4
    // numbers == [10, 30, 50, 70, 20, 40, 60, 80]
    Since partitioning is frequently used in divide-and-conquer algorithms, we also include a variant that accepts a range parameter to avoid copying when mutating slices, as well as a range-based variant of the existing standard library partition.
    
    The partitioningIndex(where:) method returns the index of the start of the second partition when called on an already partitioned collection.
    
    let numbers = [10, 30, 50, 70, 20, 40, 60]
    let p = numbers.partitioningIndex(where: { $0.isMultiple(of: 20) })
    // numbers[..<p] == [10, 30, 50, 70]
    // numbers[p...] = [20, 40, 60]
    The standard library’s existing filter(_:) method provides functionality to get the elements that do match a given predicate. partitioned(by:) returns both the elements that match the predicate as well as those that don’t, as a tuple.
    
    let cast = ["Vivien", "Marlon", "Kim", "Karl"]
    let (longNames, shortNames) = cast.partitioned(by: { $0.count < 5 })
    print(longNames)
    // Prints "["Vivien", "Marlon"]"
    print(shortNames)
    // Prints "["Kim", "Karl"]"

# Rotate
    A mutating method that rotates the elements of a collection to new positions.
    
    var numbers = [10, 20, 30, 40, 50, 60]
    let p = numbers.rotate(toStartAt: 2)
    // numbers == [30, 40, 50, 60, 10, 20]
    // p == 4 -- numbers[p] == 10
    To work around the CoW / slice mutation problem for divide-and-conquer algorithms, which are the idiomatic use case for rotation, this also includes variants that take a range:
    
    var numbers = [10, 20, 30, 40, 50, 60]
    numbers.rotate(subrange: 0..<3, toStartAt: 1)
    // numbers = [20, 30, 10, 40, 50, 60]
    numbers.rotate(subrange: 3..<6, toStartAt: 4)
    // numbers = [20, 30, 10, 50, 60, 40]

# max and min
    let numbers = [10, 20, 15, 30, 25]
    let k = 3
    
    let topK = numbers.max(count: k, sortedBy: >)
    print(topK) // [30, 25, 20]
    In this case, max(count:k, sortedBy:) efficiently extracts the k largest elements without sorting the entire array, making it potentially more optimal, especially when k is much smaller than the size of the array.
    
    Key Differences
    Sorting + prefix: Sorting the entire array and using prefix(k) gives you a sorted list, which is O(n log n). If you want to preserve order or if k is not small, this can be fine.
    max(count:): This is more efficient in some cases. It is O(n log k), making it optimal if you're only interested in the top k elements.

# Compacted
remove all nil values from a collection of optional values
let numbers: [Int?] = [1, nil, 2, nil, 3]
let compactedNumbers = numbers.compacted()
print(compactedNumbers) // Output: [1, 2, 3]

# firstNonNil
helps in finding the first non-nil value in a collection of optionals
let numbers: [Int?] = [nil, nil, 3, 5, 7]
let firstNonNilValue = numbers.firstNonNil()
print(firstNonNilValue) // Output: Optional(3)

```

# Clean Code Tips


# Miscellaneous

- How to take multiple line input?
    
    **Syntax :**
    
    ```swift
    let input = readLine()!
    let values = input.split(separator: " ")
    ```
    
    ## Example
    
    ```swift
    // Read a line of input and split it into components
    let input = readLine()!

    // Split the input into parts using space as the separator
    let values = input.split(separator: " ")

    // Assign values to variables
    let x = values[0]
    let y = values[1]

    print("First value: \(x)")
    print("Second value: \(y)")

    // Read the line of input, split by space, and convert to integers. For Multiple Integer Inputs:
    let input = readLine()!
    let values = input.split(separator: " ").map { Int($0)! }

    print("Entered values: \(values)")

    // Read multiple lines of input
    var lines = [String]()
    while let line = readLine(), !line.isEmpty {
        lines.append(line)
    }
    
    // Example: process the lines
    for line in lines {
        print("You entered: \(line)")
    }
    ```
    
    
- Math Functions
    
    - Log Function - Example 1: Natural Logarithm (log base e)
    
    ```swift
    import Foundation

    let value: Double = 14.0
    let naturalLog = log(value) // log base e
    print("Natural logarithm of 14 is: \(naturalLog)")

    ```

  - Log Function - Example 2: Logarithm with a Specific Base
    
    ```swift
    import Foundation

    let value: Double = 14.0
    let base: Double = 5.0
    let logBase5 = log(value) / log(base) // log base 5
    print("Logarithm base 5 of 14 is: \(logBase5)")
    ```
    
    - Example of Using ceil() and floor() in Swift:
    
    ```swift
    import Foundation

    let a: Double = 2.3
    
    // Returning the ceil of 2.3 (i.e 3)
    let ceilValue = ceil(a)
    print("The ceil of 2.3 is: \(ceilValue)")
    
    // Returning the floor of 2.3 (i.e 2)
    let floorValue = floor(a)
    print("The floor of 2.3 is: \(floorValue)")
    ```
    
    - Other Math
    
    ```swift
    import Foundation

    // Constants
    
    // Euler's number (e)
    print("Euler's number (e): \(M_E)")  // M_E is a constant for e
    
    // Pi (π)
    print("Pi (π): \(M_PI)")  // M_PI is a constant for pi
    
    // GCD of two numbers
    let a = 30
    let b = 12
    let gcdValue = gcd(a, b)
    print("GCD of \(b) and \(a): \(gcdValue)")
    
    // Power of a number (3^4)
    let powerValue = pow(3.0, 4.0)
    print("3^4: \(powerValue)")
    
    // Square root of 4
    let sqrtValue = sqrt(4.0)
    print("Square root of 4: \(sqrtValue)")
    
    // Convert radians to degrees
    let radians = M_PI / 6
    let degrees = radians * 180 / M_PI
    print("The converted value from radians to degrees: \(degrees)")
    
    // Convert degrees to radians
    let degreesValue = 30.0
    let radiansConverted = degreesValue * M_PI / 180
    print("The converted value from degrees to radians: \(radiansConverted)")

    // Todo: find the swift library that handles this
    // Swift does not provide a built-in function for GCD directly. However, you can define it yourself. Here is an implementation of the GCD function:
    func gcd(_ a: Int, _ b: Int) -> Int {
        var a = a
        var b = b
        while b != 0 {
            let temp = b
            b = a % b
            a = temp
        }
        return a
    }


    ```
    
    ```swift
    
    let number = 10
    let binaryString = String(number, radix: 2)
    print(binaryString)  // Output: "1010"

    
    // todo: maybe there is divmod in a swift library somewhere
    let dividend = 10
    let divisor = 3
    let quotient = dividend / divisor
    let remainder = dividend % divisor
    print("Quotient: \(quotient), Remainder: \(remainder)")  // Output: "Quotient: 3, Remainder: 1"

    
    ```
    
- Compare
    
    
    ```swift
    // Define a struct that you want to sort
    struct Item {
        var value: Int
        var name: String
    }
    
    // Example list of items
    var items = [
        Item(value: 10, name: "Apple"),
        Item(value: 5, name: "Banana"),
        Item(value: 15, name: "Cherry")
    ]
    
    // Custom comparator function
    func compareItems(item1: Item, item2: Item) -> Bool {
        // Sort by 'value' first, then by 'name' in case of ties
        if item1.value != item2.value {
            return item1.value < item2.value // Ascending order
        } else {
            return item1.name < item2.name // Lexicographic order if 'value' is the same
        }
    }
    
    // Sorting using the custom comparator
    let sortedItems = items.sorted(by: compareItems)
    
    // Print the sorted items
    for item in sortedItems {
        print("\(item.name): \(item.value)")
    }

    // Sorting using a tuple (first by value, then by name)
    let sortedItemsMultiCriteria = items.sorted {
        ($0.value, $0.name) < ($1.value, $1.name)
    }
    
    // Print the result
    for item in sortedItemsMultiCriteria {
        print("\(item.name): \(item.value)")
    }

    let text = "aAaBbcCdE"
    let sortedText = text.sorted { $0.lowercased() < $1.lowercased() }
    print(sortedText) // Output: ['A', 'a', 'a', 'B', 'b', 'C', 'c', 'd', 'E']

    ```
    
## Class Variable and Instance Variable
```
class Example {
    // Class variable (static property)
    static var classVar = "I am a class variable"
    
    // Instance variable (stored property)
    var instanceVar: String
    
    // Initializer to set instance variable
    init(instanceVar: String) {
        self.instanceVar = instanceVar
    }
    
    // Method to show both class and instance variables
    func showVariables() {
        // Accessing class variable
        print("Class variable:", Example.classVar)
        print("Class variable using self:", Example.classVar)
        
        // Accessing instance variable
        print("Instance variable:", self.instanceVar)
    }
}

// Creating an instance of Example
let obj = Example(instanceVar: "I am an instance variable")

// Calling the method to show variables
obj.showVariables()

```
## Max Int, Min Int 
```
Int.max and Int.min are used to represent the maximum and minimum values that an integer can hold.
Float.max and Float.min are for Float (32-bit), while Double.max and Double.min are for Double (64-bit).
```

## Integer Division
```
REMEMBER: When dividing, make int into float

let num1 = -3
let num2 = 2

let result = Int(Float(num1) / Float(num2)) // Ensures truncation toward zero
print(result)  // Output: -1
```

# Resources
https://swiftpackageindex.com/apple/swift-collections/
--


