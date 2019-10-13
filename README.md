# Client_Server_Palindrom

### Program Overview:
Client is prompted to input an array of strings of ASCII characters from a file and sends them to the server process on the host using TCP/IP protocols and sockets. Once client is connected to the server, server will display IP and Port it is connected to. The server checks if the string entered is a palindrome and returns the string with either "YES" or "NO".

Server is able to handle multiple connections from many clients concurrently using the select() command, through select server receieves request asynchronously. The server also uses the accept() system call to process multiple request concurrently. 


#### Run Code: 

Open three terminals, each where the selectServer.py and selectClient.py are located
* Run server 
```console
$ python3 selectServer.py 
```
* Connect 1st client 
```console 
$ python3 selectClient.py
```
* Connect 2nd client
```console
$ python3 selectClient.py
```

#### Server Display after running:
```console
Socket created
Socket listening...
```
#### Clients Display after connecting to server 
```console
Enter Text Here:
>>>
```
#### Server Display once two clients are connected and Strings entered from 2 seperate clients
```console 
Socket created
Socket Listening...
Connected with 127.0.0.1: 62308
Connected with 127.0.0.1: 62310
Palindrome:
NO
Palindrome:
YES
```

## Multiple Connection Server 

Select() command allows server to check for I/O completion on more than one socket. Calling select() will allow server to see which sockets have I/O ready for reading and/or writing
```console
while True:
    ready_to_read, ready_to_write, in_error = select.select(SOCKET_LIST, [], [], 0)
```

accept() system call allows server to process multiple requests 
```console 
connection, address = server_socket.accept() 
```
* Get list of sockets that are ready to be read through the select() command. Receives requests asynchronously
  select gets passed 3 lists, Reading, writing, and error
  Will not block when additional request arrive
```console
while True:
   ready_to_read, ready_to_write, in_error = select.select(SOCKET_LIST, [], [], 0) # Timeout = 0
   connection, address = server_socket.accept()    # Accepts system calls in order to process multiple request
   ip, port = str(address[0]), str(address[1])
   print("Connected with " + ip + ": " + port)
   Thread(target=client_threads, args=(connection, ip, port)).start()

 soc.close()
```

#### Palindrome Method to determine if string is Palindrome
```console 
def is_palindrome(input_str):
    print("Palindrome: ")
    rev_string = input_str[::-1]
    if input_str == rev_string:
        print("YES")
    else:
        print("NO")
```


Author: Christine Campbell 

