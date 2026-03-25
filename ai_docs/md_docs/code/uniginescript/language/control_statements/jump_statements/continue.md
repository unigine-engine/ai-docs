# Continue

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The *continue* keyword skips the rest of instructions of the current iteration of *for*, *forloop*, *foreach*, *foreachkey*, *while* or *do-while* loop. Code execution continues at loop condition evaluation and the beginning of the next iteration.


### Syntax


```cpp
continue;
```


### Example


```cpp
for(int i = 0; i < 5; i++) {
	if(i == 1 || i == 3) continue;
	log.message("%d ",i);
}

// the example displays the following: 0 2 4

```
