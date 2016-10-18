# Lecture 6

## Reasons for designing and documenting software architectures 

By designing the system in terms of a high-level system design
as well in modules, you, among other things, make communication with stakeholders 
easier, since it paints a clearer picture of how the system works.
It also allows for earlier design decisions and large scale reuse of modules
from similar systems.

## Analysis and sythesis of a system

Start imagining a "virtual system". Divide this into "virtual modules", and then design
these. Through design, implementation and testing these are now "concrete modules".
Finally, you have a "concrete system".

## Software architecture styles

### Client-Server

Clients need to be aware of the server, and initiate communication to it.

There are different kinds of client-server architectures.

- __Two-Tier, Thin-client__: Client handles presentation layer, while server
handles business layer and data management. This has the disadvantages of
being heavy on the server and requiring significant network traffic.

- __Two-Tier, Fat-client__: Client handles both presentation and
business layer, and the server handles only data management. This distributes
the workload on clients, but it's more difficult to update the software since the 
clients handle bigger parts of it.

- __Three-Tier__: This involves a client, handling the presentation layer, middleware 
to handle the business layer and a server to handle data management. This efficiently
maps each software layer to different pieces of hardware and makes it easy to load-balance.

### Layers

Simply abstraction layers. In a purely layered system, each layer can only immediately access
the layer below.

The advantages of this setup include the layers being easier to reuse and standardize, 
dependencies being kept local and incremental development and testing is supported.

This approach could however lead to performance penalties. Also, if there is _layer bridging_,
that is, if a high-level layer can access a layer lower than the closest one, it causes 
some modularity to be lost.

