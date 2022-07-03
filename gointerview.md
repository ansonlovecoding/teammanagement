# Golang面试题
***\*1. What is a package in a Go program?\****

A package (pkg) is a directory in the Go workspace that contains Go source files or other packages. Every function, variable and type in the source file is stored in the linked package. Every Go source file belongs to a package, which is declared at the top of the file with the following command:

package<packagename>

You can import and export packages to reuse exported functions or types using:

import<packagename>

Golang's standard package is fmt, which contains formatting and printing functions like Println().

 

***\*2. What is a Goroutine? How do you stop it?\****

A Goroutine is a function that runs concurrently with other functions. Goroutines can be considered lightweight threads managed by the Golang runtime. To create a Goroutine, you only need to add the keyword “go” before the function;

There are the following ways to stop a goroutine:

1. Accurate control of goroutines is accomplished with the help of the channel's close mechanism;

2. With the help of a semaphore, poll the channel regularly, and judge whether to close the channel through the semaphore;

3. Use the context of the Golang to control and close the goroutine

 

***\*3. What is Channel and what is its role?\****

Channel is a core type in Golang, you can think of it as a pipe, through which concurrent core units can send or receive data for communication;

In the Golang, memory sharing is achieved not through shared memory, but through communication. Go's CSP (Communicating Sequential Process) concurrency model is implemented through goroutines and channels.

 

***\*4. What are the characteristics of the Channel?\****

1. Send data to a nil channel will be blocked forever

2. Receive data from a nil channel will be blocked forever

3. Sending data to a closed channel will cause panic

4. Return a value of zero if the buffer is empty when receiving data from a closed channel

5. Unbuffered channels are synchronous, while buffered channels are asynchronous

6. closing a nil channel will panic

 

***\*5. Talk about parameter passing and reference types in Golang\****

All parameters in Golang are passed by a value which is a copy. Because the copied content is sometimes a non-reference type (int, string, struct, etc.), the original content cannot be modified in the function. Some are reference types (pointer, map, slice, chan, etc.), so you can modify original content data

Golang's reference types include slice, map, and channel. They have complex internal structures, and in addition to allocating memory, they also need to initialize related properties. The built-in function “new” calculates the size of the type, allocates zero-valued memory for it, and returns a pointer. And make will be translated by the compiler into a specific creation function, which allocates memory and initializes member structures, and returns objects instead of pointers

 

***\*6. Talk about the GC of Golang\****

After Golang 1.5, the "non-generational, non-moving, concurrent, three-color" mark-clearing garbage collection algorithm is adopted.

GC in golang is basically the process of mark-clearing:

The GC process is divided into four stages:

1. Stack scan (STW at the beginning)

2. First mark (concurrency)

3. Second Mark (STW)

4. Clear (concurrent)

The memory occupied by each object applied in the entire process space can be regarded as a graph. In the initial state, each memory object is marked in white color:

1. First STW, do some preparatory work, such as enabling the write barrier. Then cancel the STW, and immediately enqueue the scan task as multiple concurrent goroutines to the scheduler, and then be processed by the CPU

2. In the first round, scan the root object, including the global pointer and the pointer on the goroutine stack, mark it as gray color, and put it in the queue

3. In the second round, the object referenced by the object in the first step queue is grayed out and added to the queue. After all, objects referenced by an object are grayed out and added to the queue, the object can be turned black and taken out of the queue. The cycle repeats, and when the final queue is empty, the remaining white memory space of the entire graph is the unreachable object, that is not referenced;

4. The third round is STW again, marking (gray) the memory applied for by the newly added objects in the second round. Here, a write barrier is used to record

 

***\*7. What is the GPM scheduling model\****

Goroutine can have a strong concurrency implementation through the GPM scheduling model:

1. M: represents a kernel-level thread, one M is one thread, and a goroutine runs on top of M; M is a large structure that maintains a small object memory cache (mcache), currently executing goroutines, and random number generation device, etc.

2. G: represents a goroutine, which has its own stack, instruction pointer, and other information (waiting channels, etc.) for scheduling.

3. P: The full name of P is Processor. Its main purpose is to execute goroutines, so it also maintains a goroutine queue, which stores all the goroutines that need it to execute.

 

 

***\*8. Talk about the process of TCP connection and disconnection (three-way handshake and four waves)\****

TCP connection process:

In the TCP/IP protocol, the TCP protocol provides reliable connection services, and uses a three-way handshake to establish a connection. The process is as follows:

1. The first handshake: When the connection is established, client A sends an SYN packet (SYN=j) to server B, and enters the SYN_SEND state, waiting for server B to confirm.

