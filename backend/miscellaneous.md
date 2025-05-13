## URL
- URL (Uniform Resource Locator) is the address used to access resources on the internet.It provides all the necessary information for locating a specific resource on a server.
```
https://www.example.com:443/path/page.html?search=query
└─┬──┘  └──────────────┘ └┬┘ └─────┘ └────────────┘ 
 │          DomainName      │     Path    Query Params 
Protocol                 Port
```

- **protocol** :	http, https – Defines the communication scheme used between the client and server.
- **Domain Name or hostname** :		www.example.com – The human-readable address of the server (typically maps to an IP address).
- **port** :		443, 3000, etc. – Specifies the port(application or service) on the server to connect to (optional for standard protocols: 80 for HTTP, 443 for HTTPS).
- **pathname** :	/path/page.html – Indicates the specific location of a resource on the server.
- **query** : 		?search=query – Provides additional information to the server in key-value pair format (often used for searches or filters).

## Protocol
- A protocol is a set of rules that define how data is transmitted between devices or software.
  
  
| Protocol       | Purpose                         |
| -------------- | ------------------------------- |
| **HTTP/HTTPS** | Web communication               |
| **FTP**        | File Transfer Protocol          |
| **TCP/IP**     | Base protocols for the internet |
| **SMTP/IMAP**  | Email communication             |
| **WebSocket**  | Real-time communication         |


## HTTP
- HTTP stands for Hypertext Transfer Protocol.
- It is the protocol used for communication between clients (like browsers) and servers.
- The client sends an HTTP request to a server. The server processes it and returns an HTTP response

## API
- An API, or Application Programming Interface, is a set of rules and specifications that defines how software components can interact with each other.
- Helps frontend (React, mobile apps) talk to backend (Node.js, Python, etc.)

## REST API
- REST stands for Representational State Transfer.
- A design pattern or architectural style for creating APIs over HTTP.
1. **Stateless** : Each request is independent and  No session stored between requests.
2. **Resource-based** : Everything is treated as a resource (user, product, etc.).
3. **Uses standard HTTP methods** : GET, POST, PUT, PATCH, DELETE, etc.

- **GET**    : GET the data       
- **POST**   : Create new data      
- **PUT**    : Replace full resource
- **PATCH**  : Partially update resource
- **DELETE** : Delete resource


