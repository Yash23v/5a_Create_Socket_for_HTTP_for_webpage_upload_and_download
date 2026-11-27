# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<BR>

## Program 
### `Server:`
```
import socket
s = socket.socket()
s.bind(("localhost",8081))
s.listen(1)
print("Server running...")
while True:
    c,addr = s.accept()
    request = c.recv(1024).decode()
    print("Request received")
    if "GET" in request:
        f = open("index.html","r")
        data = f.read()
        f.close()
        response = "HTTP/1.1 200 OK\n\n" + data
        c.send(response.encode())
    elif "POST" in request:
        data = request.split("\n\n")[1]
        
        f = open("upload.txt","w")
        f.write(data)
        f.close()
        c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())
    c.close()
```
### `Client:`
```
import socket
s = socket.socket()
s.connect(("localhost",8081))
ch = input("1.Download 2.Upload : ")
if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())
    data = s.recv(4096)
    print(data.decode())
else:
    msg = input("Enter data to upload: ")
    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())
    data = s.recv(1024)
    print(data.decode())
s.close()
```

## OUTPUT
### Upload:
### `Server:`
<img width="635" height="101" alt="Screenshot 2026-11-27 082539" src="https://github.com/user-attachments/assets/0eb47ad5-a5bb-4b71-964a-46305e3711d3" />

### `Client:`
<img width="630" height="172" alt="Screenshot 2026-11-27 082604" src="https://github.com/user-attachments/assets/0ff75be4-1bf1-4b5d-ac5e-4701d8e1a1a5" />

### Download:
### `Server:`
<img width="635" height="101" alt="Screenshot 2026-11-27 082539" src="https://github.com/user-attachments/assets/0eb47ad5-a5bb-4b71-964a-46305e3711d3" />

### `Client:`
<img width="640" height="617" alt="Screenshot 2026-11-27 083539" src="https://github.com/user-attachments/assets/4b4e62af-281d-4ca7-957c-9517f3380628" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed
