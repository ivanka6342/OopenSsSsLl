### Создать CSR запрос для существующего закрытого ключа

Если уже есть закрытый ключ, то можно создать для него csr запрос<br>
я скопирую ключ, [созданный ранее](../2/) <br>

`# openssl req -key domain.key -new -out domain.csr` <br>

Сначала команда спросит пароль от rsa-ключа, [созданного ранее](../2/) <br>
Enter pass phrase for domain.key:HardPass/2*4<br>

Далее команда спросит данные для CSR, [как в примере 1](../1/):<br>

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
* -key - это как key_in - имеющийся закрытый ключ
* -new - новый csr запрос (нужно запросить информацию о csr у пользователя)
* -out - выходной файл для него как выше
