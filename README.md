# NGINX Performance Testing

#### CPU, Memory and process related 

Display CPU and process metrics - Enable multi CPU by loading top hit "1" then "W" to save configuration first

`top -n 1 -b`

Display virtual memory stats for 30 intervals

`vmstat -n 1 30`

Additional memory stats

`vmstat -a 1`


#### Networking related

Get a list of tcp connections and their states

`netstat -ant`

Get list of TCP sockets

`ss -atn`

Print a list of TCP connections each second

`netstat -antc`

Display packets, errors, drop and states per interface

`netstat -i 1`

Various network counters, it make sense to collect each 5 or 10 minutes

`netstat -st`


### Disk I/O related

Disk I/O dmesg and /var/log/messages (RHEL) /var/log/syslog (debian/ubuntu)

`iostat 1`


# cURL

 - https://curl.haxx.se/docs/manpage.html


# OpenSSL

### Generate client server key, cert and ca certificates

```
openssl genrsa -des3 -out ca.key 4096
openssl req -new -x509 -days 365 -key ca.key -out ca.crt
openssl genrsa -des3 -out client.key 4096
openssl req -new -key client.key -out client.csr
openssl x509 -req -days 365 -in client.csr -CA ca.crt -CAkey ca.key -set_serial 01 -out client.crt
openssl pkcs12 -export -clcerts -in client.crt -inkey client.key -out client.p12
openssl genrsa -des3 -out server.key.rsa 4096
openssl rsa -in server.key.rsa -out server.key
openssl req -new -key server.key -out server.csr
openssl x509 -req -days 365 -in server.csr -CA ca.crt -CAkey ca.key -set_serial 02 -out server.crt
```

 - https://github.com/nginxinc/show-demos/tree/master/n-dockerui


### Extract key and cert from pkcs12 bundle

```
openssl pkcs12 -in path.p12 -out newfile.crt.pem -clcerts -nokey
openssl pkcs12 -in path.p12 -out newfile.key.pem -nocerts -nodes
```

 - http://stackoverflow.com/questions/15144046/need-help-converting-p12-certificate-into-pem-using-openssl


### Convert .crt to .pem

```
openssl x509 -in mycert.crt -out mycert.pem -outform PEM
```

 - http://stackoverflow.com/questions/4691699/how-to-convert-crt-to-pem
