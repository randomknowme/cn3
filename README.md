https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
# Question A
### Go-Back-N ARQ

We all know that the **Data Link Layer (DLL)** in the **OSI model** is responsible for the **flow and error control** of the data that is sent from sender to receiver. This flow and error control mechanism follows some set of rules/protocols. We will be discussing **flow control protocols** in this article.

## Flow Control Protocols

The flow control protocols are generally divided into two categories:

- **Stop and Wait Protocol**
- **Sliding Window Protocol**

The difference between these two categories of flow control protocols is:
- In the **Stop and Wait Protocol**, only one data frame is sent at a time from sender to receiver.
- In the **Sliding Window Protocol**, multiple frames can be sent at a time from sender to receiver.

## Go-Back-N ARQ

**Go-Back-N ARQ** is a **sliding window protocol** used for **flow control** purposes. Multiple frames present in a single window are sent together from sender to receiver.

**Pipelining** is allowed in the **Go-Back-N ARQ protocol**. Pipelining means sending a frame before receiving the acknowledgment for the previously sent frame.

In this article, we will discuss all the important concepts related to the **Go-Back-N ARQ protocol** in detail.

### Sender Window and Receiver Window in Go-Back-N ARQ Protocol

The **sender window** is a **fixed-sized window** that defines the number of frames that are transmitted from sender to receiver at once. The integer ‘N’ in the **Go-Back-N** represents the frame size.

For example, in **Go-Back-4 ARQ**, the size of the sender window is **4**.
![sender-window-and-receiver-window (1)](https://github.com/user-attachments/assets/113f2709-6e3c-4a29-b58f-64857e71035e)
The Receiver window in the Go Back N ARQ protocol is always of size 1. This means that the receiver takes at most 1 frame at a single time.

# packet loss

# Packet Loss in Go-Back-N ARQ
![image](https://github.com/user-attachments/assets/94fbeb7c-5b2c-41a2-a032-6dbd9f506b43)
1. **Sender transmits frames 0, 1, 2, 3, and 4 sequentially** to the receiver, following the sliding window approach.
2. **The receiver successfully acknowledges frames 0, 1, and 2**, moving the window forward.
3. **Frame 3 and 4 are transmitted, but frame 5 is lost (indicated by the red 'X')** due to an error in the transmission channel.
4. **The sender waits for an acknowledgment (ACK) for frame 3, 4, and 5**, but since frame 5 is lost, the receiver never acknowledges it.
5. **After a timeout**, the sender **goes back** to the last unacknowledged frame (frame 3) and **retransmits frames 3, 4, and 5 again**, even if frames 3 and 4 were correctly received before.
6. **The receiver discards previously received frames after the lost packet** because Go-Back-N ARQ only accepts frames in order.
7. **Once retransmitted, the receiver successfully receives the frames in order and acknowledges them**, allowing the sender to proceed with new frames.
## **Steps for ACK Loss in Go-Back-N ARQ**

# **ACK Loss in Go-Back-N ARQ**

## **Steps for ACK Loss in Go-Back-N ARQ**
1. **The sender transmits frames 0, 1, 2, 3, and 4 sequentially** to the receiver.
2. **The receiver successfully receives a frame and sends an acknowledgment (ACK) back** to the sender.
3. **However, the ACK gets lost in transmission** (e.g., the acknowledgment for frame 2 is lost).
4. Since the sender **does not receive an acknowledgment for frame 2**, it assumes that **frame 2 was lost** (even though the receiver has it).
5. **After the timeout period**, the sender **retransmits frame 2** (even though the receiver already has it).
6. **The receiver receives the duplicate frame 2 but discards it** because it was already correctly received before.
7. The receiver **sends a new acknowledgment (ACK 3)** for the next expected frame.
8. The sender **resumes normal transmission from frame 3 onwards**.
![Sliding_SET_2-3](https://github.com/user-attachments/assets/e66c2cdb-6d2a-438d-aead-4e60b272ceea)

# **Premature Timeout or Packet Delay in Go-Back-N ARQ**

## **1. What is Premature Timeout?**
Premature timeout occurs when the **sender's timer expires too early**, even though the receiver has already received and acknowledged the frame. This causes **unnecessary retransmissions**, leading to inefficiencies in the protocol.

### **Steps for Premature Timeout in Go-Back-N ARQ:**
1. **The sender transmits frames 0, 1, 2, 3, and 4** sequentially.
2. **The receiver successfully receives and acknowledges a frame** (e.g., ACK 2 is sent for frame 2).
3. **However, due to network congestion or processing delays, the ACK does not reach the sender before the timer expires.**
4. The sender **assumes the frame was lost** and **retransmits frame 2 unnecessarily**.
5. The receiver **discards the duplicate frame 2** since it has already received it.
6. The receiver sends an **ACK again** for the next expected frame.
7. The sender **resumes normal transmission after receiving the delayed ACK**.
![gobackn automatic repeat request_send window](https://github.com/user-attachments/assets/654065bb-aa8d-4948-a7ad-8465ad627d9f)

---

## **2. What is Packet Delay?**
Packet delay occurs when **a data frame or acknowledgment (ACK) is delayed** due to network congestion or processing delays. This can **cause unnecessary retransmissions** if the sender’s timer expires before receiving the delayed ACK.

### **Steps for Packet Delay in Go-Back-N ARQ:**
1. **The sender transmits frames 0, 1, 2, 3, and 4**.
2. The receiver **receives frame 2 and sends ACK 2**.
3. **ACK 2 gets delayed in the network**.
4. The sender **does not receive ACK 2 before the timer expires** and **wrongly assumes frame 2 is lost**.
5. The sender **retransmits frame 2**.
6. The receiver **discards the duplicate frame 2** but still acknowledges it.
7. Eventually, the **delayed ACK 2 arrives at the sender**, but by then, the unnecessary retransmission has already occurred.
![Sliding_SET_2-1](https://github.com/user-attachments/assets/61b214e5-ae38-4326-ba0a-607565c27fa6)

---
# Question B

!!!!!!!!!!!!!!!!!!!!!!! see which is there in q3 and write accordingly 
Demultiplexing – 
Delivering received segments at the receiver side to the correct app layer processes is called demultiplexing. 
 
Network-Assisted Conventional Control (NACC) is a control approach that integrates conventional control methods with network-based assistance to enhance system performance. It utilizes communication networks to exchange real-time data, enabling better coordination, remote monitoring, and adaptive control. This approach improves efficiency, reduces delays, and enhances the reliability of control systems in applications like industrial automation, smart grids, and autonomous systems.
---

---




https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
