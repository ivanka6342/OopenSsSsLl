## отличия OpenSSL, Easy-RSA и других

Вопрос-Ответ<br>
есть ли разница, чем создавать Certificate Authority (CA): OpenSSL или Easy-RSA?<br>
* и `ДА`, и `НЕТ`

Easy-RSA - обертка для OpenSSL. это toolkit для облегчения создания и управления Public Key Infrastructure (PKI) для VPN<br>
* автоматизирует создание CA, key pair, CSR, CRT.
* немного не такой набор полей сертификата - рассчитан не на веб-серверы и браузеры, а на проверку openssl
* * поэтому лучше его для вэб-серверов не применять (без тюнинга)
* Security зависит от версии Easy-RSA и настроек
* CA для OpenVPN обычно приватные, а сертификаты не publicly/globally trusted - они trusted within the VPN ecosystem
* для OpenVPN нужны сертификат сервера для auth и сертификат клиента (каждому юзеру свой) - mutual auth (клиент и сервер проверяют друг друга). возможно, не всегда
* разные цели - разные протоколы (здесь OpenVPN)
* сертификаты обычно long-lived - действуют годы, так как они юзаются для внутренних целей
* часто генерит static TLS keys (ta.key) для TLS-auth, чтобы избежать DoS attacks. и это помимо server.crt + server.key и client.crt + client.key

OpenSSL - general-purpose cryptographic toolkit<br>
* он может создать ключи и сертификаты для любых application, включая web servers (HTTPS), mail servers, and VPNs. 
* но требует ручной настройки и команд на каждый шаг
* Security зависит от настроек и только
* всегда publicly/globally trusted CA (Let's Encrypt, Digicert) - подписывают наши сертификаты и браузеры распознают их as valid
* нужен только SSL/TLS сертификат сервера - one-way auth (browser verifies the server’s certificate). не забываем, клиенты в своей OS хранят trusted CA файлы - этого нет в OpenVPN
* разные цели - разные протоколы (здесь HTTPS)
* Public CAs выдают сертификаты short-lived certificates (90 дней от Let's Encrypt)

Общее<br>
* сертификаты почти одинаковые: оба X.509 и подписываются by CA
* вообще ноль разницы в приватных ключах - RSA/ECC (ECDSA) keys
* их сертификаты и ключи взаимозаменяемы, если установлены правильные поля и расширения - но лучше так не делать
* для OpenVPN вооще нет разницы: OpenSSL поддерживет формат для OpenVPN, но Easy-RSA удобнее
* оба юзают Public Key Infrastructure (PKI)

Вывод<br>
* скорее разница не в тулзах PKI (Easy-RSA, OpenSSL), а в сфере применения (OpenVPN, HTTPS) и их особенностях (Private CA и interanl use для OpenVPN)
* PKI тулзы можно настроить на нужную цель. можно даже сконвертировать неподходящие сертификаты или сгенерить из "чужеродных" ключей

Alternatives<br>
* Easy-RSA
* * Smallstep (step-ca) - CLI/Web
* * BounCA - Web-based
* * FreeIPA - Integrated System
* * LDAP Account Manager (LAM)
* OpenSSL
* * LibreSSL - CLI/Library (OpenSSL fork)
* * BoringSSL - Library
* * mbed TLS - Library
* * wolfSSL - Library
* * GnuTLS - Library
* * NSS (Network Security Services) - Library
* * Botan - C++ Library
* * CFSSL (Cloudflare's PKI/TLS toolkit) - CLI Tool + API-friendly
* * Let's Encrypt - Certbot, acme.sh (For web server certificates - HTTPS only)
* * Microsoft Certificate Services - Built into Windows Server
* * Vault (by HashiCorp)
* * Cloud Providers' Certificate Services: AWS Certificate Manager (ACM), Google Cloud (GCP) Certificate Manager, Azure Key Vault
* * mkcert - for Local Development. Self-signed certs for localhost testing


Other Methods and Tools<br>
* Programming Libraries
* * Python: cryptography или pyOpenSSL
* * Java: BouncyCastle или Keytool
* * Golang: crypto/x509
* Manual Key Generation
* * custom scripts or lower-level libs - технически возможно (generate RSA key pairs and certs), но очень сложно, долго, небезопасно, подвержено ошибкам и недопустимо в продакшене
