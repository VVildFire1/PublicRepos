# Network Topology Study Sheet

Network topology refers to the layout of a network, including how nodes (like computers, printers, routers) and connections (like cables, Wi-Fi) are arranged. Each topology has its own structure and operational characteristics.

## Common Types of Network Topologies

### Bus Topology
- **Description**: All devices are connected to a single central cable, the bus.
- **Advantages**: Easy to implement and extend.
- **Disadvantages**: Limited cable length and number of stations; if the main cable fails, the entire network goes down.

### Star Topology
- **Description**: All devices are connected to a central hub. 
- **Advantages**: If one cable fails, only one node will be affected.
- **Disadvantages**: If the central hub fails, the entire network fails.

### Ring Topology
- **Description**: Each device has exactly two neighbors for communication purposes. All messages travel through a ring in the same direction.
- **Advantages**: Data packets travel at great speed.
- **Disadvantages**: A break in the ring (such as a failure in one of the nodes) can result in network failure.

### Mesh Topology
- **Description**: Devices are interconnected with many redundant interconnections between network nodes.
- **Advantages**: Provides high reliability and redundancy. If one path fails, another can be used.
- **Disadvantages**: Expensive to implement; requires more cable than the other topologies.

### Tree Topology
- **Description**: Group of star-configured networks connected to a linear bus backbone.
- **Advantages**: Supports future expandability of the network much better than a bus topology.
- **Disadvantages**: Heavily cabled; if the backbone line breaks, the entire segment goes down.

### Hybrid Topology
- **Description**: A combination of two or more different types of topologies.
- **Advantages**: Combines the strengths of various topologies.
- **Disadvantages**: Complex in design and may inherit weaknesses of the component topologies.

## Important Considerations

- **Scalability**: Some topologies are more scalable than others.
- **Fault Tolerance**: The ability to sustain network functionality in case of partial failure.
- **Cost**: The expense associated with the cabling and devices required for the topology.
- **Maintenance**: Consider the ease of diagnosing and repairing connectivity issues.

