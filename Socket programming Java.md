
# Socket programming

## prerequisites

- [[Networking basics]]
- Java

We can resume the process that two computers follow two communicate to each other, as a connection type transmission, or a connectionless (UDP) transmission.

 A connection type transmission works as a two-way channel, with a server, and a client that makes requests or receives from the server.

  This connection makes uses of the IP address of the device, and the specified port to which the communication channel is going to "connect" and where it expects a connection. A connection of this type makes uses of sockets, that are basically one-way endpoints that allow a communication channel between devices, but it requires that the client and server implement their own sockets.


As part of this learning I'm gonna implement a simple terminal chat that allows to users to send messages between them (a server, and a client).

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
	 -serverSocket:ServerSocket
	 -clientSocket:Socket
	 -output:PrintWriter
	 -input:BufferedReader

	+Server()
	
	+start(port:Integer):void

	+stop():void
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
	-clientSocket:Socket
	-output:PrintWriter
	-input:BufferedReader

	+Client()

	+startConnection(ip:String,port:int):void
	
	+sendMessageGetResponse(msg:String):String

	+stopConnection():void
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


## My own implementation: console_chat

We are gonna implement all of this in the console-chat project.
github: https://github.com/avm-x/console-chat

 The purpose of this project is to allow a communication channel between two users and a server, that is gonna act as a middleman to deliver messages to the other.

Apart from the classes above, I'm also gonna implement a custom Message class to make formatting easier.

### requisites

**Users:**
- Each user can terminate its endpoint writing "end" to the console.
- Each message shows the username of the sender, along with the time it was sent.

**Server:**
- Shows when a user stablish connection, and also when the two users are "connected".
- If an user end its side of the communication channel, it automatically closes
- Inspect messages for "end", so it can terminate the connection between the users


**Message Class**
```plantuml
Class Message {
	-username:String
	-localTime:LocalTime
	-msg:String

	+Message(username:String, msg:String)
	+Message(User user, msg:String)

	+toString():String
}

```


**User Class**
Its purpose its to make "easier" the interaction with the server through Client class

```plantuml
class User{
	-username:String
	-client:Client

	+User()
	
	+User(username:String)
	
	+getUsername():String
	
	+setUsername():void
	
	+getClient():Client
	
	+connectsTo():void
	
	+SendMessageGetResponse(msg:String):String
	
	+closeConnection():void
}
```


### Server and Users interactions

1._ Server init | users starts to connect


## My own implementation II: arithmetic_server


**Status** : **DONE** 
**Description:**
simple program where a user connects to the server, and sent arithmetic operations to get a result. Like "2+3" -> 5, also "+ 3 2" is also accepted. 

- github: https://github.com/avm-x/arithmetic_server


```plantuml
class ArithmeticOperations <<static>>{

	+sum(nums:List<Integer>):int
	+sum(nums:List<Double>):int
	
	+minus(nums:List<Integer>):int
	+minus(nums:List<Double>):int
	
	+multiply(nums:List<Integer>):int
	+multiple(nums:List<Double>):int
	
	+divide(nums:List<Integer>):int
	+divide(nums:List<Double>):int
}

```


## Handling multiple clients

Until now our server has ben a pretty simple server that can handle a single client, and if this client disconnects then it couldn't reconnect again, a pretty straightforward server. But now for our chat project we are gonna need a server that can handle multiple clients along with their i/o

**server**
- The server enters a loop where doesnt stop listening to each new request, and push them (clientHandler) into a List

- The same happens with the i/o chain, with respectives i/o Lists

**client**
- A normal client, nothing extra from the base point but the Thread extension of the class

**+clientHandler**
- Handle clients connections to the server creating a thread for each client.
- Is invoked in loop by the server for each new socket connection

## 040824 UPDATE:

Since i've started working with multiple clients i based my development on this mental model of three horizontally connected classes: Server, ClientHandler, Client. where ClientHandler was going to be a channel that would receive the input from the client and send it to the server, taking the output of the server, and send it to the client.

 But since I started working with a different model, one where ClientHandler is the operative arm of the server i've been able to implement my chat server project.  