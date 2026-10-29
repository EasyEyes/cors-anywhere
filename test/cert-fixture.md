# Public TLS test fixture

`key.pem` and `cert.pem` are public test fixtures, never production credentials. The RSA key is 2048 bits. The certificate is deliberately expired (May 6 to June 5, 2015), preserving the suite's certificate-rejection checks while allowing supported Node versions to create the HTTPS server. The previous 1024-bit key was rejected by Node 24 before certificate validation could be tested.

The self-signed certificate uses SHA-256 and CN `cors-anywhere test`. Do not renew its expiration: the tests verify rejection of an expired certificate and explicitly test the opt-out behavior separately.
