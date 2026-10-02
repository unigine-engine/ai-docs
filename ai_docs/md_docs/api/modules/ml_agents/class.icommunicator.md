# MLAgents::ICommunicator Class


ICommunicator is the transport between the session and an external trainer. It carries the observations out and the actions back, one exchange per step of the decision loop.


The built-in implementation is **[TrainerCommunicator](../../../api/modules/ml_agents/class.trainercommunicator.md)**, which speaks the demo's open gRPC protocol. Implement this interface and hand it to **[Session::setCommunicator()](../../../api/modules/ml_agents/class.session.md)** to connect a trainer of your own over some other transport.


An exchange does not have to finish within the call. A communicator that reports **supportsAsync()** is driven through **exchangeBegin()** and **exchangePoll()** instead, so the engine keeps running while the trainer thinks.


### Exchange Results


| Value | Meaning |
|---|---|
| OK | The actions have arrived and can be applied |
| PENDING | The exchange is still in flight; poll again next step |
| RESET | The trainer asks for every episode to start over |
| QUIT | The trainer is done and the application should close |
| DISCONNECTED | The connection is gone; the behaviors fall back to what they can run on their own |


### See Also


- **[MLAgents::TrainerCommunicator](../../../api/modules/ml_agents/class.trainercommunicator.md)**
- **[MLAgents::Session](../../../api/modules/ml_agents/class.session.md)**


## ICommunicator Class

---

## virtual isConnected ( ) =0

Returns a value indicating if the communicator currently has a trainer connected.
### Return value

true while a trainer is on the other end; otherwise, false.
## virtual void onBehaviorRegistered ( ) =0

Called when a behavior registers with the session, so the trainer learns what observations and actions it has.
### Arguments

## virtual exchange ( ) =0

Sends the pending observations and waits for the actions to come back.
### Arguments

### Return value

Outcome of the exchange.
## virtual supportsAsync ( )

Returns a value indicating if this communicator can exchange without blocking the loop.
### Return value

true if the exchange can be split into a begin and a poll. Returns false unless overridden.
## virtual void exchangeBegin ( )

Starts an exchange without waiting for it to finish. Implemented by communicators reporting **supportsAsync()**.
### Arguments

## virtual exchangePoll ( )

Checks whether the reply to an exchange started by **exchangeBegin()** has arrived.
### Arguments

### Return value

PENDING while the reply has not arrived yet, otherwise the outcome of the exchange.
## virtual void shutdown ( ) =0

Closes the connection and releases whatever the transport holds.
