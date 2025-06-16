## Variable scope, closure 
Read this(important) - https://javascript.info/closure 
JavaScript is a very function-oriented language. 

**Closure** - Usually, a function remembers where it was born(created) in the special property [[Environment]]. It references the Lexical Environment from where it’s created. 

## For loop
For generates a new lexical environment with it's own variable. So, function generated inside for loop in every iteration refrences it's own i, from that very iteration. (Remember this for closures)
