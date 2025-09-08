# 2c.SIMULATING ARP /RARP PROTOCOLS
### Name:gokulan R
### Reference Number: 212224230076
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
## PROGRAM - ARP
### server.py
```python
import socket
c=socket.socket()
c.connect(('localhost',8000))
while True:
    ip=input("Enter IP address to find MAC (or type 'exit' to quit):")
    if ip.lower()=='exit':
        break
    c.send(ip.encode())
    mac=c.recv(1024).decode()
    print(f"MAC Address for {ip}: {mac}")
c.close()

```
### client.py
```python
import socket
s=socket.socket()
s.bind(('localhost',8000))
s.listen(5)
print("Server is listening..")
c,addr=s.accept()
address={"10.147.162.57":"52-D1-9C-21-AC-AD","172.20.10.2":"E0-2E-0B-37-CE-B8"}
while True:
    ip=c.recv(1024).decode()
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())
```
## OUPUT - ARP
<img width="1918" height="203" alt="image" src="https://github.com/user-attachments/assets/b7348228-5a8a-4964-acc6-77c78ea19c0b" />
<img width="1919" height="275" alt="image" src="https://github.com/user-attachments/assets/2430f853-fc9e-49e5-9526-a16a6d66f111" />

## PROGRAM - RARP
### server.py
```python
import socket
c=socket.socket()
c.connect(('localhost',8000))
while True:
    ip=input("Enter MAC address to find IP (or type 'exit' to quit):")
    if ip.lower()=='exit':
        break
    c.send(ip.encode())
    mac=c.recv(1024).decode()
    print(f"MAC Address for {ip}: {mac}")
c.close()

```
### client.py
```python
import socket
s=socket.socket()
s.bind(('localhost',8000))
s.listen(5)
print("Server is listening..")
c,addr=s.accept()
address={"52-D1-9C-21-AC-AD":"10.147.162.57","E0-2E-0B-37-CE-B8":"172.20.10.2"}
while True:
    ip=c.recv(1024).decode()
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())
```
## OUPUT -RARP
<img width="1919" height="269" alt="image" src="https://github.com/user-attachments/assets/4b182388-6c4b-4b96-bd27-b2ad1836998e" />
<img width="1918" height="269" alt="image" src="https://github.com/user-attachments/assets/ca599d8c-ff3e-4ba4-b3fb-0e7927340626" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
