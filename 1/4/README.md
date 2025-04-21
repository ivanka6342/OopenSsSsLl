### Создать сертификат из закрытого ключа и запроса .csr

скопирую `domain.key` и `domain.csr`, [созданные ранее](../3/) <br>

`# openssl x509 -signkey domain.key -in domain.csr -req -days 365 -out domain.crt`

Команда спросит пароль от приватного ключа domain.key, [созданного ранее](../2/)<br>
> Enter pass phrase for domain.key:HardPass/2\*4<br>
> Certificate request self-signature ok<br>
> subject=C=RU, ST=Moscow, L=Moscow, O=LogicalAwesomeLLC, OU=Department1X, CN=mydomain.ru, emailAddress=certs@mydomain.ru<br>

Опции:<br>
* x509 - X.509 Certificate Data Management (display and signing) utility
* -signkey - входной закрытый ключ (не просто -key потому что в паре с .csr который signed by this key)
* -in - входной .csr, созданный с ключом выше
* -req - не знаю зачем он тут если x509 уже указал на создание сертификата
* -days - сколько действует сертификат
* -out - сам сертификат