2. The second handshake: Server B receives the SYN packet, and must confirm the SYN of client A (ACK=j+1), and also sends an SYN packet (SYN=k), so is the SYN+ACK packet, at this time Server B enters the SYN_RECV state.

3. The third handshake: Client A receives the SYN+ACK packet from server B, and sends an acknowledgment packet ACK (ACK=k+1) to server B. After the packet is sent, client A and server B enter the ESTABLISHED state and complete the three handshakes.

After completing the three-way handshake, the client and server begin to transmit data.

 

TCP disconnection process:

Since TCP connections are full-duplex, each direction must be closed individually, as follows:

1. Client A sends a FIN to close the data transfer from client A to server B.

2. Server B receives this FIN, and it sends back an ACK, confirming that the sequence number is the received sequence number + 1. Like SYN, a FIN will occupy a sequence number.

3. Server B closes the connection with client A and sends a FIN to client A.

4. Client A sends an ACK message confirmation and sets the confirmation sequence number to the received sequence number + 1.

 

***\*9. Talk about what aspects of the MySQL index need to pay attention to\****

1. Do not use functions and operations on columns;

2. Try to avoid using negation operators such as "!=" or "not in" or "<>";

3. Try to avoid using "or" to connect conditions;

4. Multiple single-column indexes are not the best choice. MySQL can only use one index, and will select the most restrictive index from multiple indexes;

5. The compound index follows the "leftmost prefix" principle, that is, the index is used only when the first field of the compound index is used in the query condition;

6. The benefits of covering indexes: If an index contains the values of all the fields that need to be queried, the data can be returned directly according to the query results of the index without reading the table, which can greatly improve the performance. Therefore, it is possible to define an extra column to be included in the index, even if this column is useless for the index;

7. The impact of range query on the multi-column query: if a column in the query has a range query, all columns on the right side of the query cannot be searched using index optimization;

8. The index will not contain columns with NULL values;

9. The impact of implicit conversion: when the types on the left and right sides of the query condition do not match, the implicit conversion will occur. The impact of implicit conversion may cause the index to fail and perform a full table scan;

10. The index failure problem of the left fuzzy matching "%###" in the like statement;

 

***\*10. The difference between coroutine, thread, and process\****

1. Process

A process is a running activity of a program with a certain independent function on a certain data set, and a process is an independent unit for the system to allocate and schedule resources. Each process has its own independent memory space, and different processes communicate through inter-process communication. Because the process is relatively heavy and occupies independent memory, the switching overhead between context processes (stack, register, virtual memory, file handle, etc.) is relatively large, but it is relatively stable and safe.

2. Thread

A thread is an entity of a process and the basic unit of CPU scheduling and dispatching. It is a basic unit smaller than a process that can run independently. Threads basically do not own system resources themselves, but only have a few resources that are essential in operation. (such as the program counter, a set of registers, and stacks), but it can share all the resources owned by the process with other threads belonging to the same process. Communication between threads is mainly through shared memory, context switching is fast, and resource overhead is less, but compared to processes, it is less stable and easy to lose data.

3. Coroutines

A coroutine is a lightweight thread in user mode, and the scheduling of the coroutine is completely controlled by the user. A coroutine has its own register context and stack. When the coroutine is scheduled to switch, save the register context and stack it to other places. When switching back, restore the previously saved register context and stack, and directly operate the stack without the overhead of kernel switching, and you can access global variables without locking, so the context switch is very fast

 

***\*11. Why is single-threaded redis so fast\****

1. Pure memory operation

2. The single-threaded operation, avoiding frequent context switching

3. Using a non-blocking I/O multiplexing mechanism

 

***\*12. What is a non-blocking I/O multiplexing mechanism\****

Non-blocking IO is very simple. Set it to non-blocking mode through fcntl (POSIX) or ioctl (Unix). At this time, when you call read, if there is data received, it will return the data, and if no data is received, it will return immediately An error like EWOULDBLOCK. This will not block the thread, but you still have to constantly poll to read or write.

Therefore, we need to introduce the concept of IO multiplexing. Multiplexing refers to using a thread to check the ready status of multiple file descriptors (Socket), such as calling the select and poll functions, passing in multiple file descriptors, and returning if one file descriptor is ready, otherwise block until timeout. After getting the ready state, the real operation can be executed in the same thread, or you can start the thread execution (such as using a thread pool)

 

***\*13. What is a Docker container?\****

Docker containers create abstractions at the application layer and package the application and all its dependencies together. This allows us to deploy applications quickly and reliably. Containers don't require us to install a different OS. Instead, they use the CPU and memory of the underlying system to perform tasks. This means that any containerized application can run on any platform, regardless of the underlying operating system. We can also think of a container as a runtime instance of a Docker image.

 

