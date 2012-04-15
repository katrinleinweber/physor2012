# Flow Control

[Back To Python Data
Structures](http://github.com/thehackerwithin/UofCSCBC2012/tree/master/2b-PythonDataStructures)
- [Forward To Python Functions and
Modules](http://github.com/thehackerwithin/UofCSCBC2012/tree/master/2d-PythonFunctionsAndModules/)

* * * * *

**Presented By : Joshua R. Smith**

**Based on Lecture Materials By: Milad Fatenejad**

So far we've learned about various data types in python and how to rudimentarily read data out of a file. Now we will learn how to do logical operations with conditional blocks (if statements) and how to iterate using for and while loops. We will also learn to write data to a file.

## For Loops

Iteration is a very useful concept, and it appears all the time in python. Lets consider our current and voltage data again.

```python
In [1]: voltageList = [-2.0, -1.0, 0.0, 1.0, 2.0]

In [2]: currentList = [-1.0, -0.5, 0.0, 0.5, 1.0]
```

We know that power is the product of current and voltage. We already have the current as a function of voltage, but what if we wanted to generate a list of values of power coresponding to the value of voltage? We use a for loop.

```python
In [3]: powerList = [] # Initialize an empty list to be filled later.
In [4]: indxList = range(len(currentList))

In [5]: for indx in indxList:
   ....:    power = voltageList[indx] * currentList[indx]
   ....:    powerList.append(power)
``` 

There's a lot of stuff that just happened here. Lets break it down.

### Indentation

The indentation is a feature of python that some people hate. Some other programming languages use brackets to denote a command block. Python uses indentation. The amount of indentation doesn't matter, so long as everything in the same block is indented the same amount.

The for loop itself is pretty simple: we take a list (in this case), pull out the presently indexed value, and execute the block below the for command. Once the block has been executed, the for loop increments to the next index and keeps going to the end.

The range command gives us an incremental list of values. We are using it to generate our lists of indices for our for loop iteration.

## Conditional (if) Statements

There are many situations where you want to execute some code based on some condition, say you want a message to print if the value of current is higher than a preset value. In this case, you use a conditional statement. There are amny different conditions, here are some of them:

```python
i=1
j=2
i==j # i is equal to j : FALSE
i<j  # i is less than j
i<=j # i is less than or equal to j : TRUE
i>j  # i is greater than j
i>=j # i is greater than or equal to j : FALSE
i!=j # i is not equal to j : TRUE
```

Consider the following example.

```python
In [11]: for current in currentList:
   ....:     if current > 0.7:
   ....:         print "high"
   ....:     elif current < -0.7:
   ....:         print "low"
   ....:     else:
   ....:         print "ok"
   ....:         
   ....:         
low
ok
ok
ok
high
```

In this example, we are iterating over the list of values of current. We've nested the conditional statement within the for loop statement, and we are looking at each value of current to make a decision. The lowest value causes the code to display "low". The three middle values are "ok" and the last value is "high".

Conditional blocks can be a source of bugs, so make sure you are paying attention to the logic when you write them.

## While Loops

Lets start by looking at while loops since they function like while
loops in many other languages. The example below takes a list of
integers and computes the product of each number in the list up to the
-1 element.

A while loop will repeat the instructions within itself until the
conditional that defines it is no longer true.

```python
mult = 1
sequence = [1, 5, 7, 9, 3, -1, 5, 3]
while sequence[0] is not -1:
    mult = mult * sequence[0]
    del sequence[0]

print mult
```

Some new syntax has been introduced in this example.

-   On line 3 We begin the while loop. Notice that instead of using the
    not-equals symbol, !=, we can simply enter "is not" which is easier
    to read. This while loop will execute until sequence[0]= -1 . That
    is, until deletes all of the entries of the sequence that come
    before -1.

-   On line 4, we compute the product of the elements just to make this
    more interesting.

-   On line 5, we use the \`del\` keyword to remove the first element of
    the list, shifting every element down one.

**Watch Out**

Since a while loop will continue until its conditional is no longer
true, a **poorly formed** while loop might repeat forever. For example :

```python
i=1
print "Well, there's egg and bacon, egg and spam, egg bacon and"
while i is 1:
  print "spam "
print "or Lobster Thermidor a Crevette with a mornay sauce served in a Provencale manner with shallots..." 
```

Since the variable **i** never changes within the while loop, we can
expect that the conditional, **i=1** will remain true forever and the
while loop will just go round and round, as if this restaurant offered
nothing but spam. (If you try this at home, please note that one way to
interrupt a non-terminating process is **ctrl+c** or **ctrl+z**.

## Writing to a File
We could have gone over this toic in the previous lesson, but iteration makes writing data to files a lot less ugly. 

Recall our file data.dat. There is no mention of the name of the user in that file, and I want to insert my own name since I generated the data. I want my name to appear on the second line, immediately below the experiment type. Here's how we do that.

```python
# Create an empty list to contain all of the file data.
dataList = []

# Open the file and iterate over it to read all of the data into the list.
f = open("data.dat")

for line in f:
  dataList.append(line)

f.close()

# Insert my name into the list.
dataList.insert(1, "user: Joshua Ryan Smith\n")

# Open a new file for writing and write all of the new lines to it.
f = open("newdat.dat", "w")
for line in dataList:
  f.write(line)

f.close()
```

You have to have that newline character or else you're going to get a weird result.

# break, continue, and else

A break statement cuts off a loop from within an inner loop. It helps
avoid infinite loops by cutting off loops when they're clearly going
nowhere.

```python
reasonable = 10
for n in range(1,2000):
    if n == reasonable :
        break
    print n
```

Something you might want to do instead of breaking is to continue to the
next iteration of a loop, giving up on the current one..

```python
reasonable = 10
for n in range(1,2000):
    if n == reasonable :
      continue
    print n
```

What is the difference between the output of these two?

Importantly, Python allows you to use an else statement in a for loop.

That is :

```python
knights={"Sir Belvedere":"the Wise", "Sir Lancelot":"the Brave", \
        "Sir Galahad":"the Pure", "Sir Robin":"the Brave", "The Black Knight":"John Clease"} 

favorites=knights.keys()
favorites.remove("Sir Robin")
for name, title in knights.iteritems() : 
    string = name + ", "
    for fav in favorites :
        if fav == name :
            string += title
            break
    else:
        string += title + ", but not quite so brave as Sir Lancelot." 
    print string
```
