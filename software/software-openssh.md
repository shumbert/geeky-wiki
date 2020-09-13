# Per-user OpenSSH server configuration
For instance, allow password authentication for some users only:
```
Match User bob
    PasswordAuthentication yes
```

# Generate the public key file from the private key file
```
ssh-keygen -y -f key > key.pub
```

# Troubleshooting
## ssh keeps asking for private key passphrase even though it is loaded in ssh-agent
Apparently if you only have the private key in your .ssh folder, and the host you are connecting to has the IdentitiesOnly option set to yes, ssh will keep asking for the private key passphrase. The solution is to copy the public key file to your .ssh folder.