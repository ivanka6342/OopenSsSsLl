### Просмотр данных CSR и CRT + проверка соответствия ключей

я скопирую [созданные ранее](../4/) ключ KEY, CSR и CRT<br>

Просмотр данных сертификата (CRT) и Certificate Signing Request (CSR)<br>
```
# openssl rsa -check -in domain.key - для просмотра данных KEY
# openssl req -noout -text -verify -in domain.csr - для просмотра данных CSR
# openssl x509 -noout -text -in domain.crt - для просмотра данных CRT
```


Проверка соответствия ключей<br>

```
openssl x509 -noout -modulus -in domain.crt | openssl md5
openssl rsa -noout -modulus -in domain.key | openssl md5
```

Значения ключей в командах должны совпадать<br>
