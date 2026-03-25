# Break

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The *break* keyword terminates execution of the current iteration of the *for*, *forloop*, *foreach*, *foreachkey*, *while* or *do-while* loop. It also terminates execution of the *switch-case* blocks. Code execution continues with the first line of the code that goes after the loop or the *switch-case* block.


### Syntax


```cpp
break;
```


### Example


```cpp
for(int i = 0; i < 10; i++) {
	if(i == 3) break;
		log.message("%d ",i);
}

// the output of the example is: 0 1 2

```
