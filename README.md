# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM
### SERVER
```
import socket

port = 60000
s = socket.socket()
host = socket.gethostname()

s.bind((host, port))
s.listen(5)
print("Server is listening...")

while True:
    conn, addr = s.accept()
    print('Got connection from', addr)

    data = conn.recv(1024)
    print('Server received:', repr(data))

    filename = 'mytext.txt'
    with open(filename, 'rb') as f:
        l = f.read(1024)
        while l:
            conn.send(l)
            print('Sent', repr(l))
            l = f.read(1024)

    print('Done sending.')
    conn.close()
    print('Connection closed.\n')
```

### CLIENT
```
import socket

s = socket.socket()
host = socket.gethostname()  # or use server IP if on different system
port = 60000

s.connect((host, port))
print("Connected to server.")

# Optional greeting
s.send("Hello server!".encode())

with open('received_file', 'wb') as f:
    while True:
        print('Receiving data...')
        data = s.recv(1024)
        if not data:
            break
        f.write(data)

print('Successfully received the file.')
s.close()
print('Connection closed.')
```

## OUPUT
### SERVER:
<img width="953" height="296" alt="image" src="https://github.com/user-attachments/assets/7dd768a7-719a-40eb-8606-7b61d1ae9600" />

### CLIENT:
<img width="937" height="342" alt="image" src="https://github.com/user-attachments/assets/0daf1adb-d110-41d2-940c-2474fdf626c4" />


## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
