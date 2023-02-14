# HTTP Server Test Error

Group sizes of 512 bits and 768 bits are now

[considered weak](https://weakdh.org/)

. Generally, 1024 bits is the minimum accepted size but not recommended, and

[2048 bits is considered best practice](https://supportforums.cisco.com/t5/security-documents/diffie-hellman-groups/ta-p/3147010)

. In particular OpenSSL, the library that provides HTTPS functionality for ThousandEyes and most other HTTP client software, has

[deprecated 512bit and 768-bit Diffie-Hellman groups](https://www.openssl.org/blog/blog/2015/05/20/logjam-freak-upcoming-changes/)

. Web servers that attempt TLS negotiations using 512-bit and 768-bit Diffie-Hellman groups will cause OpenSSL-based clients to terminate the TLS negotiation. This includes the client that executes a ThousandEyes HTTP Server test.
