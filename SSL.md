# Generate self signed sert for 999 days
*Swap out app_name for purpose*

`openssl req -newkey rsa:2048 -nodes -keyout app_name.key -out app_name.key`

`openssl req -new -key app_name.key -out app_name.csr`

Common Name is FQDN *.app_name.com

`openssl req -newkey rsa:2048 -nodes -keyout app_name.key -x509 -days 999 -out app_name.crt`


# Variation method, self signed sert for wildcard, 3650 days
*Swap out app_name for purpose*

```sh
openssl genrsa 2048 > app_name-wildcard.key

openssl req -new -x509 -nodes -sha1 -days 3650 -key app_name-wildcard.key > app_name-wildcard.cert

# Common Name (eg, your name or your server's hostname) []:*.app_name.com

openssl x509 -noout -fingerprint -text < app_name-wildcard.cert > app_name-wildcard.info

cat app_name-wildcard.cert app_name-wildcard.key > app_name-wildcard.pem

chmod 644 app_name-wildcard.key app_name-wildcard.pem
```

*example nginx conf below*
```sh
# SSL

server {
  listen 443;
	server_name *.app_name.com;

	ssl                  on;
	ssl_certificate      /etc/nginx/ssl/app_name-wildcard.pem;
	ssl_certificate_key  /etc/nginx/ssl/app_name-wildcard.key;
	ssl_session_timeout  5m;

}
```
