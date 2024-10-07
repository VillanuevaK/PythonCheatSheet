# Data Structures

*Important data structures for LeetCode*
- how to deal with strings
- what are closures
- what are functinoal programming paradigms (mapping, filtering, reducing)
- Higher-Order Functions

## Strings

```Swift
# ** split Function **
let text = "Python is a fun programming language"
let words = text.split(separator: " ")
print(words)
// Output: ["Python", "is", "a", "fun", "programming", "language"]

# convert string to list
let s = "abcd"
let characters = Array(s)
print(characters)
// Output: ["a", "b", "c", "d"]

# ** count Function **
# returns the number of occurrences of a substring in the given string.
let message = "python is popular programming language"
let count = message.filter { $0 == "p" }.count
print("Number of occurrence of p:", count)
// Output: Number of occurrence of p: 4

# The isnumeric() method returns True if all characters in a string are numeric characters. If not, it returns False.
let s = "1242323"
let isNumeric = s.allSatisfy { $0.isNumber }
print(isNumeric) // Output: true

# The find() method returns the index of first occurrence of the substring (if found). If not found, it returns -1.
# check the index of 'fun'
let message = "python is a fun programming language"
if let index = message.range(of: "fun")?.lowerBound {
    print(message.distance(from: message.startIndex, to: index))
} else {
    print(-1)
}
// Output: 12

# The isalnum() method returns True if all characters in the string are alphanumeric (either alphabets or numbers). If not, it returns False.
let name = "M3onicaGell22er"
let isAlphanumeric = name.allSatisfy { $0.isLetter || $0.isNumber }
print(isAlphanumeric)
// Output: true

# The isalpha() method returns True if all characters in the string are alphabets. If not, it returns False
let name = "Monica"
let isAlpha = name.allSatisfy { $0.isLetter }
print(isAlpha)
// Output: true

# other important functions
let string = "  Hello, World!  "
let strippedString = string.trimmingCharacters(in: .whitespaces) #The strip() method returns a copy of the string by removing both the leading and the trailing characters (based on the string argument passed).

let uppercasedString = string.uppercased() # The upper() method converts all lowercase characters in a string into uppercase characters and returns it.

let lowercasedString = string.lowercased() # The lower() method converts all uppercase characters in a string into lowercase characters and returns it.
let isLower = string.allSatisfy { $0.isLowercase } # The islower() method returns True if all cased characters in the string are lowercase and there is at least one cased character, False otherwise.
let isDigit = string.allSatisfy { $0.isNumber }
let isUpper = string.allSatisfy { $0.isUppercase } # The isupper() method returns True if all cased characters in the string are uppercase and there is at least one cased character, False otherwise.

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
let lastTwoChars = String(str.suffix(1))
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

## Lists

> Lists are used to store multiple items in a single variable
> 
- *Operations Time Complexities*
    
    ![Untitled](https://user-images.githubusercontent.com/47276307/172330098-1c5f0a6e-7f80-4f4f-9be6-1d734e2c70cd.jpg)
    

```swift
var nums = [1, 2, 3]

var nums = [1, 2, 3]

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

// Pop the last element from the array
let lastElement = nums.popLast() // Removes and returns 6

// Reverse the array in place
nums.reverse() // [5, 4, 1, 2, 1, 10]

// Sort the array in place (ascending order)
nums.sort() // [1, 1, 2, 4, 5, 10]

// Creating an array with repeated elements (similar to list multiplication in Python)
let list1 = Array(repeating: 1, count: 5) // [1, 1, 1, 1, 1]


```
## Matrices
```
let matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

// To transpose a matrix in Swift (turn rows into columns for easy access of just columns)
let transposedMatrix = Array(zip(matrix[0], matrix[1], matrix[2])) // Result: [(1, 4, 7), (2, 5, 8), (3, 6, 9)]
// To make it more generic and handle matrices of any size
let transposedMatrix = matrix[0].indices.map { index in
    matrix.map { $0[index] }
}


//flatMap for something similar to list compression
let board = [
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12],
    [13, 14, 15, 16]
]
let i = 1
let j = 1
let square = (i..<i+2).flatMap { x in
    (j..<j+2).map { y in
        board[x][y]
    }
}
// Result: [6, 7, 10, 11]

```


List slicing 

```Swift
let a = [1, 2, 3, 4, 5, 6, 7, 8, 9]
//Items from start through stop-1:
let slice1 = a[2..<5]  // [3, 4, 5]
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
var dict: [String: Int] = [:]
let key = "key1"
let value = dict[key] ?? 0 // Use 0 as the default if the key doesn't exist
dict[key] = value + 1 // Increment the value

