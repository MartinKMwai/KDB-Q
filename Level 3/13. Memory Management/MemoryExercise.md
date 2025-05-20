# Memory Exercises

### Exercise 1
Output used memory using the appropriate .Q function
```q
// your code here

.Q.w[][`used]
```


### Exercise 2
Output heap memory using the appropriate function
```q
// your code here

.Q.w[][`heap]
```


### Exercise 3
Use .Q.w with .z.ts to track the memory usage of a q process in 10 second intervals. Store the results in a table called memUsage with columns time, bytesUsed and peak.
```q
// your code here

memUsage:([time:`timestamp$()] bytesUsed:`int$(); peak:`int$())
```

```q
.z.ts:{`memUsage insert (.z.p;.Q.w[][`used]; .Q.w[][`peak])};
```
```q

\t 10000
```

### Exercise 4
Create a table called newTrade with 10,000,000 rows and columns time, sym, price, size and suitable data for each. Using a pen and paper –estimate how much memory this should use up. 
```q
// your code here
n : 10000000

newTrade:([]time: 9 +n?8t; sym: n?`AAPL`GOOG`FD`KX`JPM`MS; price:n?200.00; size: n?500j)



```
### Exercise 5
Check how much memory was actually used using memUsage.
```q
// your code here

memUsage
```

### Exercise 6
Check the size of the table in bytes using appropriate internal function(!)
```q
// your code here
-22!newTrade

```


### Exercise 7
Create a second table called newerTrade:newTrade. Check the memory again. What has happened?
```q
// your code here
newerTrade:newTrade

```

```q
memUsage //nothing much, because all we did was create a reference to an existing dataset
```
### Exercise 8
Set garbage collection mode as deferred using the appropriate system command.
```q
// your code here

\g 0
```
### Exercise 9
Delete newerTrade from your workspace. What effect does this have?
```q
// your code here

delete newerTrade from `.
//not much change, just deleted a reference to newTrade, which still exists
```

```q
memUsage
```
### Exercise 10
Run .Q.gc[]. What effect does this have?
```q
// your code here

.Q.gc[]

```

```q
memUsage
//nothing much, 2nd reference still exists, so no memory returned.
```

### Exercise 11
Delete newTrade from your workspace. Then run .Q.gc[] again. What effect does this have now?
```q
// your code here

delete newTrade from `.;
.Q.gc[];
```
```q


-5#memUsage //memory returned since last existing reference is removed
```
### Exercise 12
Define a function ```tilFunc``` that multiplies x by a list of y length incrementing from 0-y
```q
// your code here

tilFunc:{[x;y] x * til y};


tilFunc[10;10]
```


### Exercse 13
Create a table ```.prof.events``` with columns func (type symbol) and time (type timespan)
```q
// your code here

.prof.events:([]func:`$(); time:`timespan$());

.prof.events
```

### Exercise 14
Define a function ```.prof.time``` that:
* takes 2 arguments f and a where f= function and a= arguments
* runs input function with input arguments
* adds a new record to the .prof.events table with function name and time taken to execute
```q
// your code here

.prof.time:{[func;arg] s:.z.p; r: func . arg; `.prof.events upsert (func;.z.p-s) ;r}; 

```

 ### Exercise 15
 Run .prof.time with function tilFunc created in Exercise 13 with varying arguments. 
 
 Check the output of .prof.events - time taken and captured in table should vary according to type of arguments passed.
```q
// your code here

.prof.time [`tilFunc;(9;10)];
.prof.time [`tilFunc;(100;500)];
.prof.time [`tilFunc;(10;79)];
 
 .prof.events
```



