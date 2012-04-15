# Methods and Modules

[Back To Flow
Control](http://github.com/thehackerwithin/UofCSCBC2012/tree/master/2c-PythonFlowControl/)
- [Forward To Local Version
Control](http://github.com/thehackerwithin/UofCSCBC2012/tree/master/3a-VersionControlLocal/)

* * * * *

**Presented By : Joshua R. Smith**

**Original material by Milad Fatenejad**

At this point, we've been over the basics of the python language except for the parts that allow you to reuse code you and others have written. First we will talk about wirting methods (sometimes called functions), then we'll talk about modules. A very important topic that we unfortunately won't have time to cover is classes (aka, object orientation). Dive Into Python has an excellent chapter on this topic that you should read.

## Methods

Lets say you frequently want to calculate a list of values of power given a list of voltages and a list of currents. You could continually drop the for loop we wrote before into your code, but this approach quickly becomes unwieldy and error prone. The solution is to abstract this functionality into a method. Here's how.

```python
def calcpower(voltageList, currentList):
  powerList = [] # Initialize an empty list to be filled later.
  indxList = range(len(currentList))

  for indx in indxList:
    power = voltageList[indx] * currentList[indx]
    powerList.append(power)

  return powerList
```

That's it: just a block containing the code we already wrote plus one extra line. The return statement at the end tells python that when the method is done executing, hand back the value of powerList.

You can call this method at any point in the following way:

```python
calcpower(voltageList, currentList)
```

In fact, we've been using methods almost this entire time:

```python
len()
type()
"string!".upper()
```

and so on.

We just looked at one way to construct a method; there are more. Lets say we wanted to write the ugliest method ever that calculates and returns a value raised to a power. (In fact, this method already exists, so writing a new one is a terrible idea). Here's how it would look:

```python
def topower(base,expt):
  product = 1
  for indx in range(expt):
    product = product * base

  return product
```

Seriously though, don't ever use the above code.

What if most of the time we were just squaring a number? We'd want a default value of 2 for the exponent.

```python
def topower(base,expt = 2):
  product = 1
  for indx in range(expt):
    product = product * base

  return product
```

In this case, we are setting the default value to 2. We can change that value when we call the command, but we don't always need to set it to 2.

## Modules

Modules are a way to package code for reuse at a later time. You can buld your own modules, install others' modules, or use built-in modules provided from python.

Lets do the exponents right. It turns out that python ships with a math module containing exactly that functionality. Here's how you bring it in to your environment.

```python
import math
```

Now we can do exponents, say 3^2

```python
math.pow(3,2)
```

How about 2^4?

```python
math.pow(2,4)
```

Writing a method to create this functionality was a terrible idea because the math module already exists. The math module has other methods like sine, cosine, exp, and so on.

There are other ways to pull from modules into your environment. If you only wanted the sine method, you could import it like so

```python
from math import sin
```

and you'd be able to directly use it without a dot.

```python
sin(3)
```

If you want to pull in everything from the math module, but you're too lazy to type out "math" all the time, you can give the module an alias

```python
import math as mth
```

or whatever you want the alias to be.

One final way to import stuff is to use the asterisk notation. This approach is almost always a terrible idea, so you probably shouldn't do it.

```python
from math import *
```

It is a terrible idea because you dump all of the names of data and methods into your local namespace. If you already have data or methods of the same name, you can end up facing some nasty problems.

# Fin

So that wraps up the python lessons. Please take a look at the resources I mentioned at the top of the first lesson for some really excellent information.

## Exercise

Write a program that will pull the data from the data.dat file into a dictionary that looks like the dict we made in lesson 2. This task seems trivial, but its a little harder than it looks.