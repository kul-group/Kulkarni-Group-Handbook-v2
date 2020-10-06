
## Programming

*Note: We have written a lot of useful code already in the group. Repurposing code from the group [github page](https://github.com/kul-group) can save you time.*

### Some Specific Guidelines for Writing Code

1. Naming: Make sure your names for variables are descriptive. `h_atom_dict` is better than `atom_dict` or `h_atoms`

2. Comments: Code is read more often than it is run. Comments should be extensive and clear. Imagine you are seeing this code for the first time, do the comments explain everything? Use docstrings for functions and classes.

3. Use Python's functionality to make code shorter, but don't overdo it. For example Python's list comprehension can help remove a `for` loop while still being readable. But, if you find yourself trying to combine several steps into a single line, stop. Break these steps over several lines and explain them with comments.

4. Start small, test, then build more. You may be confident that several lines of code you wrote will work as intended, but test them anyways. It is a nightmare to find a bug inside dozens of connected functions over hundreds of lines of code. Instead, build a small working part, then make sure it outputs what you expect on several test cases and make sure it integrates nicely with the rest of the program. Only then should you start writing something new.

5. Search for help, then ask for help. A lot of coding issues can be resolved by a websearch. If you are stuck, first search for solutions to your problem online. Usually this will resolve your issue within 20 minutes. If you are still stuck, it is important that you ask the group for help (this can save you a lot of time!). Message the group on Slack with your problem and attempted solutions. If that doesn't work, ask someone to look over your code with you, oftentimes a new person will be able to see what you are missing. 

### High Level Python Guidelines

Summarized from materials covered in ECS 32B.

Two Major Topics:

#### Object-oriented programming (OOP)
OOP is a coding style where we define both the type of the data structures and functions that can be applied to those data structures. This way of treating data structures as objects allows the programmers to build connections between different objects; for example, one inherits characteristics from another. Another advantage compared to sequential coding is that OOP enables programmers to dissect a problem into sections where we call them classes without constantly having to worry about the whole picture.

#### Data structures and algorithms
Understanding data structures, such as arrays, trees, heaps, graphs and Python built-ins, allows programmers to store information where it can be accessed efficiently (Beginner theorists may not be needing this as much as OOP)

Some Smaller Topics:

#### Debug & Unit testing
Pycharm has fancy debugging tools that allow programmers to step into the code and update all local variables after executing each line of code. Unit testing is an essential part of OOP since it helps to verify that the parts of the program (functions) do return results that match our expectations. For that reason, the test cases are usually written along with the program.

#### Type hinting
Type hints are hints that are given to the variables; for example, the inputs and outputs of a function, regarding their data types. It is useful especially when multiple programmers are working on the same project.

#### Inheritance
Objects with similar properties can inherit characteristics from the parent object without rewriting everything from the parent object. For example, different types of zeolite objects such as MFI inherits from the zeolite class. The child objects can also override the methods inherited from the parent.

### Outside References

https://david.goodger.org/projects/pycon/2007/idiomatic/handout.html

https://www.python.org/dev/peps/pep-0008/


For more general python advice type “import this” into your python command line.


