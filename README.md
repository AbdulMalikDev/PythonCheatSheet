# Python Cheat Sheet
> **Contributions are welcome!**
# Basics

- Data Types
    
    ![Untitled](https://user-images.githubusercontent.com/47276307/172329842-38f3de07-62d9-4d7d-9a19-fc576ee396a9.jpg)
    
- Operators and it’s precendence
    
    ![Untitled](https://user-images.githubusercontent.com/47276307/172329850-61fc0809-a4b0-416c-848b-1c502ecb4772.jpg)
    

# Data Structures

*Important data structures for Leetcode*

## Lists

> Lists are used to store multiple items in a single variable
> 
- *Operations Time Complexities*
    
    ![Untitled](https://user-images.githubusercontent.com/47276307/172330098-1c5f0a6e-7f80-4f4f-9be6-1d734e2c70cd.jpg)
    

```python
nums = [1,2,3]

nums.index(1) # returns index
nums.append(1) # appends 1
nums.insert(0,10) # inserts 10 at 0th index
nums.remove(3) # removes all instances of 3
nums.copy(1) # returns copy of the list
nums.count(1) # returns no.of times '1' is present in the list
nums.extend(someOtherList) # ...
nums.pop() # pops last element [which element to pop can also be given as optional argument]
nums.reverse() # reverses original list (nums in this case)
nums.sort() # sorts list [does NOT return sorted list]
#Python's default sort uses Tim Sort, which is a combination of both merge sort and insertion sort.
```

List or String slicing in Python

- Resource
    
    [Understanding slice notation](https://stackoverflow.com/questions/509211/understanding-slice-notation)
    

```python
It's pretty simple really:

a[start:stop]  # items start through stop-1
a[start:]      # items start through the rest of the array
a[:stop]       # items from the beginning through stop-1
a[:]           # a copy of the whole array
There is also the step value, which can be used with any of the above:

a[start:stop:step] # start through not past stop, by step
The key point to remember is that the :stop value represents the first value
that is not in the selected slice. So, the difference between stop and start is
the number of elements selected (if step is 1, the default).

The other feature is that start or stop may be a negative number, which means
it counts from the end of the array instead of the beginning. So:

a[-1]    # last item in the array
a[-2:]   # last two items in the array
a[:-2]   # everything except the last two items
Similarly, step may be a negative number:

a[::-1]    # all items in the array, reversed
a[1::-1]   # the first two items, reversed
a[:-3:-1]  # the last two items, reversed
a[-3::-1]  # everything except the last two items, reversed
Python is kind to the programmer if there are fewer items than you ask for. For
example, if you ask for a[:-2] and a only contains one element, you get an
empty list instead of an error. Sometimes you would prefer the error, so you
have to be aware that this may happen.

Relation to slice() object
The slicing operator [] is actually being used in the above code with a slice()
object using the : notation (which is only valid within []), i.e.:

a[start:stop:step]
is equivalent to:

a[slice(start, stop, step)]
Slice objects also behave slightly differently depending on the number of
arguments, similarly to range(), i.e. both slice(stop) and slice(start, stop[,
step]) are supported. To skip specifying a given argument, one might use None,
so that e.g. a[start:] is equivalent to a[slice(start, None)] or a[::-1] is
equivalent to a[slice(None, None, -1)].

While the :-based notation is very helpful for simple slicing, the explicit use
of slice() objects simplifies the programmatic generation of slicing.
```

## Dictionary

> Dictionaries are used to store data values in key:value pairs. *Info about **collections.Counter()** available below.*
> 
- *Operations Time Complexities*
    
    ![Untitled](https://user-images.githubusercontent.com/47276307/172330107-e68e3228-1c76-4bfb-bb38-04d18f94d5b9.jpg)
    

```python
dict = {'a':1,'b':2,'c':3}

dict.keys() # returns list of keys of dictionary
dict.values() # returns list of values of dictionary
dict.get('a') # returns value for any corresponding key
dict.items() # returns [('a',1),('b',2),('c',3)]
dict.copy() # returns copy of the dictionary
# NOTE : items() Returns view object that will be updated with any future
# changes to dict
dict.pop(KEY) # pops key-value pair with that key
dict.popitem() # removes most recent pair added
dict.setDefault(KEY,DEFAULT_VALUE) # returns value of key, if key exists, else default value returned
# If the key exist, this parameter(DEFAULT_VALUE) has no effect.
# If the key does not exist, DEFAULT_VALUE becomes the key's value. 2nd
# argument's default is None.
dict.update({KEY:VALUE}) # inserts pair in dictionary if not present, if present, corresponding value is overriden (not key)
# defaultdict ensures that if any element is accessed that is not present in
# the dictionary
# it will be created and error will not be thrown (which happens in normal dictionary)
# Also, the new element created will be of argument type, for example in the below line
# an element of type 'list' will be made for a Key that does not exist
myDictionary = defaultdict(list) 
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
set.discard(item) | set.remove(item) # removes item | remove will throw error if item is not there, discard will not
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

> A tuple is a collection which is ordered, unchangeable and can contain duplicate values
> 
- *Operations Time Complexities*
    
    Similar to list
    

```python
tuple = (1,2,3,1)

tuple.count(1) # returns occurence of an item
tuple.index(1) # returns index of 1 in array
```

## Strings

[Python String isnumeric()](https://www.programiz.com/python-programming/methods/string/isnumeric)

```python
# ** split Function **
# The split() method breaks up a string at the specified separator and returns
# a list of strings.
text = 'Python is a fun programming language'

# split the text from space
print(text.split(' '))
# Output: ['Python', 'is', 'a', 'fun', 'programming', 'language']

# convert string to list
s="abcd"
s=list(s)
print(s)
# Output: ['a', 'b', 'c', 'd']

# ** count Function **
# The count() method returns the number of occurrences of a substring in the given string.
# Example
message = 'python is popular programming language'
# number of occurrence of 'p'
print('Number of occurrence of p:', message.count('p')) # Output: Number of occurrence of p: 4

# The isnumeric() method returns True if all characters in a string are numeric characters. If not, it returns False.
s = '1242323'
print(s.isnumeric()) #Output: True

# The find() method returns the index of first occurrence of the substring (if found). If not found, it returns -1.
# check the index of 'fun'
print(message.find('fun')) # Output: 12

# The isalnum() method returns True if all characters in the string are alphanumeric (either alphabets or numbers). If not, it returns False.

name = "M3onica Gell22er "
print(name.isalnum()) # Output : False

# The isalpha() method returns True if all characters in the string are alphabets. If not, it returns False
name = "Monica"
print(name.isalpha()) #output true

# other imp functions
string.strip([chars]) #The strip() method returns a copy of the string by removing both the leading and the trailing characters (based on the string argument passed).
string.upper() #he upper() method converts all lowercase characters in a string into uppercase characters and returns it.
string.lower() #The lower() method converts all uppercase characters in a string into lowercase characters and returns it.
string.islower()
string.isdigit()
string.isupper()
```

# Built-in or Library functions

- Functions to iterate over list / other iterable (tuple, dictionaries)
    
    ```python
    
    ** map(fun, iter) **
    # fun : It is a function to which map passes each element of given iterable.
    # iter : It is a iterable which is to be mapped.
    
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

- **Doc Strings -**  Documentation for your functions in the interview to look slic 😎
    
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
    

> Python integer division doesn’t work properly with -ve numbers ex: -3//2 will give -2 answer instead of -1 so always use int(-3/2) for integer division in problems
> 

# Resources

- PDF with all Python Data Structures in-depth
    
    [Python Data Structure.pdf](Python%20Brushup%20bb9cdcd84f45485984711559d663c8c6/Python_Data_Structure.pdf)
    

[The Modulo Operation (%) With Negative Numbers in Python](https://betterprogramming.pub/modulo-operation-with-negative-numbers-in-python-38cb7256bb32)
