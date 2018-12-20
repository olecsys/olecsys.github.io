Для того, чтобы проверить соединение *SSL* с сервером:
```bash
openssl s_client -connect <URL>
```

Например:
```bash
openssl s_client -connect bitbucket.org:443
```

Для того, чтобы получить список поддерживаемых веб сервером типов шифрования, используется следующая команда:
```bash
nmap --script ssl-enum-ciphers -p <PORT> <URL> 
```

Например, для проверки *hhtps://bitbucket.org* используется следующая команда:
```bash
nmap --script ssl-enum-ciphers -p 443 bitbucket.org
```