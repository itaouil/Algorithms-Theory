# **Array-Based Sequences (Python)**

In this summary chapter the discussion is centered on three main *built-in* sequence based types in the Python programming language:

1. **Lists**
2. **Tuples**
3. **Str**

There are many similarities between these classes, for example all of them support indexing to access individual elements in the sequence and all of them uses the low-level concept of array to store the sequence. However, there are as many differences as there are similarities. One above all: **how Python differs in the internal representation**.

And as these built-in types are used in a lot of circumstances to create other data structures, it is best to give each one of them adequate time to understand the behavioural and technical differences between them.

### Low-Level Arrays

So tell me thing, how are arrays represented in the hardware ? Good question. Deep under the hood our powerful computers makes extensive use of memory. Memory is just a block of bits where data are stored. These bits make up bigger chunks, such as bytes (8 bit) which themselves make up bigger chunks and so on. Now the question is how does our computer what data in what memory location is stored. Well each of the memory location have a reference to them that is the **memory address** that explicitly define each unit of memory we have in out computer architecture, and thanks to this memory address we are able to access, retrieve and store data into memory in a constant amount of time, which is pretty good.

In computer programming there is an association between the identifier and the memory address on which the identifier's data had been stored in. We might as well reference related objects/data and this is where arrays comes into place. Arrays are a higher level container where related data get stored next to each other in a contiguous space in memory. Specific elements in the array are called cell, and they must take up a constant amount of bytes such that the various elements can be accessed in constant amount of time. In fact if you know the size of each cell, the index you want to access and at which memory address the array starts you can access the desired reference (memory address) by simply computing: ```start + cell * size```. Of course this is entirely handled by the interpreter and the OS so you and me (as programmers) only have to deal with a higher level view.

### Referential Arrays

We stated that to maintain a constant access to our array based structures the cell size must be equal for all entries of the array. But what if we are storing strings, who are notably of different lengths especially if you are storing names ? This would break the constant access time on the index. In the latter case, Python handles the list/tuple instance such that the contiguos memory is only storing a reference to the string (aka the memory address). As a consequence the array cell have all the same size as they are not storing the string directly but the memory address of where the string is stored, whose size is constant for all (64 bits). Hence, **list and tuples are referential structures**, which means we might have the same object reference on the same list, an object can be referenced in different list, and when you call methods like slice() what you obtain is a new list/tuple referencing the object of the original one, however changes to the object does not instigate a chain reaction on all the others, but it just created a new reference.

### Compact Arrays

The difference between **compact arrays** and **referential arrays** is that compact arrays do not store references to objects, but instead they store the core data, as for example **strings** they are sequential types based on indexing and arrays structure whose low level interpretation is an array referencing the single character (taking 2 bytes), of course because the character is not variable in size bit it has a constant size of 2 bytes that maintains our constant access, differently from the referenced array where we usually store size variable items.

### Compact Arrays vs Referential Arrays

The advantages of compact arrays over referential arrays resided mainly on computational and memory efficiency (which is all about computing). In fact compact arrays stores only the necessary data without the need of the memory address overhead, hence if you were to store millions of items in a referenced items you would have to store the memory address reference for all the millions of items (64bit) plus the amount of data that is taken from the type and length of the literal. This hence, makes compact arrays more memory efficient than the referential ones. Secondly, compact array are stored contiguously in memory which makes computation faster, while referential ones, although we are careful with maintaining the order of the references in our referential array, we cannot be sure that the actual datas referenced are being placed next to each other themselves.

### Dynamic Arrays and Amortization

For the memory structure to create the contiguous memory allocation a defined size has to be passed of course. This could be a limitation for one of the three sequence based types we saw, the *list*. In fact as the *tuple* and the *string* are immutable structures once they are initialised they won't be changed, hence, we won't encounter any resizing problem with those two. However, it is a different matter for the list, as it is not a mutable structure, this implies that the size of the array might grow over time as well as shrink. Python to secure a dynamic behaviour of the latter, uses a dynamic array algorithm, that behaves as follow:

1. When the list is initialised ```ex: list = [None] * 8``` the interpreter allocates a space in memory (bytes) that is notably higher than the one requested such to let the list grow (appending) without encountering problem due to filled neighboring spaces. What if we exceed the number of spaces allocated, well in this case Python requests a new allocation, or new array to our memory system so to fill the necessity.