or even better:
counts[element, default: 0] += 1
```

## Counter

> Python Counter is a container that will hold the count of each of the elements present in the container. The counter is a sub-class available inside the dictionary class. Specifically used for element frequencies
> 

*Pretty similar to dictionary, in fact I use* **defaultdict(int)** *most of the time* 

```python
from collections import Counter #(capital 'C')
# can also be used as 'collections.Counter()' in code

list1 = ['x','y','z','x','x','x','y', 'z']

# Initialization
Counter(list1) # => Counter({'x': 4, 'y': 2, 'z': 2})
Counter("Welcome to Guru99 Tutorials!") # => Counter({'o': 3, ' ': 3, 'u': 3, 'e': 2.....})

# Updating
counterObject = collections.Counter(list1)
counterObject.keys() = [ 'x' , 'y' , 'z' ]
most_common_element = counterObject.most_common(1) # [('x', 4)]
counterObject.update("some string") # => Counter({'o': 3, 'u': 3, 'e': 2, 's': 2})
counterObject['s'] += 1 # Increase/Decrease frequency

# Accessing
frequency_of_s = counterObject['s']

# Deleting
del couterObject['s']

```

## Deque

> A double-ended queue, or deque, has the feature of adding and removing elements from either end.
> 
- *Operations Time Complexities*
    
    ![Untitled](https://user-images.githubusercontent.com/47276307/172330115-78500420-3276-4e45-8ce3-fd668b7eb14e.jpg)
    

```python

#in BFS(Breadth-first search) or other algorithms where we have to pop or add elements to the begining , deque is the best option 
#we can also use list, but list.pop(0) is O(n) operation where as dequeu.popleft() is O(1)

from collections import deque

queue = deque(['name','age','DOB'])

queue.append("append_from_right") # Append from right
queue.pop() # Pop from right

queue.appendleft("fromLeft") # Append from left
queue.popleft() # Pop from left

queue.index(element,begin_index,end_index) # Returns first index of element b/w the 2 indices.
queue.insert(index,element)
queue.remove() # removes first occurrance
queue.count() # obvious

queue.reverse() # reverses order of queue elements
```

## Heapq

> As we know the Heap Data Structure is used to implement the Priority Queue ADT. In python we can directly access a Priority Queue implemented using a Heap by using the **Heapq** library/module.
> 
- *Operations Time Complexities*
    
    ![Untitled](https://user-images.githubusercontent.com/47276307/172330122-29cf0756-89bc-4654-a4e8-4e318156c7d1.jpg)
    

```python
import heapq # (minHeap by Default)

nums = [5, 7, 9, 1, 3]

heapq.heapify(nums) # converts list into heap. Can be converted back to list by list(nums).
heapq.heappush(nums,element) # Push an element into the heap
heapq.heappop(nums) # Pop an element from the heap
# heappush(heap, ele) :- This function is used to insert the element mentioned
# in its arguments into heap. The order is adjusted, so as heap structure is
# maintained.
# heappop(heap) :- This function is used to remove and return the smallest
# element from heap. The order is adjusted, so as heap structure is maintained.

# Other Methods Available in the Library
# Used to return the k largest elements from the iterable specified 
# The key is a function with that accepts single element from iterable,
# and the returned value from that function is then used to rank that element in the heap
heapq.nlargest(k, iterable, key = fun)
heapq.nsmallest(k, iterable, key = fun)


#Max heap in python 

#By default heapq in python is min heap, 
#if we want to use max heap we can simply invert the value of the keys and use heapq. 
#For example, turn 1000.0 into -1000.0 and 5.0 into -5.0.

#The easiest and ideal solution
#Multiply the values by -1

#All the highest numbers are now the lowest and vice versa.

#Just remember that when you pop an element to multiply it with -1 in order to get the original value again.

#Example: 

import heapq
heap = []
heapq.heappush(heap, 1*(-1))
heapq.heappush(heap, 10*(-1))
heapq.heappush(heap, 20*(-1))
print(heap)

The output will look like:

[-20, -1, -10]

#when popping element multiply it with -1

max_element = -heapq.heappop(heap)
print(max_element)

Output will be:
20
```

## Sets

> A set is a collection which is unordered, immutable, unindexed, No Duplicates.
> 
- *Operations Time Complexities*
    
    ![Untitled](https://user-images.githubusercontent.com/47276307/172330132-7a785f5f-bbc6-43b9-b82f-794190813787.jpg)
    

```python
set = {1,2,3}

