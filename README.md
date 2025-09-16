# 2a_Stop_and_Wait_Protocol
## AIM 
To write a python program to perform stop and wait protocol
## ALGORITHM
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
Client.py
```
NAME : SHOBANA.B
REG NO : 212224230262

import socket
import time

client = socket.socket()
client.connect(('localhost', 8000))
client.settimeout(5)  

while True:
    msg = input("Enter a message (or type 'exit' to quit): ")

    client.send(msg.encode())  

    if msg.lower() == 'exit':  
        print("Connection closed by client")
        client.close()
        break

    try:
        ack = client.recv(1024).decode()
        if ack == "ACK":
            print(f"Server acknowledged: {ack}")
    except socket.timeout:
        print("No ACK received, retransmitting...")
        continue  

```
Server.py
```
import socket

server = socket.socket()
server.bind(('localhost', 8000))
server.listen(1)
print("Server is listening...")
conn, addr = server.accept()
print(f"Connected with {addr}")

while True:
    data = conn.recv(1024).decode()

    if data:
        print(f"Received: {data}")
        conn.send("ACK".encode())

        if data.lower() == 'exit':  
            print("Connection closed by client")
            conn.close()
            break

```
## OUTPUT
Client:

<img width="710" height="312" alt="484522748-be86e64f-7d37-4664-95e8-345103e0d816" src="https://github.com/user-attachments/assets/049401ff-8522-4527-b781-09cac94dfb9f" />

Server:

<img width="701" height="194" alt="484522773-fbfd08ea-84cd-4fb5-b83a-e0087aa142e3" src="https://github.com/user-attachments/assets/13dedb0b-dbda-4969-9731-c0bfdd8c3e05" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
