# pipe

Byte stream pipe abstractions for Acton.

The package provides a common `Pipe` interface and an in-process `ActorPipe`
implementation for connecting clients and mock servers in tests.

`actor_pipe_pair()` constructs an unconnected pair. Call
`connect_pipe_pair(pipes)` to connect both endpoints; writes made before
connection are buffered. This separates actor initial bindings from startup:

```acton
from pipe import actor_pipe_pair, connect_pipe_pair

actor Example():
    pipes = actor_pipe_pair()

    proc def __startup__():
        connect_pipe_pair(pipes)

    __startup__()
```

```sh
acton build
acton test
```
