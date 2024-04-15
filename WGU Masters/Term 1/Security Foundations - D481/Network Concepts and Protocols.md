
# OSI

| Layer | Name         | Function                                                                                       |
| ----- | ------------ | ---------------------------------------------------------------------------------------------- |
| 7     | Application  | Provides network services directly to applications.                                            |
| 6     | Presentation | Transforms data to provide a standardized application interface and data encryption.           |
| 5     | Session      | Manages sessions between applications. Controls the dialogues (connections) between computers. |
| 4     | Transport    | Provides reliable data transfer. Manages error recovery and flow control.                      |
| 3     | Network      | Manages device addressing, tracks the location of devices on the network.                      |
| 2     | Data Link    | Provides node-to-node data transfer—a link between two directly connected nodes.               |
| 1     | Physical     | Transmits raw bit stream over the physical medium.                                             |


### OSI Model Study Notes

1. **Physical Layer (Layer 1)**:(hardware)
   - Concerned with transmission and reception of the unstructured raw data over a physical medium.
   - Deals with the electrical, mechanical, and procedural specifications to activate, maintain, and deactivate physical connections.

2. **Data Link Layer (Layer 2)**: (local)
   - Responsible for node-to-node deliverance and error detection and correction in the physical layer.
   - Introduces MAC addresses.

3. **Network Layer (Layer 3)**:(internet)
   - Responsible for transferring variable length data sequences from one node to another connected in different networks (routing).
   - Introduces IP addressing.

4. **Transport Layer (Layer 4)**: ( make a session using TCP)
   - Provides transparent transfer of data between end systems.
   - Responsible for end-to-end error recovery and flow control.
   - Ensures complete data transfer.

5. **Session Layer (Layer 5)**:
   - Manages sessions between end-user applications.
   - Establishes, manages, and terminates connections between applications.

6. **Presentation Layer (Layer 6)**:
   - Ensures that the data is in a usable format and is where data encryption occurs.
   - Translates data between the application layer and the network format.

7. **Application Layer (Layer 7)**:
   - Enables end-user software to communicate with other software.
   - Provides network services to the applications.
   - Examples include web browsers, email clients, and various types of servers.

## Detailed Encapsulation at Layers 2, 3, and 4 of the OSI Model

#### Layer 4: Transport Layer
- **Function**: Responsible for providing reliable, transparent transfer of data between end systems. This is where data is segmented and control information is added to enable error-free transmission.
- **Data Unit**: Segments (TCP) or Datagrams (UDP).
- **Encapsulation Details**:
  - **TCP**: Adds a header including source and destination port numbers, sequence numbers, acknowledgment numbers, flags, window size, and checksum. This is used for establishing connections, sequencing data, and error recovery.
  - **UDP**: Encapsulation includes source and destination port numbers and a simpler header structure, offering fewer features but lower overhead compared to TCP.
  - **Purpose**: Ensures that messages are delivered error-free, in sequence, and with no losses or duplications.

#### Layer 3: Network Layer
- **Function**: Handles the routing of the data (packets) across a network. Responsible for logical addressing, which involves determining the best path for data across networks.
- **Data Unit**: Packets.
- **Encapsulation Details**:
  - **IP Header**: Adds logical addressing information including source and destination IP addresses. May also include other fields like version, header length, differentiated services, total length, identification, flags, fragment offset, TTL (time to live), protocol (TCP, UDP, etc.), header checksum, and options.
  - **Purpose**: Delivers packets from the source host to the destination host solely based on the IP addresses in the packet headers. Routing and forwarding are functions of this layer.

#### Layer 2: Data Link Layer
- **Function**: Provides node-to-node data transfer—a link between two directly connected nodes. It handles framing, error checking, flow control, and MAC addressing.
- **Data Unit**: Frames. (MTU 1500Bytes max normal)
- **Encapsulation Details**:
  - **Ethernet Frame Structure**: Typically includes MAC addresses (source and destination), an Ethernet type field (indicating the network layer protocol used), the payload (packet from Network Layer), and a frame check sequence (FCS) for error checking.
  - **Purpose**: Ensures that data frames are directed to the correct device on a LAN using physical addresses. It corrects errors that may have occurred at the physical layer.

### Understanding Segments and Their Role in Data Transfer
- **Segmentation in the Transport Layer**: Involves breaking down data into manageable segments which are then encapsulated with headers that contain the information required to reassemble the data correctly at the destination.
- **Role**:
  - Facilitates efficient data transfer by breaking large data sets into smaller packets that can be managed and transported effectively over the network.
  - Enhances error recovery by only retransmitting the erroneous segments rather than the entire data stream.
  - Enables multiplexing of a single connection between the hosts to different services distinguished by port numbers.

This detailed encapsulation process at each layer ensures efficient, secure, and reliable transmission of data across complex networks. Each layer has a specific role and functions collaboratively to achieve seamless data communication between networked devices.


# Rj45  pin layout


| Pin Number | T568A Wiring (Straight-Through) | T568B Wiring (Straight-Through) | Crossover Cable (T568A to T568B) |
|------------|---------------------------------|---------------------------------|----------------------------------|
| 1          | Green/White                     | Orange/White                    | Orange/White                     |
| 2          | Green                           | Orange                          | Orange                           |
| 3          | Orange/White                    | Green/White                     | Green/White                      |
| 4          | Blue                            | Blue                            | Blue                             |
| 5          | Blue/White                      | Blue/White                      | Blue/White                       |
| 6          | Orange                          | Green                           | Green                            |
| 7          | Brown/White                     | Brown/White                     | Brown/White                      |
| 8          | Brown                           | Brown                           | Brown                            |


