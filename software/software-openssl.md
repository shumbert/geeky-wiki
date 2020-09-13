# Symmetric encryption
```
# encryption
openssl enc -aes-256-ctr -a -salt -pbkdf2 -in file -out file.enc

# decryption
openssl enc -d -aes-256-ctr -a -pbkdf2 -in file.enc -out file
```
