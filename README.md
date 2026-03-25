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

## server

~~~
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
~~~

## client

~~~
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
~~~

## OUPUT

## server

<img width="953" height="296" alt="548637414-76bdb133-7faf-4f3e-93dd-5fc3136f67f0" src="https://github.com/user-attachments/assets/c442249b-33bc-4469-a2cc-2947f7126f38" />


## client 

<img width="937" height="342" alt="548637444-dcfa0ea3-39c1-4689-8a50-ad29160e175b" src="https://github.com/user-attachments/assets/be67e975-7dde-4310-9cea-0560a4a1dba1" />


## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
