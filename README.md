# pipe

Byte stream pipe abstractions for Acton.

The package provides a common `Pipe` interface and an in-process `ActorPipe`
implementation for connecting clients and mock servers in tests.

`actor_pipe_pair()` creates and connects a pair in one call.

For separate declarative initialization and startup, use
`create_actor_pipe_pair()` and `connect_actor_pipe_pair(pipes)`. Writes made
before connection are buffered:

```acton
from pipe import create_actor_pipe_pair, connect_actor_pipe_pair

actor Example():
    pipes = create_actor_pipe_pair()

    proc def __startup__():
        connect_actor_pipe_pair(pipes)

    __startup__()
```

```sh
acton build
acton test
```
