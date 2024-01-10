TCP (Transmission Control Protocol) 

TCP is a connection-oriented protocol that provides reliable, ordered, and error-checked delivery of data packets over an IP network. It guarantees that data sent from one device is received correctly by the destination device. TCP achieves this reliability through mechanisms like acknowledgement, retransmission, and flow control. It breaks data into smaller packets, assigns sequence numbers to them, and ensures they are reassembled correctly at the receiving end. TCP is widely used for applications that require guaranteed delivery, such as web browsing, email, file transfer, and remote login.

UDP (User Datagram Protocol) 



The three-way handshake is a process used by TCP to establish a connection between two devices.

![[WireShark_Syn_Packet.png]]

1. SYN (Synchronize): The initiating device  This packet indicates the desire to establish a connection and includes an initial sequence number.

2. SYN-ACK (Synchronize-Acknowledge): This packet acknowledges the receipt of the initial SYN packet and also includes its own initial sequence number.

3. ACK (Acknowledge): This packet confirms the establishment of the connection and typically contains an incremented sequence number.

[[Ports]]
