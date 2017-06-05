# **Recursion**

#### Introduction
In computer programming, we as programmers use a lot repetitions. Just think about it. How many times you used a `for` loop to iterate over an array that you would add to the DOM in a webpage, or carrying manipulations in the data that you retrieved from a storage (as a collection of a certain type), being it a simple CSV file or a relational database. We all love our `for` and `while` looping statements, given their simplicity in usage. But be aware that as programmers we have another hidden gem, and you guessed it, it is *recursion *.

#### What Is Recursion ?
Recursion, put down simply, is a **function that calls itself one or more times**, until a base case is reached.

#### How Does It Work ?
Good question. But before diving deep into the answer and later on giving some examples I would like to point out that **recursion** is not only used on computer programs only, but even in data-structures. Now, the matter is the following. When a recursive function is called (recursion calls are handled the same as normal function calls) in the middle of the execution of the same function, the calling function state is stored/save in what is called an **active record**or **frame**, which basically keeps track of where the flow of the function was when it was interrupted. The new function called (the recursive one) is added to the stack and it starts executing. This function will either call itself another time and the same process will run again (save state of the function and add a new function to the stack) or it will return a value if the base is reached.

Do you remember about the stored function state, well when the deeper function calls start returning the calling function resumes from the same state where it was previously *"frozen"*(thanks to the active record).

#### Examples
The examples we are going to tackle will comprehend the following topics:

*Fibonacci (warm up)
*Folder cumulative sum
*Binary Search
*Create a tree like object from a given object array

**N.B:** The programming languages used for these example will be Python and JavaScript (ES6) and you can find the example programs in the repo as well.

###### Fibonacci
The mathematical approach to computer the factorial of a number is **NOT** a perfect example of a recursive approach but it is simple and basic enough to give you a general idea.

Fibonacci says:

`n! = 1 if n = 0`

`n! = n * (n-1)! if n>0`

Hence:

**Python Code**
```Python
def factorial(n):

  """
    Input: A non-negative number.
    Output: The fatorial of the number.
  """

  # Define Base Case
  if n == 0:
    return 1

  # Define Recursive Function
  else:
    return n * factorial(n-1)
```

**JavaScript Code**
```JavaScript
var factorial = (n) => {

    /*
      Input: A non-negative number.

      Output: The fatorial of the number.
    */

    if (n == 0)
      return 1;

    else
      return n * factorial(n-1);

}
```

###### File System Cumulative Sum
The problem tackled is that given the path to a file system we want to be able to compute the cumulative sum, that is the memory occupied the folder itself plus any child folders.

This recursive approach derives from the fact that all modern Operating Systems handle their file system in a recursive manner (a folder, within a folder, and so on: aka tree structure). So it is not a surprise if operations on folders (copy, delete, etc) are carries out by recursive algorithms.

**Python Code**

You will need the os module import.

```Python
def cumulative(path):

  """
    Input: The path to a file system.
    Output: The cumulative sum.
  """

  # Get immediate size
  total = os.path.getSize(path)

  # Recursive case
  if os.path.isDir(path):

    # Iterate over children dirs
    for child in os.listDir(path):

      # Compute cumulative sum
      total += os.path.join(path, child)
  return total  
```

###### Binary Search
Binary Search is one of the most important/famous algorithms in computer science, part of the divide and conquer methodology. The binary search makes searching a lot more faster than the usual sequential search (brute force). Here is a link if you want to get to know more about it: [binary search](https://en.wikipedia.org/wiki/Binary_search_algorithm).

The algorithm can be broken in the following steps:

1. If target equals the middle element then we are done.
2. If target is smaller than the middle element, we drop the upper half of the collection and we run the function again on the remaining part.
3. If target is bigger than the middle element, we drop the lower half of the collection and we run the function again on the remaining part.
4. If low > high we reached our worst base case and the element is not in the collection.

**Python Code**

You will need the os module import.

```Python
def binary_search(data, target, low, high):

  """
    Input: Elements
    Output: True or False.
  """

  # Base case element not in the collection
  if low > high:
    return False

  else:

    #Compute middle element
    mid = (low + high) // 2

    if target < data[mid]:
      binary_search(data, target, low, mid - 1)

    else:
      binary_search(data, target, mid + 1, high)

```

###### Creating tree like object
The following example is a funfunfunction episode about recursion: [video](https://www.youtube.com/watch?v=k7-N8R0-KY4)

**JavaScript Code**

```JavaScript
// Our collection
var categories = [
  {id: "animals", parent: null},
  {id: "mammals", parent: "animals"},
  {id: "cats", parent: "mammals"},
  {id: "dogs", parent: "mammals"},
  {id: "siamese", parent: "cats"},
  {id: "pitbul", parent: "dogs"},
]

var makeTree = (categories, parent) => {
  // Our building node
  let node = {}

  // Build our tree
  categories
    .filter(item => item.parent = parent)
    .map(item => node[item.id] = makeTree(categories, item.id))

  // Return tree object
  return node
}

// Call to function
makeTree(categories, null)

```

#### Useful Tips
Before wrapping up I would like to add some useful info about one of the ways you could proceed with when designing a recursive algorithm:

###### Design
1. **Test For Base Cases**:
Try to define what will be the different base cases that might arise the problem you are trying to tackle, as this is the true recursion spirit, you break the problem into subproblems but you MUST reach at one point a base case to start returning back to your original problem's solution. So make sure you understand the base cases and you TEST for them in your algorithm.

2. **Recur**: Yes, you need to recur in a recursive algorithm. If in any situation a previous call does not reach the base case, break it into smaller instances. The recursion part might even have a test case to see which recursive call to make (as in the binary search example).


###### Optimisation
Each recursive call your algorithms makes drains away CPU and takes away memory resources. Hence, makes sure you design your algorithm properly as well as optimise it in the best way. You could either try optimising it by not relying on the interpreter stack memory (at least in Python, not sure in JavaScript but should be the same), by for example using your own stack to store only the minimal information required. Another approach would be to actually eliminate **tail recursion**, where a tail recursion is a recursion whose returned value is the last operation.

#### Conclusions
Recursion is an elegant and more efficient way, sometimes, then the usual looping statements. Even because whenever you use a loop you can easily use a recursive approach but the opposite is far more unusual.
