# Nginx local https

## 產生 SSL 憑證

生成一個 rsa 非對稱加密演算法的 2048 位元長的密鑰

```shell
openssl genrsa -out privatekey.pem 2048
```

以密鑰建立憑證簽章請求檔案

```shell
openssl req -new -key privatekey.pem -out private-csr.pem
```

```
Country Name (2 letter code) [AU]:TW
State or Province Name (full name) [Some-State]:Taiwan
Locality Name (eg, city) []:Taipei
Organization Name (eg, company) [Internet Widgits Pty Ltd]:My Company
Organizational Unit Name (eg, section) []:My Unit
Common Name (e.g. server FQDN or YOUR name) []:myhost.gtwang.org
Email Address []:user@gtwang.org
```

以同一隻密鑰來簽發憑證

```
openssl x509 -req -days 365 -in private-csr.pem -signkey privatekey.pem -out certificate.pem
```

## Nginx Config file

參考 nginx.conf

## Docker command

```shell
docker run --name my-custom-nginx-container -v /Users/kuochehuang/self/ssl/nginx.conf:/etc/nginx/nginx.conf:ro -v /Users/kuochehuang/self/ssl/certificate.pem:/etc/nginx/cert/certificate.pem:ro -v /Users/kuochehuang/self/ssl/privatekey.pem:/etc/nginx/cert/privatekey.pem:ro -p 80:80 -p443:443 -d nginx
```
