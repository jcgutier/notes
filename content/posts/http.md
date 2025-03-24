# HTTP

To send a request to an HTTP server we can use `telnet`, and write the request:

```bash
telnet example.com

GET /index.html
Host: example.com
user-agent: curl/7.81.0
accept: application/json, */*
```

To send a request to an HTTPS server we can use `openssl` and write the request:

```bash
openssl s_client -connect example.com:443


GET https://example.com/index.html
Host: example.com
user-agent: curl/7.81.0
accept: application/json, */*
```

