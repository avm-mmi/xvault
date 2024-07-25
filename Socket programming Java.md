
# Socket programming

## prerequisites

- [[Networking basics]]
- Java

We can resume the process that two computers follow two communicate to each other, as a connection type transmission, or a connectionless (UDP) transmission.

 A connection type transmission works as a two-way channel, with a server, and a client that makes requests or receives from the server.

  This connection makes uses of the IP address of the device, and the specified port to which the communication channel is going to "connect" and where it expects a connection. A connection of this type makes uses of sockets, that are basically one-way endpoints that allow a communication channel between devices, but it requires that the client and server implement their own sockets.


As part of this learning i'm gonna implement a simple terminal chat that allows to users to send messages between them (a server, and a client).

- Each user can terminate its side of the connection writing "end"
- Each message shows the name of the user and maybe the time, like this:
	`Jane_doe[13:03]: hello world`
	`Jane_doe: hello world`



## Start!

First we are gonna need the net library that takes care of low-level communication details between the client and the server (net), and also a library to handle the input/output streams
```java
import java.net.*;
import java.io.*;
```

### Basic server
 ```plantuml
 class Server {
	 ServerSocket serverSocket
	 Socket clientSocket
	 printWriter output
	 BufferedReader input

	Server()
	
	start(Integer port): void

	stop(): void
 }
 ```

#### Why `printWriter` class for output and `BufferedReader` class for input?

They simplified to us the task that is printing and receiving/formating messages, they make use of their respective i/o stream.
- A stream is like a river, in this case, a river of data, a continuous flow of data that we process byte to byte, as the data is process sequentially. 
#### start(Integer port)
The `start(Integer port)` method is in charge of generating a connection with a client socket. To do this, we initialize the *serverSocket*, and initialize our *clientSocket* with `serverSock.accept()`,
```java
this.serverSocket = new ServerSocket(port);
this.clientSocket = this.ServerSocket.accept();
```

then we initialize our outputs and inputs streams

```java
this.output = new PrintWriter(clientSocket.getOutputStream(), true);
        
this.input = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
```

### stop()
This method is in charge of closing all open resources

```java
this.input.close();
this.output.close();
this.clientSocket.close();
this.serverSocket.close();

```

### Basic client

```plantuml
class Client{
	Socket clientSocket
	PrintWriter output
	BufferedReader input

	Client()

	startConnection(String ip, int port): void
	
	sendMessageGetResponse(String msg) : String

	stopConnection() : void
}
```


#### startConnection(String ip, int port)
This method is in charge of initializing the variables needed for client
```java
this.clientSocket = new Socket(ip, port);
this.output = new PrintWriter(clientSocket.getOutputStream(), true);
this.input = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
```
#### sendMessageGetResponse(String msg)
This method is in charge of sending a message, and reading the possible answer to it

```java
output.println(msg);
String response = input.readLine();
return response;
```

#### stopConnection()
This method is in charge of closing all the opened resources

```java
this.input.close();
this.output.close();
this.clientSocket.close();
```
