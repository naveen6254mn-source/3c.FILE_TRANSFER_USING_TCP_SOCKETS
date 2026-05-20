# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
## NAME : NAVEEN M
## REGISTER NO: 212225230197
## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM
server:
```
import socket

port = 60000
s = socket.socket()

host = socket.gethostname()

s.bind((host, port))
s.listen(5)

while True:
    conn, addr = s.accept()

    data = conn.recv(1024)
    print("Server received", repr(data))

    filename = "cntext.txt"

    try:
        with open(filename, 'rb') as f:
            l = f.read(1024)

            while l:
                conn.send(l)
                print("Sent", repr(l))
                l = f.read(1024)

        print("Done sending")

    except FileNotFoundError:
        conn.send("File not found".encode())
        print("cntext.txt does not exist")

    conn.close()
```
Client:
```
import socket
s = socket.socket()
host = socket.gethostname()
port = 60000
s.connect((host, port))
s.send("Hello server!".encode())
with open('received_file.txt', 'wb') as f:
    while True:
        print('receiving data...')

        data = s.recv(1024)
        print('data = %s' % repr(data))

        if not data:
            break
        f.write(data)
print('Successfully got the file')
s.close()
print('Connection closed')
```
## OUPUT

<img width="1092" height="266" alt="Screenshot 2026-05-20 083914" src="https://github.com/user-attachments/assets/c6236d5b-d2ab-401d-8cb0-b58acc3c95c8" />


## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
