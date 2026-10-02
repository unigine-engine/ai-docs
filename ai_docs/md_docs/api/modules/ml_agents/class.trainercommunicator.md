# MLAgents::TrainerCommunicator Class

**Inherits from:** ICommunicator


TrainerCommunicator is the built-in connection to an external trainer: it speaks the demo's open gRPC protocol, offers the registered behaviors, and exchanges observations for actions on every step of the decision loop.


The session creates and owns one on its own when the application is started with the *--trainer-port* command-line option, so this class is rarely constructed by hand. Build one yourself only to drive the connection on your own terms - a different port policy, or a trainer started after the world is already running.


The exchange is asynchronous: the engine hands over a batch and keeps running until the reply arrives, rather than blocking the loop on the trainer.


### See Also


- **[MLAgents::ICommunicator](../../../api/modules/ml_agents/class.icommunicator.md)**
- **[MLAgents::Session](../../../api/modules/ml_agents/class.session.md)**


## TrainerCommunicator Class

---

## TrainerCommunicator ( )

Creates a communicator bound to the given session. The connection itself is opened by **connect()**.
### Arguments

## connect ( )

Connects to a trainer listening on the given port.
### Arguments

### Return value

true if the trainer answered; otherwise, false.
## virtual isConnected ( )

Returns a value indicating if the connection is up.
### Return value

true while the trainer is connected; otherwise, false.
## virtual void onBehaviorRegistered ( )

Offers a newly registered behavior to the trainer.
### Arguments

## virtual exchange ( )

Sends the pending observations and waits for the actions to come back.
### Arguments

### Return value

Outcome of the exchange.
## virtual supportsAsync ( )

Returns a value indicating that this communicator exchanges without blocking the loop.
### Return value

Always true.
## virtual void exchangeBegin ( )

Starts an exchange and returns immediately.
### Arguments

## virtual exchangePoll ( )

Checks whether the reply to the exchange in flight has arrived.
### Arguments

### Return value

PENDING while the reply has not arrived yet, otherwise the outcome of the exchange.
## virtual void shutdown ( )

Closes the connection to the trainer.
