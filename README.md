# ** Recursion **

#### Introduction
In computer programming, we as programmers use a lot repetitions. Just think about it. How many times you used a `for` loop to iterate over an array that you would add to the DOM in a webpage, or carrying manipulations in the data that you retrieved from a storage (as a collection of a certain type), being it a simple CSV file or a relational database. We all love our `for` and `while` looping statements, given their simplicity in usage. But be aware that as programmers we have another hidden gem, and you guessed it, it is * recursion *.

#### What Is Recursion ?
Recursion, put down simply, is a ** function that calls itself one or more times **, until a base case is reached.

#### How Does It Work ?
Good question. But before diving deep into the answer and later on giving some examples I would like to point out that ** recursion ** is not only used on computer programs only, but even in data-structures. Now, the matter is the following. When a recursive function is called (recursion calls are handled the same as normal function calls) in the middle of the execution of the same function, the calling function state is stored/save in what is called an ** active record ** or ** frame **, which basically keeps track of where the flow of the function was when it was interrupted. The new function called (the recursive one) is added to the stack and it starts executing. This function will either call itself another time and the same process will run again (save state of the function and add a new function to the stack) or it will return a value if the base is reached.

Do you remember about the stored function state, well when the deeper function calls start returning the calling function resumes from the same state where it was previously * "frozen" * (thanks to the active record).

#### Examples
The examples we are going to tackle will comprehend the following topics:

* Fibonacci (warm up)
* Folder cumulative sum
* Binary Search
* Create a tree like object from a given object array

** N.B: ** The programming languages used for these example will be Python and JavaScript (ES6) and you can find the example programs in the repo as well.

###### Fibonacci

#### Conclusions
Recursion is an elegant and more efficient way, sometimes, then the usual looping statements. Even because whenever you use a loop you can easily use a recursive approach but the opposite is far more unusual.