***\*14. What are the characteristics of MongoDB?\****

1. MongoDB is a document storage-oriented database, which is relatively simple and easy to operate.

2. You can set the index of any attribute in the MongoDB record (eg: FirstName="Sameer",Address="8 Gandhi Road") to achieve faster sorting.

3. You can create data mirroring locally or through the network, which makes MongoDB more scalable.

4. If the load increases (more storage space and stronger processing power are required), it can be distributed among other nodes in the computer network which is called sharding.

5. Mongo supports rich query expressions. Query commands use JSON-style markup to easily query objects and arrays embedded in documents.

6. MongoDB can use the update() command to replace the completed document (data) or some specified data fields.

7. Map/Reduce in MongoDB is mainly used for batch processing and aggregation operations on data.

8. Map and Reduce. The Map function calls emit(key, value) to traverse all the records in the collection, and passes the key and value to the Reduce function for processing.

9. Map function and Reduce function are written in Javascript and can execute MapReduce operation through DB "runCommand" or "mapreduce" command.

10. GridFS is a built-in feature in MongoDB that can be used to store a large number of small files.

11. MongoDB allows scripts to be executed on the server-side You can write a function in Javascript and execute it directly on the server-side. You can also store the definition of the function on the server-side and call it directly next time.

 

***\*15. What can ELK do?\****

In the operation and maintenance of massive log systems, ELK components can be used to solve:

1. Distributed Centralized query and management of log data, troubleshooting

2. System monitoring, including monitoring of system hardware and application components

3. Security Information and Incident Management

4. Quickly search data

 

***\*16. What does a microservice architecture look like?\****

Microservices can be regarded as the splitting of large projects, which are generated under the need for rapid iterative deployment. New functional modules are published as new service components, which work together with other published service components. There are multiple producers and consumers inside the service, which are usually called in the form of HTTP rest, and the service is generally presented to customers in the form of one (or several) services.

Microservice architecture is an idea. We do not have a clear definition of microservice architecture, but in short, microservice architecture is:

A set of services is used to build an application. Services are independently deployed in different processes. Different services communicate through some lightweight interaction mechanisms, such as RPC, HTTP, etc. Different services can even be implemented in different programming languages and maintained by independent teams

Microservice architecture design typically includes:

1. Service fuse downgrade current limiting mechanism

2. Service registration discovery

3. Gateway

4. Distributed lock

5. Load Balancing

6. Logging

 

***\*17. What are the implementation methods of distributed locks?\****

Usually distributed locks are implemented as separate services. There are three commonly used distributed lock implementations:

1. Implement distributed locks based on databases.

2. Implement distributed locks based on caches (Redis, Memcached).

3. Implement distributed locks based on Zookeeper.

 

***\*18. How can the performance of the API be optimized?\****

1. The amount of data is relatively large, and the data is stored in batches

2. Consider asynchronous processing for time-consuming operations

3. Proper use of caches

4. Optimize program logic, code

5. SQL optimization

6. Compressed transmission content

7. Consider using other methods such as Redis/file/MQ for temporary storage, and then put in DB asynchronously

8. Discuss with the product the most appropriate and simple way to implement the requirements

 

***\*19. What is the principle of the Quicksort?\****

Quicksort is a sorting algorithm developed by Tony Hall. On average, sorting n items requires Ο(nlogn) comparisons. In the worst case, Ο(n2) comparisons are required, but this is not common;

Quick sort is another typical application of the divide and conquers idea in the sorting algorithm. In essence, quick sort should be regarded as a recursive divide and conquer method based on bubble sort;

Algorithm steps:

1. Pick out an element from the sequence, called a "pivot";

2. Reorder the sequence. All elements smaller than the reference value are placed in front of the reference, and all elements larger than the reference value are placed at the back of the reference (the same numbers can go to either side). After the partition exists, the benchmark is in the middle of the sequence. This is called a partition operation;

3. Recursively sort the subarrays of elements smaller than the reference value and the subarrays of elements larger than the reference value;

 

***\*20. What is a red-black tree? What are the characteristics?\****

The red-black tree is called a symmetric binary B-tree, and its main feature is to add an attribute to each node to represent the color of the node, which can be red or black. The red-black tree is essentially a binary search tree, and it introduces 5 additional constraints:

1 Node can only be red or black.

2 The root node must be black.

3 All NIL nodes are black.

4 Two adjacent red nodes cannot appear on a path.

5 In any recursive subtree, all paths from the root to the leaf contain the same number of black nodes.

 
