# 2c.SIMULATING ARP /RARP PROTOCOLS
##  NAME: SHYAM S
## REGISTER NUMBER: 212223240156


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
P
## PROGRAM - ARP
### server:A
```python
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(2)
print("Waiting for connection...")

c, _ = s.accept()
print("Client connected!")

arp_table = {
    "192.168.1.1": "AA:BB:CC:DD:EE:01",
    "192.168.1.2": "AA:BB:CC:DD:EE:02",
}

while True:
    ip = c.recv(1024).decode()
    if not ip:
        break

    mac = arp_table.get(ip, "Not Found")
    print(f"{ip} -> {mac}")
    c.send(mac.encode())

c.close()
s.close()
```
### client
```python
import socket

c = socket.socket()
c.connect(('localhost', 8000))

while True:
    ip = input("Enter IP (or 'exit' to quit): ")
    if ip.lower() == "exit":
        break

    c.send(ip.encode())
    print("MAC:", c.recv(1024).decode())

c.close()
```

## OUTPUT - ARP
### server:
![image](https://github.com/user-attachments/assets/f539ce75-3c02-4944-961f-712988f61d94)

### client
![image](https://github.com/user-attachments/assets/b3cc5ab7-0aac-4678-826b-884ef7da09b8)


## PROGRAM - RARP
### server
```python
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(1)  # Listen for one connection
print("Server is waiting for connection...")

c, _ = s.accept()
print("Client connected!")

# RARP Table (Mapping MAC to IP)
rarp_table = {
    "6A:08:AA:C2": "165.165.80.80",
    "8A:BC:E3:FA": "165.165.79.1"
}

while True:
    mac = c.recv(1024).decode()  # Receive MAC address
    if not mac:
        break

    ip = rarp_table.get(mac, "Not Found")  # Find IP or return "Not Found"
    print(f"MAC: {mac} -> IP: {ip}")
    
    c.send(ip.encode())  # Send IP address

c.close()
s.close()


```

### client
```python
import socket

c = socket.socket()
c.connect(('localhost', 8000))

while True:
    mac = input("Enter MAC address (or 'exit' to quit): ")
    
    if mac.lower() == "exit":
        break

    c.send(mac.encode())  # Send MAC to server
    ip = c.recv(1024).decode()  # Receive IP from server

    print(f"IP Address for {mac}: {ip}")

c.close()


```


## OUTPUT -RARP

### server
![image](https://github.com/user-attachments/assets/bc271dc9-7b53-44a6-946f-e7218fb80c8c)


### client
![image](https://github.com/user-attachments/assets/b9b7622f-a2d3-4a31-b50e-b70da83b5645)


## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
