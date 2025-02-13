https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3

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







https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
