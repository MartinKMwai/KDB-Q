# Debugging Exercises - with Solutions

### Exercise 1
Add printing to the first two expressions in the following function using display ```0N!```
```
func1:{a:1+x; b:a*100; c:neg b}
```
```q
//your code here 
func1:{a:1+x; 0N! string[.z.p], "|| finished the addition of x";
       b:a*100; 0N! string[.z.p], "|| finished the generation of b";
       c:neg b; 0N! string[.z.p], "|| finished the negation of b";
       0N! string[.z.p], "|| Function complete, returning c";
       c}
       
func1[10]
```

### Exercise 2
Define 2 functions that will print single argument ```x``` in 2 ways. What do you notice being different?
* printString0 using ```0N!``
* printString1 using ```-1```

*Add a semicolon at the end of both functions inside the lambda*

```q
//your code here 
printString0:{0N!x*x;}


printString1:{-1 string[x*x];}




printString0[10]

printString1[5]
```


### Exercise 3
Identify where the error is in the following statement using both Quick Debugger or q interpreter (q console outside of KX Developer, rememeber you can use Terminal from Jupyter for this) to investigate the error. We recommend you do both to see the difference!

```q
g:{a:x*2;a+y}
func2:{g[x;2#y]}
func2[3;4] // previously func2[3;`four]
// open the above in scratchpad to use quick debugger
```

### Exercise 4
Identify where the error is in the following statement by:
```
func3:{a:til 10;b:4#neg a;c:upper b;d:sum c}
```
* adding print statements to each expression
```q
//your code here 

func3:{a:til 10;b:4#neg a;c:upper b;d:sum c;}
```
* Using Quick Debugger to identify errror
```q
// your ans here 
```
* Now that you have identified the error, remove the failing expression and redefine ```func3```

*Hint: you will get another new error - repeat steps above to resolve it also*
```q
// your ans here 
func3:{a:til 10;b:4#neg a;d:sum b}
func3[]

```

### Exercise 5
Define a function called triple that:
* Accepts 1 argument (int) and multiplies by 3
```q
// your ans here 
triple:{x*3}
```
Using trap ```@``` evaluate the function twice:
* First time passing the int 10 and getting result of 30
* Second time pass the symbol `ten - result returned should be an Error message saying "Function has returned an error: type". Pass error string to trap function assuming we do not know which error will be returned.
```q
// your ans here
@[triple;10;{"Error: ",x}]
@[triple;`ten;{"Error: ",x}]

```

### Exercise 6
Define a function called adding that:
* Accepts 3 argument (ints) and adds them together
```q
// your ans here
adding:{[arg1;arg2;arg3] arg1+arg2+arg3}
```
Using trap ```.``` evaluate the function three times
* Once passing 3 arguments (4 ;5; 10) getting result of 19
* Second time passing 4 arguments (4 ;5; 10; 2). Result returned should be an Error message saying "Function has returned an error: rank"
* Third time pass (4;5;`ten) with the symbol `ten as third argument. Result returned should be an Error message saying "Function has returned an error: type"

*Only thing that should be changed each time is the arguments passed*
```q
// your ans here
.[adding;(4 ;5; 10);{"The function has returned an error: ", x}]
.[adding;(4 ;5; 10; 2);{"The function has returned an error: ", x}]
.[adding;(4;5;`ten);{"The function has returned an error: ", x}]
```

### Exercise 7 
Taking triple function from Exercise 6 use ```.Q.trp``` in place of ```@``` and modify the error message to show backtrace as well as error string.

Ensure output is in readable form.
```q
// your ans here
.Q.trp[triple;`ten;{2@"Function has returned an error: ",x,.Q.sbt y}]
```

### Exercise 8
Given func4:
```
func4:{a:x*x; b:y*y; a+b}
```
pause execution before the last expression in the function, insert undefined any name here ' break is commonly used.

*Hint: Make sure the name you choose is not defined in local or global scope.*
```q
// your ans here
func4:{a:x*x; b:y*y; break; a+b}
func4[10;2]
```

Try this same exercise using the q interpreter to compare how the debugger differs! What would you expect to see there?
