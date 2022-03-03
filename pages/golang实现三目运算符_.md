title:: golang实现三目运算符?:

- #golang
- golang中实现c++中的三目运算符`a? b: c`
  ```c++
  if a ? b : c {
  	BLOCK1
  } else {
  	BLOCK2
  }
  
  ==>
  
  a is true  -> b is true -> BLOCK1
  		   -> b is false -> BLOCK2
  a is false -> c is true -> BLOCK1
  		   -> c is false -> BLOCK2
  
  if (a is true && b is true) || (a is false && c is true) -> BLOCK1
  else -> BLOCK2
  
  ==> 
  
  if (a && b) || (!a && c) {
  	BLOCK1
  } else {
  	BLOCk2
  }
  
  // 更复杂
  
  if d || (a ? b : c) {
  	BLOCK1
  } else {
  	BLOCK2
  }
  
  if d || ((a && b) || (!a && c) {
  	BLOCK1
  }  else {
  	BLOCK2
  }
  ```