
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

1. **Physical Layer (Layer 1)**:
   - Concerned with transmission and reception of the unstructured raw data over a physical medium.
   - Deals with the electrical, mechanical, and procedural specifications to activate, maintain, and deactivate physical connections.

2. **Data Link Layer (Layer 2)**:
   - Responsible for node-to-node deliverance and error detection and correction in the physical layer.
   - Introduces MAC addresses.

3. **Network Layer (Layer 3)**:
   - Responsible for transferring variable length data sequences from one node to another connected in different networks (routing).
   - Introduces IP addressing.

4. **Transport Layer (Layer 4)**:
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


