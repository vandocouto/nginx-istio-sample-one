```bash
kubectl create -n istio-system secret tls istio-ingressgateway-certs --key httpbin.example.com.key --cert httpbin.example.com.crt
```

```bash
kubectl apply -f namespaces.yaml
kubectl apply -f .
``` 
```bash
curl -k -v -HHost:httpbin.example.com --resolve httpbin.example.com:$SECURE_INGRESS_PORT:$INGRESS_HOST --cacert example.com.crt https://httpbin.example.com:$SECURE_INGRESS_PORT/status/418
```
OUTPUT
```bash
* Couldn't parse CURLOPT_RESOLVE entry 'httpbin.example.com::'!
*   Trying 10.104.200.42...
* TCP_NODELAY set
* Connected to httpbin.example.com (10.104.200.42) port 443 (#0)
* ALPN, offering h2
* ALPN, offering http/1.1
* error setting certificate verify locations, continuing anyway:
*   CAfile: example.com.crt
  CApath: /etc/ssl/certs
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
* TLSv1.3 (IN), TLS handshake, Server hello (2):
* TLSv1.3 (IN), TLS Unknown, Certificate Status (22):
* TLSv1.3 (IN), TLS handshake, Unknown (8):
* TLSv1.3 (IN), TLS handshake, Certificate (11):
* TLSv1.3 (IN), TLS handshake, CERT verify (15):
* TLSv1.3 (IN), TLS handshake, Finished (20):
* TLSv1.3 (OUT), TLS change cipher, Client hello (1):
* TLSv1.3 (OUT), TLS Unknown, Certificate Status (22):
* TLSv1.3 (OUT), TLS handshake, Finished (20):
* SSL connection using TLSv1.3 / TLS_AES_256_GCM_SHA384
* ALPN, server accepted to use h2
* Server certificate:
*  subject: CN=httpbin.example.com; O=httpbin organization
*  start date: Apr  9 16:25:08 2020 GMT
*  expire date: Apr  9 16:25:08 2021 GMT
*  issuer: O=example Inc.; CN=example.com
*  SSL certificate verify result: unable to get local issuer certificate (20), continuing anyway.
* Using HTTP2, server supports multi-use
* Connection state changed (HTTP/2 confirmed)
* Copying HTTP/2 data in stream buffer to connection buffer after upgrade: len=0
* TLSv1.3 (OUT), TLS Unknown, Unknown (23):
* TLSv1.3 (OUT), TLS Unknown, Unknown (23):
* TLSv1.3 (OUT), TLS Unknown, Unknown (23):
* Using Stream ID: 1 (easy handle 0x561088d54580)
* TLSv1.3 (OUT), TLS Unknown, Unknown (23):
> GET /status/418 HTTP/2
> Host:httpbin.example.com
> User-Agent: curl/7.58.0
> Accept: */*
>
* TLSv1.3 (IN), TLS Unknown, Certificate Status (22):
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* TLSv1.3 (IN), TLS Unknown, Unknown (23):
* Connection state changed (MAX_CONCURRENT_STREAMS updated)!
* TLSv1.3 (OUT), TLS Unknown, Unknown (23):
< HTTP/2 404
< date: Thu, 09 Apr 2020 17:08:20 GMT
< server: istio-envoy
<
* Connection #0 to host httpbin.example.com left intact
```
