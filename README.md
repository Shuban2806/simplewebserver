# EX01 Developing a Simple Webserver
## Date:27/11/2026

## AIM:
To develop a simple webserver to serve html pages and display the Windows Specifications of your Laptop.

## DESIGN STEPS:
### Step 1: 
HTML content creation.

### Step 2:
Design of webserver workflow.

### Step 3:
Implementation using Python code.

### Step 4:
Import the necessary modules.

### Step 5:
Define a custom request handler.

### Step 6:
Start an HTTP server on a specific port.

### Step 7:
Run the Python script to serve web pages.

### Step 8:
Serve the HTML pages.

### Step 9:
Start the server script and check for errors.

### Step 10:
Open a browser and navigate to http://127.0.0.1:8000 (or the assigned port).

## PROGRAM:

# Ex 01 - Simple Webserver

## AIM
To develop a simple webserver to serve html pages and display the list of protocols in TCP/IP Protocol Suite.

## PROGRAM
```python
from http.server import HTTPServer, BaseHTTPRequestHandler

REG_NO = "26017964"
NAME = "Shuban S"

PROTOCOLS = {
    "Application Layer": ["HTTP", "HTTPS", "FTP", "SMTP", "POP3", "IMAP", "DNS", "DHCP", "Telnet", "SSH", "SNMP", "TFTP"],
    "Transport Layer": ["TCP", "UDP", "SCTP"],
    "Internet Layer": ["IP (IPv4/IPv6)", "ICMP", "IGMP", "ARP", "RARP", "IPsec"],
    "Network Access (Link) Layer": ["Ethernet", "Wi-Fi (IEEE 802.11)", "PPP", "Frame Relay", "ATM"],
}


def build_page():
    sections = ""
    for layer, protos in PROTOCOLS.items():
        items = "".join(f"<li>{p}</li>" for p in protos)
        sections += f"<h2>{layer}</h2><ul>{items}</ul>"

    return f"""<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>TCP/IP Protocol Suite</title>
    <style>
        body {{ font-family: Arial, sans-serif; margin: 40px; background: #f4f6f8; }}
        h1 {{ color: #1a4f8b; }}
        h2 {{ color: #333; border-bottom: 1px solid #ccc; padding-bottom: 4px; }}
        .info {{ background: #fff; padding: 10px 16px; border-left: 4px solid #1a4f8b; margin-bottom: 20px; }}
    </style>
</head>
<body>
    <h1>List of Protocols in TCP/IP Protocol Suite</h1>
    <div class="info">
        <b>Register Number:</b> {REG_NO}<br>
        <b>Name:</b> {NAME}
    </div>
    {sections}
</body>
</html>"""


class MyHandler(BaseHTTPRequestHandler):
    def do_GET(self):
        print("Request received from:", self.client_address)
        body = build_page().encode("utf-8")
        self.send_response(200)
        self.send_header("Content-Type", "text/html; charset=utf-8")
        self.send_header("Content-Length", str(len(body)))
        self.end_headers()
        self.wfile.write(body)


if __name__ == "__main__":
    server_address = ("127.0.0.1", 8000)
    httpd = HTTPServer(server_address, MyHandler)
    print("My webserver is running at http://127.0.0.1:8000")
    httpd.serve_forever()
```

## OUTPUT

<img width="1465" height="911" alt="Screenshot 2026-11-27 122343" src="https://github.com/user-attachments/assets/d69e1b44-f269-4a79-a88c-c8f8ce8caf51" />
<img width="706" height="1006" alt="Screenshot 2026-11-27 122353" src="https://github.com/user-attachments/assets/9f550663-bba4-4aa8-b555-b65596f641c5" />

## RESULT
The webserver was developed and executed successfully on localhost (127.0.0.1:8000), displaying the list of protocols in the TCP/IP Protocol Suite.

