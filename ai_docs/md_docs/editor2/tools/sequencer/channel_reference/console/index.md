# Console Command


A **Console Command** channel animates a console variable over time - the same variables you can type into the engine console by hand. Use it to drive an engine or debug setting that is only reachable through the console, and have it change on a schedule: dial a debug value up during a shot, or sweep a render setting across a cutscene.


![](console_command_channel.png)


## Choosing the Variable


Which variable the channel drives is set in the **Console Command** field of its properties panel. Pick one from the list of variables the engine knows, or type a name straight into the field.


![](choosing_console_variable.png)


The channel adapts to the variable you choose. So the keys you place match what the variable actually accepts, the same way its value types behave anywhere else (see the [Channels](../../../../../editor2/tools/sequencer/channels/index.md) article).
