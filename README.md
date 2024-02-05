# Protocol
### Server Setup
- The server initializes Winsock and creates a TCP socket.
- It binds the socket to an IP address and port number, then listens for incoming connections.
- When a client connects, the server accepts the connection, creating a new socket dedicated to this client for communication.
- The server then waits to receive commands from the client.

### Client Setup
- The client also initializes Winsock and creates a TCP socket.
- It connects to the server by specifying the server's IP address and port number.
- Once connected, the client can send commands to the server.

### Communication
1. Connection Establishment:
   - Client connects to the server using the server's IP address and port number.
   - Server accepts the connection and establishes a dedicated socket for communication with this client.

2. Command Transmission:
   - The client sends commands to the server in the form of strings.
   - Commands can include operations like GET, LIST, PUT, and DELETE, followed by necessary arguments (e.g., filename).

3. File Transmission:
   - For file transfer operations (GET and PUT), data is sent in chunks using a buffer (1024 bytes in this case).
   - The server or client reads from or writes to a file in binary mode, transferring the file in segments until completion.

4. Command Processing:
   - The server parses the received command and determines the requested operation.
   - It performs the requested operation, such as sending a file list, transferring a file, or deleting a file, and sends appropriate responses back to the client.
  
### Available operations:
- PUT (send a file to the server): The client sends the PUT command followed by the filename. The file is read in chunks and sent to the server, which writes the received data to a file.
- GET (request a file from the server): The client sends the GET command followed by the filename. The server reads the requested file in chunks and sends it to the client, which then saves it locally.
- LIST (list files on the server): The client sends the LIST command. The server responds with a list of files available in the server's storage directory.
- DELETE (delete a file on the server): The client sends the DELETE command followed by the filename. The server then deletes the specified file and acknowledges the action.

### Examples of operations
1. Client sends `PUT filename`:
   - Client sends the command to upload a file.
   - Server receives the command, creates or opens the file, and writes incoming data to it.

2. Client sends `GET filename`:
   - Client requests a file from the server.
   - Server sends the requested file in chunks, which the client then writes to a local file.

3. Client sends `LIST`:
   - Client requests a list of files stored on the server.
   - Server compiles the list of files and sends it to the client.

4. **Client sends `DELETE filename`:
   - Client requests deletion of a specific file on the server.
   - Server deletes the file and confirms the deletion to the client.
