# Generate self signed sert for 999 days

`openssl genrsa -des3 -out nl.thoughtmaybe.com.key 1024`

`openssl req -new -key nl.thoughtmaybe.com.key -out nl.thoughtmaybe.com.csr`

Common Name is FQDN *.domain.com etc

-rw-r--r-- 1 root root   963 Jun 13 20:26 nl.thoughtmaybe.com.key

-rw-r--r-- 1 root root   664 Jun 13 20:35 nl.thoughtmaybe.com.csr

`openssl x509 -req -days 999 -in nl.thoughtmaybe.com.csr -signkey nl.thoughtmaybe.com.key -out nl.thoughtmaybe.com.crt`
