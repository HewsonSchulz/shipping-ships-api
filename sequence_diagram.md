```mermaid
sequenceDiagram
    title Shipping Ships API

    participant Client
    participant Python
    participant json-server.py
    participant nss_handler.py
    participant parse.py
    participant views module
    participant Database

    Client->>Python: GET request to "/ships"
    Python->>json-server.py: run do_GET() method
    json-server.py->>nss_handler.py: call parse_url()
    nss_handler.py->>parse.py: call urlparse()
    parse.py-->>nss_handler.py: return parsed url
    nss_handler.py->>parse.py: call parse_qs()
    parse.py-->>nss_handler.py: return parsed queries
    nss_handler.py-->>json-server.py: return url as dictionary
    json-server.py->>views module: request list of ships
    views module->>Database: request ships data

    Database-->>views module: return ships data
    views module-->>views module: convert data to JSON format
    views module-->>json-server.py: return ships data
    json-server.py-->>nss_handler.py: return ships data (in JSON format)
    nss_handler.py-->>Client: return ships data (in JSON format)

```
