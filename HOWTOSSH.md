# Setup SSH for VM Admin

## Client Config File Template
Path: ```$HOME/.ssh/config```

```Host <Name Your Endpoint>
  HostName <Server Public IP>
  Port <Port>
  User <User Name>
  IdentityFile <Client Private Key Path>
```
## Example
Assume:

Client private key path: ```~/.ssh/keys/mykey.pem```

Server public IP: 158.191.78.22, port: 22

Server login user: ubuntu

Then create config file at ```$HOME/.ssh/config```:

```Host remoteserver1
  HostName 158.191.78.22
  Port 22
  User ubuntu
  IdentityFile ~/.ssh/keys/mykey.pem
```

## Connect
Connect server by:

```ssh remoteserver1```

## Check SSH Server Fingerprint
Make sure SSH server fingerprint matches the first time login message:

```for file in /etc/ssh/*sa_key.pub; do ssh-keygen -lf $file; done```

[Back to README.md](README.md)