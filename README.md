# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:ARP Server
Objective: To receive an IP address from the client and send the corresponding MAC address.

Algorithm Steps:

1. Start the program.

2. Create a TCP socket.

3. Bind the socket to the local host and port number 8000.

4. Put the server socket into listening mode.

5. Display a message indicating the server is ready.

6. Accept a connection request from the client.

7. Initialize a table containing IP address – MAC address pairs.

8. Repeat the following steps:

    •Receive the IP address from the client.
   
    •Search the received IP address in the ARP table.

    •If the IP address is found, get the corresponding MAC address.

    •If the IP address is not found, set the response as "Not Found".

    •Send the MAC address (or "Not Found") back to the client.

10. Continue until the connection is terminated.

11. Stop the program.

## Algorithm: ARP Client
Objective: To send an IP address to the server and receive the corresponding MAC address.

Algorithm Steps:

1. Start the program.

2. Create a TCP socket.

3. Connect the socket to the server using localhost and port number 8000.

4. Repeat the following steps:

    •Read the logical address (IP address) from the user.

    •Send the IP address to the server.

    •Receive the MAC address from the server.

    •Display the received MAC address.

5. Continue until the user terminates the program.

6. Stop the program.

## Algorithm: RARP Server
Objective: To receive a MAC address from the client and return the corresponding IP address.

Algorithm Steps:

1. Start the program.

2. Create a TCP socket.

3. Bind the socket to localhost and port number 8001.

4. Put the socket into listening mode.

5. Display a message indicating that the RARP server is ready.

6. Accept a connection request from the client.

7. Initialize a RARP table containing MAC address – IP address pairs.

8. Repeat the following steps:
    •Receive the MAC address from the client.

    •Search the MAC address in the RARP table.

    •If the MAC address is found, retrieve the corresponding IP address.

    •If the MAC address is not found, set the response as "Not Found".

    •Send the IP address (or "Not Found") back to the client.

9. Continue until the connection is terminated.

10. Stop the program.

## Algorithm: RARP Client
Objective: To send a MAC address to the server and receive the corresponding IP address.

Algorithm Steps:
1. Start the program.

2. Create a TCP socket.

3. Connect the socket to the server using localhost and port number 8001.

4. Repeat the following steps:

    •Read the physical address (MAC address) from the user.

    •Send the MAC address to the server.

    •Receive the IP address from the server.

    •Display the received IP address.

5. Continue until the user terminates the program.

6. Stop the program.


## PROGRAM - ARP
client_arp.py
~~~
import socket

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    ip = input("Enter Logical Address (IP): ")
    s.send(ip.encode())
    print("MAC Address:", s.recv(1024).decode())
~~~
server_arp.py
~~~
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("ARP Server is listening on port 8000...")
c, addr = s.accept()

address = {
    "148.129.123.45": "5D:BC:E3:FA",
    "109.178.123.45": "8A:2B:3C:4D",
}

while True:
    ip = c.recv(1024).decode()
    print(f"Received IP: {ip}")
    mac = address.get(ip, "Not Found")
    c.send(mac.encode())
~~~

## OUPUT - ARP

<img width="935" height="620" alt="image" src="https://github.com/user-attachments/assets/009f6918-d3c5-4440-a10c-983185a9e83b" />


## PROGRAM - RARP
client_rarp.py
~~~
import socket

s = socket.socket()
s.connect(('localhost', 8001))

while True:
    mac = input("Enter Physical Address (MAC): ")
    s.send(mac.encode())
    print("IP Address:", s.recv(1024).decode())
~~~

server_rarp.py

~~~
import socket

s = socket.socket()
s.bind(('localhost', 8001))
s.listen(5)
print("RARP Server is listening on port 8001...")
c, addr = s.accept()

address = {
    "5D:BC:E3:FA" : "148.129.123.45",
    "8A:2B:3C:4D" : "109.178.123.45",
}

while True:
    mac = c.recv(1024).decode()
    print(f"Received MAC: {mac}")
    ip = address.get(mac, "Not Found")
    c.send(ip.encode())
~~~
## OUPUT -RARP

<img width="928" height="434" alt="image" src="https://github.com/user-attachments/assets/bd824bfe-d6bc-4494-8f59-b3bd7686bbff" />


## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
