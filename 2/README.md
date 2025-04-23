## public key и private key

Подробнее о генерации ключей [описано в проекте 1](1/) <br>

Вопрос-Ответ<br>

можно ли использовать вместо приватного ключа (KEY) для openssl - свои из ssh-keygen или других утилит?<br>
* и `ДА`, и `НЕТ`

openssl<br>
* Цель: создание ключей для сертификатов X.509, TLS/SSL шифрования и других cryptographic задач
* Формат ключей: форматы PEM, PKCS#8 или DER - используемые для SSL/TLS сертификатов
* Default алгоритмы: генерит RSA и EC ключи для лучшей гибкости в cryptographic settings

ssh-keygen<br>
* Цель: генерация ключей SSH для auth в среде SSH
* Формат ключей: формат OpenSSH, оптимизированный для SSH auth. публичный ключ .pub а приватный без расширения
* Default алгоритмы: генерит RSA, Ed25519 и ECDSA - которые используются в SSH

openssl и ssh-keygen - оба могут сгенерить пару ключей: приватный(закрытый) и публичный(открытый), но используют разные форматы<br>
Чтобы использовать OpenSSL-generated ключ в SSH, можно его сконвертировать в OpenSSH-compatible format:<br>
```
    openssl rsa -in mykey.pem -out mykey.key
    ssh-keygen -i -m PEM -f mykey.key
```

Сконвертировать SSH private key в OpenSSL-compatible format сложнее, но например для RSA это возможно<br>
