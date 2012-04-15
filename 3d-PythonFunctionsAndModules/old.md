# Python 4 : Functions and Standard Modules

[Back To Flow
Control](http://github.com/thehackerwithin/UofCSCBC2012/tree/master/2c-PythonFlowControl/)
- [Forward To Local Version
Control](http://github.com/thehackerwithin/UofCSCBC2012/tree/master/3a-VersionControlLocal/)

* * * * *

**Presented By : Joshua R. Smith**

**Original material by Milad Fatenejad**

During the last session we saw how to use some of the built-in data
types. During this session, we are going to learn about writing
functions and using modules.

# Using modules

Python has a lot of useful data type and functions built into the
language. We've see some of these already, and we'll see more over the
next few lectures. For a full list, you can type
\`dir(\_[\_builtins](____________________________________________________________________))\`.
However, most of the useful function are stored in modules. An example
is the sine function, which is stored in the math module. In order to
access mathematical functions, like \`sin\`, we need to ''import'' the
math module. Lets take a look at a simple example:

```python
> print sin(3)    # Error! Python doesn't know what sin is...yet
> import math     # Import the math module
> print math.sin(3)
> print dir(math) # See a list of everything in the math module
> help(math)      # Get help information for the math module
```

It is not very difficult to use modules - you just have to know the
module name and import it. There are a few variations on the import
statement that can be used to make your life easier. Lets take a look at
an example:

```python
> from math import *  # import everything from math into the global namespace (A BAD IDEA IN GENERAL)
> print sin(3)        # notice that we don't need to type math.sin anymore
> print tan(3)        # the tangent function was also in math, so we can use that too
```

```python
> reset                 # Clear everything from IPython
> from math import sin  # Import just sin from the math module. This is a good idea.
> print sin(3)          # We can use sin because we just imported it
> print tan(3)          # Error: We only imported sin - not tan
```

```python
> reset                 # Clear everything
> import math as m      # Same as import math, except we are renaming the module m
> print m.sin(3)        # This is really handy if you have module names that are long
```

# A running example

The goal of this lecture is to use Python to read a series of strings
from the command line, convert them into numbers, and list whether they
are prime. A single run of this program will look like this:

    (unix shell)$ python findPrimes.py 2 4 3 9 7
    2 is prime
    4 is not prime
    3 is prime
    9 is not prime
    7 is prime

We'll split this problem into a few pieces: 1) Process the command line
arguments using the sys module. 2) Write a function to determine whether
a number is prime. 3) Combine the two and test it.

# Writing Python Scripts

Python scripts are simply files ending in ".py" that contain python
instructions. You can write them using any text editor such as emacs,
vi, nano, notepad, etc... If you don't have a text editor you like to
use to write computer programs then you are in luck because it turns out
that all of you installed a decent and easy to use python editor called
IDLE. So far, we have been feeding commands directly to the python
interpreter, ipython. This starts to become very tedious once we want to
write longer programs. So from now on we are going to write python
scripts instead using IDLE. You can run the scripts you wrote using the
"%run" command in ipython.

To open IDLE in Windows, simply use the run box in the start menu and
enter "idle". Similarly on Mac OSX enter "idle" into spotlight, or enter
"idle" into a terminal if you are on Linux. Once idle is open, click on
File -\> New Window to start a new python script. For the rest of this
session I will assume that you are saving the scripts to the Desktop.
Enter the command: print "Hello World!" into the new script then save it
to the Desktop with the name "hello.py". Now, we have to move ipython to
the Desktop using the commands "cd" followed by "cd Desktop". You can
now run the script by entering "%run hello.py" in ipython. We'll learn
more about writing python files ourselves in the next session.

**Aside: IDLE** IDLE can do a lot more that write simple python scripts.
It contains its own python interpreter, so you can run python scripts
directly within IDLE by hitting f5. It also contains a debugger. We're
not going to use these features in this boot camp - instead we will
write the scripts in IDLE and run them in ipython since we are already
familiar with it. However, running writing and running scripts in IDLE
has its advantages and I encourage you to learn more about it.

# Using the sys module

The sys module gives you access to the Python interpreter. Some
important objects in this module are: 1) sys.argv is a list of command
line arguments. The first argument is always the name of the file. 2)
sys.path gives a list of all paths on your computer where Python will
look for modules 2) sys.modules gives a dictionary of all currently
loaded modules.

Put the following text in a file findPrimes.py in your current working
directory.

```python
''' findPrimes.py
List whether the numbers passed in the command line are prime.
'''

from sys import argv

for i in xrange(1,len(argv)):
    print argv[i]
```

This program should print each input on its own line.

**Hands on example**

How could you alter the for loop to not use xrange and element indexing?

Now, let's work on the next piece of the program, which is a function to
compute whether a number is prime. To do that, we'll need to detour to
talk about functions in general.

# Using Functions

The keyword "\`def\`" is used to define a function. As in the case of
conditionals and loops, whitespace is used to define the body of a
function. Try entering the following into iPython:

```python
> def triangle_perimeter(a, b, c):
>    return a + b + c
> 
> p = triangle_perimeter(3,4,5)
> print p
```

Python functions can return multiple values:

```python
def rgb(color_name):

    if color_name is "red":
       return 1,0,0
    if color_name is "green":
       return 1,0,0
    if color_name is "blue":
       return 1,0,0
    if color_name is "yellow":
       return 1,1,0

    print "ERROR: Unknown color"

 r,g,b = rgb("yellow")
 print r,g,b
```

**Hands-on Example**

Write a function, "\`perimeter\`" that takes one argument - a tuple
containing the lengths of each side of a polygon. Have the function
return the perimeter of the polygon. So, for example to find the area of
a square with side length 3, the function call would be:
perimeter((3,3,3,3)) and the function would return 12. Use the \`help\`
and \`dir\` functions to figure out how to write this function in one
line.

## Variable Number of Arguments

In the last example, you wrote a function, called \`perimeter\`, that
you have to call like this:

```python
print perimeter((1,2,3,4,5))
```

You need the extra set of parentheses, because the function takes only
one argument - a single tuple. Wouldn't it be nice if we didn't have to
have the extra parentheses? It turns out that this is easy in python:

```python
def perimeter(\*args):
   return sum(args)

print perimeter(1,2,3,4,5)
```

Notice that little star on the first line. That star tells python to
take all of the arguments and bundle them into a single tuple called
args. This feature allows us to create functions that take a variable
number of arguments. The function calls do not require the extra set of
parentheses we saw earlier.

**Hands-on Example**

Write a function that takes a variable number of floating point
arguments and returns their average.

## Keyword Arguments

Consider the following function, whose arguments represent the model
year, mileage, and number of accidents that a car has had. The function
attempts to use this information to compute the value of the car.

```python
def carvalue(year, mileage, nacc):
   return 30000 - mileage/10 - nacc*1000 - (2010-year)*1000

print carvalue(2001, 100000, 2)
```

In order to use the \`carvalue\` function, we have to remember that
\`year\` is the first argument, \`mileage\` is the second, and \`nacc\`
is the third. If we accidentally put the wrong argument in the wrong
place then we will compute the wrong answer. Luckily, we can be explicit
when calling functions using the following syntax:

```python
print carvalue(year=2001, mileage = 100000, nacc=2)
print carvalue(mileage= 100000, year = 2001, nacc=2) # Also produces the correct answer!
print carvalue(2001, nacc= 2, mileage = 100000) # Sets the year to 2001, the mileage to 100000, and nacc to 2
print carvalue(year= 2001, mileage = 100000, 2) # ERROR: Keyword arguments must precede non-keyword arguments
```

## Default Value Arguments

Suppose I did a study that showed that the average number of car
accidents a particular vehicle experienced was two. Now I want to modify
the \`carvalue\` function so that if the user doesn't know the number of
accidents, the function will use two by default. I can do this by
providing a default value in the function definition.

```python
def carvalue(year, mileage, nacc=2):
   return 30000 - mileage/10 - nacc*1000 - (2010-year)*1000

print carvalue(2001, 100000, 2) # Works just like before
print carvalue(2001, 100000) # Since nacc is not specified, it defaults to 2
```

You cannot mix default value arguments and variable numbers of arguments
in the same function.

# Back to Prime Numbers

Let's write a function in findPrimes.py to find prime numbers. Recall
that a prime number is a number that has no divisors other than 1 and
the number itself. In the code below, I'm using the sqrt function, which
can be imported from the math module.

```python
def isPrime(n):
  ''' Return True iff a number is prime. '''

  if n <= 0:
     return False
  if n <= 2:
     return True

  if n % 2 == 0:
    return False

  cntr = 3 # The first odd divisor is 2.
  stopPoint = sqrt(n)
  while cntr <= stopPoint:
     if n % cntr == 0: return False
     cntr += 2

  return True
```

**Hands on example** Devise a few tests for this function. Are there any
special cases you've forgotten? Are there any checks for data validity
that we should add?
