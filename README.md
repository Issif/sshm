# SSHM

## Description

Easy connect on EC2 instances thanks to AWS System Manager Agent. Just use your `~/.aws/profile` to easily select the instance you want to connect or on create a tunnel to.

## Why

`SSH` is great, `SSH` is useful, we do love `SSH` as the sysdadmins we are but AWS doesn't let us add several keys except with a custom userdata or else. With `SSH` we have to set up a bastion and open security groups to some CIDR or even use a VPN. AWS SSM Agent permits to simplify this process, no need to share keys, no port to open, no instance to set up, you only use your IAM (with MFA) user and all which is done is logged in S3. See :https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html.

## Prerequisites

Install `session-manager-plugin` : https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html (minimum version : **1.1.35.0**)

## Usage

```bash
Usage of sshm:
  -i string
        InstanceID for direct connection
  -lpn string
        Local Port Number for Proxy
  -p string
        Profile from ~/.aws/config
  -pn string
        Port Number for Proxy
  -r string
        Region, default is eu-west-1 (default "eu-west-1")
```
You can select your instance by &larr;, &uarr;, &rarr; &darr; and filter by *Tag:Name*, *InstanceId*, *Hostname*, *PrivateIp*, *PublicIp*, etc. **Enter** key to validate.

If `-lpn` and `-pn` are specified, a tunnel is started :

```bash
$ sshm -lpn 9999 -pn 80
 
...

Starting session with SessionId: 1576756257508463700-0c3b74e1f450c5d5a
Port 9999 opened for sessionId 1576756257508463700-0c3b74e1f450c5d5a.
```

Legend :
* **Online** : all running instances with a SSM Agent connected
* **Offline** : all instances with a SSM Agent disconnected (agent down or instance is stopped)
* **Running** : all running instances with or without SSM Agent installed

## Output Example

![screenshot1](./img/screenshot1.png)
![screenshot2](./img/screenshot2.png)

## Build

```bash
go build
```
This repository uses `go mod`, so don't `git clone` inside your `$GOPATH`.

## Author

Thomas Labarussias (thomas.labarussias@fr.clara.net - https://github.com/Issif)