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

# Start ssh-agent on login
From https://stackoverflow.com/questions/18880024/start-ssh-agent-on-login:

Create a systemd user service, edit file `~/.config/systemd/user/ssh-agent.service`:
```
[Unit]
Description=SSH key agent

[Service]
Type=simple
Environment=SSH_AUTH_SOCK=%t/ssh-agent.socket
ExecStart=/usr/bin/ssh-agent -D -a $SSH_AUTH_SOCK

[Install]
WantedBy=default.target
```

In the shell startup files add an environment variable for the socket:
```
export SSH_AUTH_SOCK="$XDG_RUNTIME_DIR/ssh-agent.socket"
```

Finally enable the service:
```
systemctl --user enable ssh-agent
systemctl --user start ssh-agent
```

# Troubleshooting
## ssh keeps asking for private key passphrase even though it is loaded in ssh-agent
Apparently if you only have the private key in your .ssh folder, and the host you are connecting to has the IdentitiesOnly option set to yes, ssh will keep asking for the private key passphrase. The solution is to copy the public key file to your .ssh folder.
