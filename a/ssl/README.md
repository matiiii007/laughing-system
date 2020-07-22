## Crear certificados ssl

Se crea el certificado principal

```bash

openssl genrsa -aes256 -out ca-key.key 2048
openssl req -x509 -new -nodes -key ca-key.key -sha256 -days 1024 -out ca-cert.pem

```

Se crea el certificado del servidor

```bash
openssl genrsa -out server-key.key 2048
openssl req -new -key server-key.key -out server.csr
```

Se firma el certificado servidor con el certificado principal

```bash
openssl x509 -req -in server.csr -CA ca-cert.pem -CAkey ca-key.key -CAcreateserial -out server-cert.pem -sha256 -days 1024
```

y para verificar

```bash

openssl verify -CAfile ca-key.pem server-cert.pem

```