set.add(item)
set.remove(item)
set.discard(item) | set.remove(item)
# removes item | remove will throw error if item is not there, discard will not
set.pop() # removes random item (since unordered)

set.isdisjoint(anotherSet) # returns true if no common elements
set.issubset(anotherSet) # returns true if all elements from anotherSet is present in original set
set.issuperset(anotherSet) # returns true if all elements from original set is present in anotherSet

set.difference(anotherSet) # returns set containing items ONLY in first set
set.difference_update(anotherSet) # removes common elements from first set [no new set is created or returned]
set.intersection(anotherSet) # returns new set with common elements
set.intersection_update(anotherSet) # modifies first set keeping only common elements
set.symmetric_difference(anotherSet) # returns set containing all non-common elements of both sets
set.symmetric_difference_update(anotherSet) # same as symmetric_difference but changes are made on original set

set.union(anotherSet) # ...
set.update(anotherSet) # adds anotherSet without duplicate

```

## Tuples

> A [tuple](https://www.scaler.com/topics/python/tuples-in-python/) is a collection which is ordered, unchangeable and can contain duplicate values
> 
- *Operations Time Complexities*
    
    Similar to list
    

```python
tuple = (1,2,3,1)

tuple.count(1) # returns occurence of an item
tuple.index(1) # returns index of 1 in array
```

# Built-in or Library functions

- Functions to iterate over list / other iterable (tuple, dictionaries)
    
    ```python
    
    ** map(fun, iter) **
    # fun : It is a function to which map passes each element of given iterable.
    # iter : It is a iterable which is to be mapped.

    #itterating 2 lists or more in for loop
    ** zip(list,list) **
    for elem1,elem2 in zip(firstList,secondList):
    	# will merge both lists and produce tuples with both elements
    	# Tuples will stop at shortest list (in case of both lists having different len)
    # Example
    '''
    a = ("John", "Charles", "Mike")
    b = ("Jenny", "Christy", "Monica")
    
    x = zip(a, b)
    
    # use the tuple() function to display a readable version of the result:
    
    print(tuple(x))
    o/p: (('John', 'Jenny'), ('Charles', 'Christy'), ('Mike', 'Monica'))
    '''
    
    ** any(list) ** [ OPPOSITE IS => ** all() ** ]
    any(someList) # returns true if ANY element in list is true [any string, all numbers except 0 also count as true]
    
    ** enumerate(list|tuple) ** 
    # [when you need to attach indexes to lists or tuples ]
    enumerate(anyList) # ['a','b','c'] => [(0, 'a'), (1, 'b'), (2, 'c')]
    #in a forloop:
    fruits = ['apple', 'banana', 'cherry']
    for index, fruit in enumerate(fruits, start=3): #start is optional
        print(index, fruit)
    #3 apple
    #4 banana
    #5 cherry
    
    ** filter(function|list) **
    filter(myFunction,list) # returns list with elements that returned true when passed in function
    
    ***************** import bisect ***********************
    
    ** bisect.bisect(list,number,begin,end) ** O(log(n))
    # [ returns the index where the element should be inserted 
    #		such that sorting order is maintained ]
    a = [1,2,4]
    bisect.bisect(a,3,0,4) # [1,2,4] => 3 coz '3' should be inserted in 3rd index to maintain sorting order
    
    # Other variants of this functions are => bisect.bisect_left() | bisect.bisect_right()
    # they have same arguments. Suppose the element we want to insert is already present
    # in the sorting list, the bisect_left() will return index left of the existing number
    # and the bisect_right() or bisect() will return index right to the existing number
    
    # ** bisect.insort(list,number,begin,end)       ** O(n) to insert
    # ** bisect.insort_right(list,number,begin,end) ** 
    # ** bisect.insort_left(list,number,begin,end)  ** 
    
    The above 3 functions are exact same of bisect.bisect(), the only difference
    is that they return the sorted list after inserting and not the index. The
    left() right() logic is also same as above.
    ```
    
- Getting ASCII value of a character
    
    ```python
    ** ord(str) **
    # returns ascii value of the character , Example ord("a") = 97
    ** chr(int) ** 
    # return character of given ascii value , Example chr(97) = "a"
    ```
    

# Clean Code Tips

- **Doc Strings -**  Documentation for your functions in the interview to look slick 😎
    
    A docstring is short for documentation string.
    
    Python docstrings (documentation strings) are the [string](https://www.programiz.com/python-programming/string) literals that appear right after the definition of a function, method, class, or module.
    
    Triple quotes are used while writing docstrings. For example:
    
    ```
    def double(num):
        """Function to double the value"""
        return 2*num
    ```
    
    Docstrings appear right after the definition of a function, class, or a module. This separates docstrings from multiline comments using triple quotes.
    
    The docstrings are associated with the object as their `__doc__` attribute.
    
    So, we can access the docstrings of the above function with the following lines of code:
    
    ```
    def double(num):
        """Function to double the value"""
        return 2*num
    print(double.__doc__)
    ```
    
    **Output**
    
    ```
    Function to double the value
    ```
    
- Use **Assert keyword** in python for testing edge cases. Looks more professional.
    
    ### Definition and Usage
    
    The `assert` keyword is used when debugging code.
    
    The `assert` keyword lets you test if a condition in your code returns True, if not, the program will raise an AssertionError.
    
    You can write a message to be written if the code returns False, check the example below.
    
    ```python
    x = "hello"
    
    #if condition returns False, AssertionError is raised:
    assert x == "goodbye", "x should be 'hello'"
    ```
    
- **ALWAYS** be aware of any code snippet that is being **REPEATED** in your solution. **MODULARITY** #1 Priority. Refactoring is also an important part of  interview.
    - This is usually asked as a follow up after coding the solution. *Are there any changes you want to make to this solution?*

# Miscellaneous

- How to take multiple line input in python?
    
    [Taking multiple inputs from user in Python - GeeksforGeeks](https://www.geeksforgeeks.org/taking-multiple-inputs-from-user-in-python/)
    
    - Using split() method
    - Using List comprehension
    
    **Syntax :**
    
    ```
    input().split(separator, maxsplit)
    ```
    
    ## Example
    
    ```python
    # Python program showing how to
    # multiple input using split
     
    # taking two inputs at a time
    x, y = input("Enter a two value: ").split()
    print("Number of boys: ", x)
    print("Number of girls: ", y)
    print()
     
    # taking three inputs at a time
    x, y, z = input("Enter a three value: ").split()
    print("Total number of students: ", x)
    print("Number of boys is : ", y)
    print("Number of girls is : ", z)
    print()
     
    # taking two inputs at a time
    a, b = input("Enter a two value: ").split()
    print("First number is {} and second number is {}".format(a, b))
    print()
     
    # taking multiple inputs at a time
    # and type casting using list() function
    x = list(map(int, input("Enter a multiple value: ").split()))
    print("List of students: ", x)
    ```
    
    ```python
    # Python program showing
    # how to take multiple input
    # using List comprehension
     
    # taking two input at a time
    x, y = [int(x) for x in input("Enter two value: ").split()]
    print("First Number is: ", x)
    print("Second Number is: ", y)
    print()
     
    # taking three input at a time
    x, y, z = [int(x) for x in input("Enter three value: ").split()]
    print("First Number is: ", x)
    print("Second Number is: ", y)
    print("Third Number is: ", z)
    print()
     
    # taking two inputs at a time
    x, y = [int(x) for x in input("Enter two value: ").split()]
    print("First number is {} and second number is {}".format(x, y))
    print()
     
    # taking multiple inputs at a time
    x = [int(x) for x in input("Enter multiple value: ").split()]
    print("Number of list is: ", x)
    
    # taking multiple inputs at a time separated by comma
    x = [int(x) for x in input("Enter multiple value: ").split(",")]
    print("Number of list is: ", x)
    ```
    
- Important Python Math Functions
    
    [Python Math Module - GeeksforGeeks](https://www.geeksforgeeks.org/python-math-module/)
    
    - Log Function
    
    [Log functions in Python - GeeksforGeeks](https://www.geeksforgeeks.org/log-functions-python/)
    
    ```
    Syntax :
    math.log(a,Base)
    Parameters :a : The numeric value
    Base :  Base to which the logarithm has to be computed.
    Return Value :
    Returns natural log if 1 argument is passed and log with
    specified base if 2 arguments are passed.
    Exceptions :
    Raises ValueError is a negative no. is passed as argument.
    ```
    
    ```python
    import math
      
    # Printing the log base e of 14
    print ("Natural logarithm of 14 is : ", end="")
    print (math.log(14))
      
    # Printing the log base 5 of 14
    print ("Logarithm base 5 of 14 is : ", end="")
    print (math.log(14,5))
    ```
    
    - Finding the ceiling and the floor value
        - Ceil value means the smallest integral value greater than the number and the floor value means the greatest integral value smaller than the number. This can be easily calculated using the ceil() and floor() method respectively.
    
    ```python
    # Python code to demonstrate the working of
    # ceil() and floor()
     
    # importing "math" for mathematical operations
    import math
     
    a = 2.3
     
    # returning the ceil of 2.3 (i.e 3)
    print ("The ceil of 2.3 is : ", end="")
    print (math.ceil(a))
     
    # returning the floor of 2.3 (i.e 2)
    print ("The floor of 2.3 is : ", end="")
    print (math.floor(a))
    
    ```
    
    - Other Important functions
    
    ```python
    # Constants
    # Print the value of Euler e (2.718281828459045)
    print (math.e)
    # Print the value of pi (3.141592653589793)
    print (math.pi)
    print (math.gcd(b, a))
    print (pow(3,4))
    # print the square root of 4
    print(math.sqrt(4))
    a = math.pi/6
    b = 30
     
    # returning the converted value from radians to degrees
    print ("The converted value from radians to degrees is : ", end="")
    print (math.degrees(a))
     
    # returning the converted value from degrees to radians
    print ("The converted value from degrees to radians is : ", end="")
    print (math.radians(b))
    ```
    
    ```python
    
    ** bin(int) **
    bin(anyNumber) # Returns binary version of number
    
    ** divmod(int,int) **
    divmod(dividend,divisor) # returns tuple like (quotient, remainder)
    
    ```
    
- Python cmp_to_key function to sort list with custom compare function
    
    [Sort a list of lists with a custom compare function](https://stackoverflow.com/questions/5213033/sort-a-list-of-lists-with-a-custom-compare-function)
    
    ## How the custom comparator works
    
    When providing a custom comparator, it should generally return an integer/float value that follows the following pattern (as with most other programming languages and frameworks):
    
    - return a negative value (`< 0`) when the left item should be sorted *before* the right item
    - return a positive value (`> 0`) when the left item should be sorted *after* the right item
    - return `0` when both the left and the right item have the same weight and should be ordered "equally" without precedence
    
    ```python
    from functools import cmp_to_key
    sorted(mylist, key=cmp_to_key(compare))
    
    # Example
    def compare(item1, item2):
        if fitness(item1) < fitness(item2):
            return -1
        elif fitness(item1) > fitness(item2):
            return 1
        else:
            return 0
    ```

    Sorting with a tie breaker/Sorting based on two things
    ```python
    tuples.sort(key=lambda x: (x[0], x[1]))
    ```

    Sort list on multiple objects but only one in reversed order
    ```python
    a = [str(i) for i in range(10,29)]
    a.sort(key = lambda x: x[1], reverse=True)
    a.sort(key = lambda x: x[0])
    ```

    Sort string in lexicographic order
    ```python
    sorted(s, key=str.lower) or sorted(s, key=str.upper)

    #for a specific order of uppers and lowers
    text='aAaBbcCdE'
    sorted(text, key=lambda x: (str.lower(x), x))
    # ['A', 'a', 'a', 'B', 'b', 'C', 'c', 'd', 'E']
    ```
    
## Class Variable and Instance Variable
```
class Example:
    # Class variable
    class_var = "I am a class variable"

    def __init__(self, instance_var):
        # Instance variable
        self.instance_var = instance_var

    def show_variables(self):
        # Accessing class variable
        print("Class variable:", Example.class_var)
        print("Class variable using self:", self.class_var)
        
        # Accessing instance variable
        print("Instance variable:", self.instance_var)

# Creating an instance of Example
obj = Example("I am an instance variable")

# Calling the method to show variables
obj.show_variables()
```
## Max Int, Min Int 
```
float('inf')
float('-inf')
```

## Integer Division
```
REMEMBER: When dividing, make int into float

> Python integer division acts a bit weird with -ve numbers ex: -3//2 will give -2 answer instead of -1 so always use int(-3/2) for integer division in problems
>
#to always truncate two integers toward zero (including negatives):
int(float(num2) / num1)
#float(num2) / num1 converts num2 to a float first and then performs true division, resulting in a float.
```

# Resources

- PDF with all Python Data Structures in-depth
    
    [Python Data Structure.pdf](https://github.com/AbdulMalikDev/PythonCheatSheet/files/9033162/Python_Cheat_Sheet_Made_by_Abdul_Malik.pdf)
    

[The Modulo Operation (%) With Negative Numbers in Python](https://betterprogramming.pub/modulo-operation-with-negative-numbers-in-python-38cb7256bb32)
--


