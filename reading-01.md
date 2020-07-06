# Debugging for beginners

### Debugging: run your code step by step in a debuggin tool like Visual Studios to determine the exact spot that a mistake exists in. You can then make changes so one can continue to run a program.

##### One needs to ask themselves questions first before getting into debugging: What was the code supposed to do, what happened instead, and what type of error message did you get.

##### Make sure to examine your assumptions. Check basic stuff like are you using the right API, typos in the code, pulling data the correct way, etc.

##### Go into debugging mode to find where problem occured.

##### In Visual Studio, press F5 or Debug - Start Debugging to get into this mode. Use breakpoints in the debugger to give yourself a chance to see your code more clearly. 

##### Make a breakpint by putting the cursor on a line and pressing F9.

##### See Debugging page for example: https://docs.microsoft.com/en-us/visualstudio/debugger/debugging-absolute-beginners?view=vs-2019


# Try/Catch Blocks

### Place code statements that could raise or throw an exception in a try block, and place statements used to handle the exception or exceptions in one or more catch blocks below the try block. Each catch block includes the exception type and can contain additional statements needed to handle that exception type.

##### See example that uses above info at: https://docs.microsoft.com/en-us/dotnet/standard/exceptions/how-to-use-the-try-catch-block-to-catch-exceptions


# Exception Handling

### Statements

##### Statements are program instructions. With few exceptions, statements are executed in sequence. 

##### Category	C# keywords
###### Selection statements	if, else, switch, case
###### Iteration statements	do, for, foreach, in, while
###### Jump statements	break, continue, default, goto, return, yield
###### Exception handling statements	throw, try-catch, try-finally, try-catch-finally
###### Checked and unchecked	checked, unchecked
###### fixed statement	fixed
###### lock statement	lock


# Try Statements and Expressions

### Try Statement: specifies a code block subject to cleanup or error handler code

##### Try block must have catch block after it (or a finally block, or both)

##### Catch executes when error occurs and finally executes after you leave the try block, whether an error happened or not.

##### Catch blocks have an exception object that has error info. Catch blocks can either fix the error or rethrow the exception. You only do the latter if you want to log a problem, or want a new high level exception type.

##### Finally blocks are always executed by the CLR (good for cleanup tasks like closing network connections)

##### Example: 
###### try
###### {
######  ... // exception may get thrown within execution of this block
###### }
###### catch (ExceptionA ex)
###### {
######  ... // handle exception of type ExceptionA
###### }
###### catch (ExceptionB ex)
###### {
######  ... // handle exception of type ExceptionB
###### }
###### finally
###### {
######  ... // cleanup code
###### }

##### When an exception is thrown, the CLR performs a test. A question then: is the execution currently within a try statement that can catch the exception?

##### If yes: execution is passed to compatible catch block. If catch block finishes executing, execution moves to next place outside try statement (and does finally block if its there)

##### If no: execution jumps back to the caller of the function, and test repeats

### Catch Clause

##### Catch Clause: specifies what type of exception to catch. Has to be system.exception or a subclass of it.

##### This catches all possible errors

##### Only one catch clause executes for a given exception. If you want to include a safety net to catch more general exceptions you must put more specific handlers first.

##### Exception filter: add this by using the WHEN clause.

### Finally block

##### A finally block always executes—whether or not an exception is thrown and whether or not the try block runs to completion. 

##### They are used for cleanup code.

##### A finally block executes either:
###### After a catch block finishes
###### After control leaves the try block because of a jump statement (e.g., return or goto)
###### After the try block ends
##### Things that stop finally blocks are an infinite loop, or the process ending abruptly

##### Using statement: provides an elegant syntax for calling Dispose on an IDisposable object within a finally block.

##### Exceptions can be thrown either by the runtime or in user code.

##### They can also appear as an expression in expression-bodied functions

##### List of common exception types on 165-166.


# Therac-25

### This was a radiation therapy machine from the 80s that was infamous for giving overdoses of radiation. This was proven to be due to overconfidence leading to software bugs that caused the overdoses.

##### Root causes were that the company did not have software code independently reviewed, did not consider software design when deciding how the machine should work and show failure messages, and the system only showed the word malfunction, but did not stop the x-ray beam.

##### They also never tested the software and hardware together, which is crazy.


# Ariane 5

### It's a heavy lift space launch vehicle

##### It once had an issue with data conversion: a conversion from a 64-bit floating point value to a 16-bit signed integer caused a processor trap because the first value was too large to be represented by the latter. Variables were not protected by handlers as a result of a bad port from Ariana 4. 

##### This led to failures in launch several times.