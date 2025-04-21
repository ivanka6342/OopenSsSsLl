### Генерируем только закрытый ключ

запрос на подпись открытого ключа (CSR) [будет отдельно](../3/) <br>

`# openssl genrsa -des3 -out domain.key 2048`

Команда попросит создать пароль для ключа:<br>
> Enter PEM pass phrase:HardPass/2\*4<br>
> Verifying - Enter PEM pass phrase:HardPass/2\*4<br>

Опции:<br>
* genrsa - сгенерить закрытый rsa ключ
* des3 - шифрование (симметричное)
* out - выход закрытого ключа (а не csr как [до этого](../1/))
