# GPG
Guide and scripts on GPG.

- Simple Method to generating an encryption key
```
gpg --gen-key
```
- Generate Encryption key with full encryption options. Useful for generating ECC keys for encryption

```
gpg --expert --full-gen-key
```
## Exporting and Importing Keys
- Exporting your public key for sharing. In the example below I am specifying my key by email and writing out to the file name Public.asc.
```
gpg --export -a "example@domain.com" > Public.asc
```
- Export your private key. Caution: It's important to backup your private key to a safe place. Secure with a 14 character or more password.
```
gpg --export-secret-key -a "example@domain.com" > private.asc
```
- Importing a public key. Please note this process is the same for importing a private key in your posession.
```
gpg --import Public.asc
```
## Revoking a keypair
- Revoking a keypair is used to distribute a revocation key to those by email or keyserver. It lets people know that your public key has been revoked. 
It's important to generate a revocation key immediately after key creation in case you ever misplace or lose your encryption key.
```
gpg --gen-revoke example@domain.com
```
## Signing Files, Messages, and other people's keys
- Signing is a method used to your sender that your file or message has not been altered during transit. It simply verifies
authenticity. Everyone should get in a habit of signing and verifying messages and files. 

- This command signs a file with a detached signature that can later be used for verification by the recipient. 
This option is the most useful for simply ensuring the integrity (but not privacy) of a file.
```
gpg --detach-sign -o sig.gpg testfile.txt
```
- Verify that a file has been signed with a good signature
```
gpg --verify sig.gpg testfile.txt
```
- Clearsign messages by wrapping an ASCII armored signature into a message. 
```
gpg --clearsign -o output.txt testfile.txt
```
- Verifying output file with ASCII armored signature
```
gpg --verify output.txt
```
## working with GPG encryption (Putting it all together)
- Encrypt, sign and ACII Armor file. I find this useful when you are encrypting a message consisting of pure text to the receiver of the message. 
```
gpg --encrypt --sign --armor -r person@email.com name_of_file
```
- To encrypt to multiple receivers. 
```
gpg --encrypt --sign --armor -r person@email.com -r person2@email.com name_of_file
```
- It is also possible to encrypt without a public key using symmetric encryption
```
gpg --output doc.gpg --symmetric doc
