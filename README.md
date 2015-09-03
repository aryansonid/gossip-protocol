# gossip
Go implementation of the Gossip protocol.

This package provides an implementation of an eventually consistent in-memory
data store. The data store values are exchanged using a push-pull gossip protocol.

```
// Create a gossiper
g := NewGossiper("<ip>:<port>", <unique node id>)
// Add peer nodes with whom you want to gossip
g.AddNode("<peer_ip>:<peer_port>")
...
// update self values 
g.UpdateSelf("<some_key>", "<any_value>")
```

These values are exchanged using the gossip protocol between the configured
peers.

```
// Get the current view of the world
storeKeys = g.GetStoreKeys()
for _, key := range storeKeys.List {
	nodeInfoList := g.GetStoreKeyValue(key)
	for _,  nodeInfo := nodeInfoList.List {
		// node_info_list is an array, to be indexed
		// by node id. Valid nodes can be identified
		// by the following:
		//    node_info.Status != types.NODE_STATUS_INVALID
	}
}

// Stop gossiping
g.Stop()
```
