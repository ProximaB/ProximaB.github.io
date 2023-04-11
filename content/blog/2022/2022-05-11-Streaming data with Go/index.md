+++
title = "Streaming data with Go"
description = "Avoid unnecessary large memory allocations when processsing data"
draft = false

[taxonomies]
tags = ["go", "webdev"]

[extra]
feature_image = './lauren-george-WmD8EfNeyXE-unsplash.jpeg'
feature = true
link = ""
+++

![Streams](lauren-george-WmD8EfNeyXE-unsplash.jpeg)

## Streaming data with Go

In the world of web development, streaming data is a common requirement for applications to function efficiently. Whether it is transferring large files or processing real-time data from external services, streaming allows for seamless and faster data transfer. In this article, we will explore how to use Go for streaming data without the need for large memory allocation.

### Introduction to data transfer

Data transfer is the process of moving data from one location to another. In web development, data transfer can occur between a server and a client or between two services. The data can be in various formats, including text, images, audio, or video. The traditional approach to data transfer is to read the entire file into memory and then transfer it. However, this approach is not always feasible, especially for large files or real-time data.

### Basic example with io. file interface

When we transfer data between two endpoints, we usually send it in a single chunk. For instance, when downloading a file from the internet, we download the entire file in one go. The same thing happens when we read a file using Go's io package.

```go
file, err := os.Open("file.txt")
if err != nil {
    log.Fatal(err)
}
defer file.Close()

data, err := ioutil.ReadAll(file)
if err != nil {
    log.Fatal(err)
}
```

The above code reads the entire contents of the file.txt file into memory before processing it. This works well for small files, but can be problematic for large files.

### Concerns about performance and ways to optimize it

When dealing with large files, reading the entire file into memory can consume a lot of resources. This can lead to slow performance, high memory usage, and even crashes. To avoid these issues, we need to find ways to optimize the data transfer process.

One way to optimize the data transfer process is to use streaming. Streaming allows us to transfer data in small, manageable chunks. This can help reduce memory usage and improve performance.

### Why big memo allocation is bad thing

When we allocate a large amount of memory in one go, it can cause several problems. First, it can cause performance issues because allocating memory is an expensive operation. Second, it can lead to memory fragmentation, which can make it difficult to find contiguous blocks of memory.

### Streaming data using pipe

Go provides a convenient way to stream data using pipes. A pipe is a communication channel between two Go routines that can be used to transfer data.

```go
reader, writer := io.Pipe()

go func() {
    data := []byte("Hello, World!")
    _, err := writer.Write(data)
    if err != nil {
        log.Fatal(err)
    }
    writer.Close()
}()

buf := make([]byte, 1024)
n, err := reader.Read(buf)
if err != nil {
    log.Fatal(err)
}
fmt.Println(string(buf[:n]))
```

In the above code, we create a pipe using io.Pipe(). We then create a Go routine that writes data to the pipe and closes it. Finally, we read data from the pipe using reader.Read(). Since the data is streamed in small chunks, we can process it as it arrives without allocating a large amount of memory.

Streaming Data from Another Service to Client Over TCP with Splice

We can also use pipes to transfer data between two endpoints over a network. For instance, if we have a server that produces data and a client that consumes it, we can use pipes to transfer the data over TCP.

```go
serverConn, err := net.Dial("tcp", "localhost:8000")
if err != nil {
    log.Fatal(err)
}
defer serverConn.Close()

clientConn, err := net.Dial("tcp", "localhost:9000")
if err != nil {
    log.Fatal(err)
}
defer clientConn.Close()

go func() {
    _, err := io.Copy(serverConn, clientConn)
    if err != nil {
        log.Fatal(err)
    }
}()

_, err = io.Copy(clientConn, serverConn)
if err != nil {
    log.Fatal(err)
}
```

In the above code, we create two TCP connections, one for the server and one for the client. We then use io.Copy() to transfer data between the two endpoints. Since the data is streamed using pipes, we can process it as

### Streaming data from another service to client over tcp with splice

Using pipes, we can read and write data to and from files, network connections, and other I/O sources in a way that minimizes memory allocation, as we don't need to store the entire contents of the data in memory before processing it. This is especially important for working with large files or streaming data over a network, where we want to minimize memory usage and reduce the risk of running out of memory.

To illustrate this, let's take an example where we need to transfer data between two services over a TCP connection. We could do this using the io.Copy() function in the Go standard library, which allows us to copy data from one io.Reader to one io.Writer. However, this approach requires that we allocate a buffer to hold the data being transferred, which can be a problem if we're working with large files or streaming data continuously.

Instead, we can use the splice() system call to transfer data directly between the two connections without needing to allocate a buffer. The splice() system call allows us to efficiently transfer data between two file descriptors (e.g., network connections or files) without the need to copy the data into user space. This can greatly reduce the amount of memory needed to transfer data, and can improve performance by reducing the number of system calls needed to complete the transfer.

Here's an example of how we can use splice() to transfer data between two network connections in Go:

```go
func transferData(src net.Conn, dst net.Conn) error {
    // Create a buffer to hold data temporarily
    buf := make([]byte, 64*1024)
    
    // Loop until there's no more data to transfer
    for {
        // Use splice to transfer data from the source connection to the destination connection
        n, err := syscall.Splice(
            int(src.(*net.TCPConn).File().Fd()), // File descriptor for the source connection
            nil,
            int(dst.(*net.TCPConn).File().Fd()), // File descriptor for the destination connection
            nil,
            len(buf), // Maximum amount of data to transfer
            0,
        )
        if err != nil {
            return err
        }
        
        // If we've reached the end of the stream, return nil to indicate that the transfer completed successfully
        if n == 0 {
            return nil
        }
    }
}
```

In this example, we're using the syscall.Splice() function to transfer data between the two network connections. The src and dst parameters are both net.Conn objects representing the source and destination connections, respectively.

We're also using a buffer to temporarily hold data as it's being transferred between the connections. In this example, we're using a buffer size of 64KB, but you can adjust this value to match your specific use case.

Once we've set up our buffer and connections, we enter a loop that repeatedly calls syscall.Splice() to transfer data between the connections. The len(buf) parameter specifies the maximum amount of data to transfer in each call to splice(), which helps to prevent excessive memory usage.

If splice() returns a value of 0, that means we've reached the end of the data stream and we can break out of the loop. If splice() returns an error, we return that error to the calling function.

By using splice() to transfer data between the connections, we can minimize memory allocation and improve performance, making it an ideal approach for streaming data in Go.

### Conclusion

In this article, we've explored how to stream data in Go without allocating large amounts of memory. We've looked at using pipes and the io.Copy() function to read and write data, and we've seen how to use the splice() system call to transfer data between two network connections without allocating a buffer. By minimizing memory usage, we can improve performance and reduce