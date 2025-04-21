### Создать CRT, имея закрытый ключ

я скопирую ключ, [созданный ранее](../2/) <br>

`# openssl req -key domain.key -new -x509 -days 365 -out domain.crt` <br>

Сначала команда спросит пароль от rsa-ключа, [созданного ранее](../2/) <br>
> Enter pass phrase for domain.key:HardPass/2\*4<br>

Далее команда спросит данные для CSR, [как в примере 1](../1/):<br>
> Country Name (2 letter code) [XX]:RU<br>
> State or Province Name (full name) []:Moscow<br>
> Locality Name (eg, city) [Default City]:Moscow<br>
> Organization Name (eg, company) [Default Company Ltd]:LogicalAwesomeLLC<br>
> Organizational Unit Name (eg, section) []:Department1X<br>
> Common Name (eg, your name or your server's hostname) []:mydomain.ru<br>
> Email Address []:certs@mydomain.ru<br>

Опции:<br>
* req - PKCS#10 X.509 Certificate Signing Request (CSR) + certificate generating utility - без CSR в промежутке CRT не получится, поэтому req - создание CSR, хотя он и не сохранится
* -key - указываем входной ключ
* -new - хотим создать новый .csr запрос (нужно запросить информацию о csr у пользователя)
* -x509 - эта операция создаёт подписанный сертификат
* далее параметры сертификата

замечу, что команда не попросила задать пароль для CSR запроса<br>
потому что CSR не сохраняется. это пароль именно от CSR и сертификату он не нужен<br>
