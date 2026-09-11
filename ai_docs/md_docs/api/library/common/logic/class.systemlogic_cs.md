# Unigine::SystemLogic Class (CS)


The *SystemLogic* class is used to control the logic of the application. Methods of this class are called after corresponding methods of the system script.


## SystemLogic Class

### Members

---

## virtual bool Init ( )

Engine calls this function on engine initialization. Similar to the system script's *init()* function.
### Return value

Returns true if there were no errors; otherwise, false.
## virtual bool Shutdown ( )

Engine calls this function on engine shutdown. Similar to the system script's *shutdown()* function.
### Return value

Returns true if there were no errors; otherwise, false.
## virtual bool Update ( )

Engine calls this function before updating each render frame. Similar to the system script's *update()* function.
### Return value

Returns true if there were no errors; otherwise, false.
## virtual bool PostUpdate ( )

Engine calls this function before rendering each render frame. Similar to the system script's *postUpdate()* function.
### Return value

Returns true if there were no errors; otherwise, false.
