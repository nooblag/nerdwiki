# Generate self signed sert for 999 days

`openssl req -newkey rsa:2048 -nodes -keyout nl.thoughtmaybe.com.key -out nl.thoughtmaybe.com.key`

`openssl req -new -key nl.thoughtmaybe.com.key -out nl.thoughtmaybe.com.csr`

Common Name is FQDN *.domain.com etc

-rw-r--r-- 1 root root   963 Jun 13 20:26 nl.thoughtmaybe.com.key

-rw-r--r-- 1 root root   664 Jun 13 20:35 nl.thoughtmaybe.com.csr

`openssl req -newkey rsa:2048 -nodes -keyout nl.thoughtmaybe.com.key -x509 -days 999 -out nl.thoughtmaybe.com.crt`
