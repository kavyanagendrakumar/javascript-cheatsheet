## Variable scope, closure 
Read this(important) - https://javascript.info/closure 
JavaScript is a very function-oriented language. 

**Closure** - Usually, a function remembers where it was born(created) in the special property [[Environment]]. It references the Lexical Environment from where it’s created. 

**Function Creation**
When a function is created, it remembers the lexical environemtn it was created in and stores in internal property called [[Environment]]

**Function Runtime**
When a function is executing, before it executes a lexical environment is created for it's execution. 
Lexical Env has 
1. Environment record - which contains local variables, this.
2. Pointer to Outer Lexical environment which it gets when it's created([[Environment]]). 

## For loop
For generates a new lexical environment with it's own variable. So, function generated inside for loop in every iteration refrences it's own i, from that very iteration. (Remember this for closures)
