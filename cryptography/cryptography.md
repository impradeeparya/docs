# Cryptography

Cipher : Mathematical algorithm to generate cipher text with the help of key and content.

 > Content + key -> cipher(DES or AES) -> cipher text.


1. **Symmetric**

    - Symmetric cryptography also know as secret key cryptography.
    - This technique uses one single key also know as secret key to encrypt and decrypt content.
    - Single key is shared between client and server.
    - For communication client encrypt content with shared key and send it to server then server decrypt it with shared key or visa-versa.
    - If someone knows the public key then that person can easily hack the client server communication.
    - In this technique longer the key is more secure is the communication.
    
    ![alt tag](https://cloud.githubusercontent.com/assets/8745622/25774215/e983e03e-32a8-11e7-8848-e91d3d51c1cc.png)
    
2. **Public** 

    - To overcome the drawback of symmetric cryptography public key cryptography came into picture.
    - This technique uses concept of two key i.e. to encrypt by one key and decrypt by another key.
    - Two keys are know as public key and private key.
    - Server contain public and private key both.
    - Server share its public key with client for further communication.
    - Client sends its confidential information with server by encrypting it with public key of server.
    - If content is encrypted with public key then it can only be decrypted with private key of that public key.
    - With this way of communication if someone knows public he/she will not able to decrypt client confidential information that is send to server.
    - Now only thing that client needs to verify is that the public key valid public key of server to whom client is sending its confidential information.
    - if someone hack and send its own public key to client than that person can easily decrypt client content.
    - For this we use Digital certificate created by trusted parties called certificate authorities aka CA to authenticate public key of a server.
    - [How CA signed certificate works](https://github.com/impradeeparya/docs/blob/master/cryptography/digital-certificate.md)
        
        
    ![alt tag](https://cloud.githubusercontent.com/assets/8745622/25774321/9c52e3da-32aa-11e7-99fa-9214072b46d7.png)
    
    