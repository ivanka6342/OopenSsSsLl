### Генерируем закрытый ключ (KEY) и CSR - запрос на подпись открытого ключа

`# openssl req -newkey rsa:2048 -nodes -keyout domain.key -out domain.csr`

Команда спросит данные:<br>
> Country Name (2 letter code) [XX]:RU<br>
> State or Province Name (full name) []:Moscow<br>
> Locality Name (eg, city) [Default City]:Moscow<br>
> Organization Name (eg, company) [Default Company Ltd]:LogicalAwesomeLLC<br>
> Organizational Unit Name (eg, section) []:Department1X<br>
> Common Name (eg, your name or your server's hostname) []:mydomain.ru<br>
> Email Address []:certs@mydomain.ru<br>
> A challenge password []:SimplePass-1+2<br>
> An optional company name []:Github<br>

Опции:<br>
* req - PKCS#10 X.509 Certificate Signing Request (CSR) + certificate generating utility
* -newkey - с созданием нового закрытого ключа, но не генерация из имеющегося
* rsa:2048 - параметр создания: тип rsa и сложность 2048 байт
* -nodes - шифровать ключ не нужно
* -keyout - выход закрытого ключа
* -out - выход запроса на подпись открытого ключа (== неподписанный сертификат (открытый ключ + инфо о компании))


