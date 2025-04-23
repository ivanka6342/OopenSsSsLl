## Генерация ключей (public и private)

### OpenSSL
```
openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048
openssl rsa -pubout -in private_key.pem -out public_key.pem
```

private key: private_key.pem<br>
public key: public_key.pem<br>


### ssh-keygen
```
ssh-keygen -t rsa -b 2048 -f my_ssh_key
```
private key: my_ssh_key<br>
public key: my_ssh_key.pub<br>

в оригинале эти ключи подходят только для SSH (даже rsa:2048), но их можно сконвертировать в SSL формат<br>

### GPG
```
gpg --full-generate-key
```


### Python
```
from cryptography.hazmat.primitives.asymmetric import rsa
from cryptography.hazmat.primitives import serialization

# Generate private key
private_key = rsa.generate_private_key(
    public_exponent=65537,
    key_size=2048
)

# Serialize private key
private_pem = private_key.private_bytes(
    encoding=serialization.Encoding.PEM,
    format=serialization.PrivateFormat.PKCS8,
    encryption_algorithm=serialization.NoEncryption()
)

# Generate public key
public_key = private_key.public_key()
public_pem = public_key.public_bytes(
    encoding=serialization.Encoding.PEM,
    format=serialization.PublicFormat.SubjectPublicKeyInfo
)

print(private_pem.decode())
print(public_pem.decode())
```


### Java
```
import java.security.*;

public class KeyPairExample {
    public static void main(String[] args) throws Exception {
        KeyPairGenerator keyGen = KeyPairGenerator.getInstance("RSA");
        keyGen.initialize(2048);

        KeyPair pair = keyGen.generateKeyPair();
        PrivateKey privateKey = pair.getPrivate();
        PublicKey publicKey = pair.getPublic();

        System.out.println("Private Key: " + privateKey);
        System.out.println("Public Key: " + publicKey);
    }
}
```


### Web-Based Tools

На различных сайтах можно сгенерировать ключи для тестирования<br>
