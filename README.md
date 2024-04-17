# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
To write a python program to perform sliding window protocol.
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
Client:
```
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
c, addr = s.accept()

size = int(input("Enter number of frames to send: "))
frames = list(range(size))
window_size = int(input("Enter Window Size: "))
start = 0
i = 0

while True:
    while i < len(frames):
        end = min(start + window_size, len(frames)) 
        c.send(str(frames[i:end]).encode())
        ack = c.recv(1024).decode()
        if ack:
            print(ack)
        i += window_size
        start = end  
    break  
```

Server:
```
import socket
s = socket.socket()
s.connect(('localhost', 8000))
while True:
    data = s.recv(1024).decode()
    if not data: 
        break
    print(data)
    s.send("acknowledgement received from the server".encode())
```

## OUTPUT

![Screenshot 2024-04-17 104822](https://github.com/ThakshaRishi/2b_SLIDING_WINDOW_PROTOCOL/assets/144870423/87df7fc2-7c22-4759-a97c-89e64a53ce08)

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
