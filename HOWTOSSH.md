# Setup SSH for VM Admin
Your will need to have a VM with private SSH key under your control

Use your desired cloud provider to create a VM, usually the cheapest/smallest VM will be good enough to setup a VPN server

Creating a client side SSH config file makes your life easier

## Client Config File Template
Path: ```$HOME/.ssh/config```

```
Host <Give Your Endpoint A Name>
  HostName <Server Public IP>
  Port <Port>
  User <User Name>
  IdentityFile <Client Private Key Path>
```
## Example
Assume following values

Client private key path: ```~/.ssh/keys/mykey.pem```
(It should be available from cloud provider before creating the VM)

Server public IP: 40.87.100.12, port: 22

Server login user: ubuntu

Then create config file at ```$HOME/.ssh/config```

```
Host remoteserver1
  HostName 40.87.100.12
  Port 22
  User ubuntu
  IdentityFile ~/.ssh/keys/mykey.pem
```

## Check SSH Server Fingerprint For Safety
Although not required, it's always good to prevent "man in the middle" attack at the first time login

Make sure SSH server fingerprint matches the first time login message

Run the command below in the cloud provider provided utillity (cloud shell or cloud scripting environment )

```for file in /etc/ssh/*sa_key.pub; do ssh-keygen -lf $file; done```

The SSH server fingerprint should be one of the results shown above

## Connect
Connect server by:

```ssh remoteserver1```

[Back to README.md](README.md)