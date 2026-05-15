# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM  
To implementation of Sliding Window Protocol
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
server2b.py
```
import socket 
 
s = socket.socket() 
s.bind(('localhost', 8000)) 
s.listen(1) 
 
print("Waitng for connecton...") 
conn, addr = s.accept() 
print("Connected to", addr) 
 
while True: 
    data = conn.recv(1024).decode() 
 
    if not data: 
        break 
 
    print("Frames received:", data) 
 
    ack = "ACK for " + data 
    conn.send(ack.encode()) 
 
conn.close() 

```
Client2b.py
```
import socket 
 
s = socket.socket() 
s.connect(('localhost', 8000)) 
 
n = int(input("Enter number of frames: ")) 
w = int(input("Enter window size: ")) 
 
frames = list(range(1, n+1)) 
i = 0 
 
while i < n: 
    send_frames = frames[i:i+w] 
 
    msg = " ".join(map(str, send_frames)) 
    print("Sending frames:", msg) 
 
    s.send(msg.encode()) 
 
    ack = s.recv(1024).decode() 
    print("Received:", ack) 
 
    i += w 
 
s.close() 

```
## OUPUT

<img width="1922" height="1030" alt="server2b" src="https://github.com/user-attachments/assets/6d5f8814-8ab6-4f79-9df6-bb1b6d4e87e6" />

<img width="1922" height="1030" alt="client2b" src="https://github.com/user-attachments/assets/8d3ed4d6-2e4e-4115-916b-05fc9442d786" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
