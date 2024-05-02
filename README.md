# ESCnet Protocol
Description of the ESCnet protocol.

> Warning - this is work-in-progress and is / will be changed frequently until stable version is released.

# Basics
Structure of ESCnet assumes that the network is divided like a tree into 3 (4) components:
- Zone, global region (continents)
- Net, local region (city, state)
- Node, a server
- Point, a user on a node (not a member of ESCnet)

All of those are represented with a number and stored in this format:
> zone:net/node(.point)
If point is not specified, it is assumed to be 0 (node's system operator - sysop).

Each zone and net has their "zero" server that is used as a gate between zones, nets and nodes.

# Netmail and echoconferences
ESCnet is made to serve metmail (direct messages) between users and allow them to participate in echoconferences (echoes), which are similar to netmail, but everyone can see messages in it. Echoes can be public or local - available only to some nodes / nets / zones.

Any user (point) can write a message to an echo, and it should be immediately available to other points on the same node.

Other points on other nodes cannot yet see the message, because it wasn't yet synced to their node. For this to happen, the synchronisation between nodes needs to occur.

# Synchronization
Nodes can be linked together manually by their sysops, and they will be synchronized automatically really quick (every 7 minutes if new netmail / echo messages are available).

Otherwise, nodes will sync with their net once each 15 minutes. Nets will sync with other nets every 20 minutes, and will sync with zones every 20 minutes. Zones will sync with other zones each 20 minutes.

But, as you may have noticed, this configuration only works in one-way - from the bottom nodes of the ESCnet to the top nodes (uplinks of the bottom nodes).

This won't allow for messages to actually get to their destinations, so there is also a downlink synchronisation in place:
- Zones will sync with nets every 20 minutes;
- Nets will sync with nodes every 15 minutes.

All these "every N minutes" aren't aligned to some global time to prevent all members of ESCnet from trying to synchronize at the same time and effectively DDoSing the whole infrastructure.

# Uplinks and downlinks
Uplinks of a node are nets. Optionally, nodes may serve as up/down-links to each other.
Uplinks of a net are zones and other nets. Downlinks are nodes and other nets.
Uplinks of a zone are other zones. Downlinks are nets and other zones.

# Discovery
Nodes, nets and zones will discover each other from a global nodelist:

WIP
