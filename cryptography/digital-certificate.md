# Digital Certificate

> Digital certificate ensure that content belongs to right source. These certificates are created by the trusted authorities knows as Certificate Authorities aka CA.

- source refer to the party that wants to create its digital certificate from CA.
## How CA sends public key of source to destination.
    - Source share public key with CA to for creating trusted certificate.
    - CA create hash of its entire content and public key of source through hash function. **i.e. hash_ca = certificate content + public key(source)**.
    - Hash function refer to the message digest or algorithm to genrate encrypted text from given plain text.
    - Then CA encrypt the hash with its private key and attach it with certificate. **i.e. en_hash = encrypt_private_key(hash_ca)**.
    - **Certificate = Certificate + public key(source) + en_hash**.
    - Client decrypt the hash value with CA pulic key. **i.e hash_ca = decrypt_public_key(en_hash)**.
    - Client generate hash value. **i.e hash_client = certificate + public key**.
    - if hash_client == hash_ca means public key belongs to right source not changed while transmitting over network.
    
    
    
> Mostly used hash function are MD5(126-bit) and SHA-1(168-bit). The create one way encryption means we can't decrypt hash function output back to original plain text.


