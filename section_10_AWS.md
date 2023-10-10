## 75. Overview

***

## 76. Creating a virtual server instance on `AWS EC2`

### Create an instance

* Create an `AWS` Account
    - Enter Credit Card info

* `aws.amazon.com` -> My Account -> `AWS Management Console` 
    - Login / Password -> Sign in using alternative factors of authentication

* Create a new `EC2` instance
    - `Services` -> `EC2`
    - Instances -> `Launch Instances`
    - Application and OS Images (AMI) -> Quick Start -> `Ubntu` -> Free tier eligible
    - Instance type (`t2.micro`)
    - Configure storage / 8GB free 
    - Name add tags / web-server-mm-dd-yyyy (`web-server-10-12-2023`)
    - Create security group/ SSH / HTTP
    - Create key pair (`kp-mm-dd-yyyy`) / Download
    - Launch

***

## 77. Hello World on `AWS`

### Deploy your binary

```
$ mv ~/Desktop/kp-mm-dd-yyyy.pem ~/.ssh
```

```
$ sudo chmod 400 kp-mm-dd-yyy.pem                   # -r--|---|---
```

### Build hello world

```
$ /Users/marshad/Desktop/golang-web-dev/031_aws/01_hello

$ go env
$ go help build

$ go mod init 01_hello
$ go mod tidy
$ GOOS=linux GOARCH=amd64 go build -o mybinary              # `-o` flag: put the binary to a particular name
```

### Copy your binary to the sever

```
$ scp -i ~/.ssh/kp-10-10-2023.pem mybinary ubuntu@[public-IPv4-DNS]:              # There is a `:` at the end
```

* `ec2-user` might be `ubuntu` depending upon your machine
 - say "yes" to The authenticity of host ... can't be established.

### SSH into your server

```
$ ssh -i ~/.ssh/kp-10-10-2023.pem ubuntu@[public-IPv4-DNS]
```

```
$ hostname
```
* Private IPv4 addresses: 172.31.37.108

```
$ whoami
```
* `ubuntu`

```
$ uname -a
```

### Run your code

```
$ sudo chmod 700 mybinary
$ sudo ./mybinary
- check it in a browser at [public-IP]
```

### Exit

```
- ctrl + c
- exit
```

***

## 78. Persisting your application

To run our application after the terminal session has ended, we must do one of the following:

* Possible options
    - screen
    - `init.d`
    - upstart
    - `system.d`

### `System.d`

```
# Create a configuration file
$ cd /etc/systemd/system/
$ sudo touch anynamewewant.service
$ sudo vim   anynamewewant.service
```

```
[Unit]
Description=Go Server

[Service]
ExecStart=/home/<username>/<exepath>            # /home/ubuntu/mybinary
User=root
Group=root
Restart=always

[Install]
WantedBy=multi-user.target
```

```
$ sudo systemctl enable ```<filename>```.service
$ sudo systemctl start  ```<filename>```.service
$ sudo systemctl status ```<filename>```.service
$ sudo systemctl stop   ```<filename>```.service
```

### Troubleshooting

* A possible issue could be that you're cross-compiling for the wrong architecture: AWS might have assigned you a different machine than the one used in this example. 
* To solve this problem, we will install `Go` on the AWS machine and then run `go env` to see `GOOS` & `GOARCH` for that machine.

```
* download Go
    - wget https://storage.googleapis.com/golang/go1.7.4.linux-amd64.tar.gz

* unpack go
    - tar -xzf go1.7.4.linux-amd64.tar.gz

* remove the tar file
    - rm -rf go1.7.4.linux-amd64.tar.gz

* make your go workspace
    - mkdir goworkspace
    - cd gowoworkspace
    - mkdir bin pkg src
    - cd ../
```

```
* add environment variables
    - $ vim ~/.bashrc

export GOROOT=/home/ubuntu/go
export GOPATH=/home/ubuntu/goworkspace
export PATH=$PATH:/home/ubuntu/goworkspace/bin
export PATH=$PATH:/home/ubuntu/go/bin
```

```
* refresh environment variables
  - $ source ~/.bashrc
* confirm installation
  - $ go version
* get machine GOOS & GOARCH info
  - $ go env
```

### Troubleshooting

* Sometimes students miss setting port openings in security. 
* If you are having issues, check to make sure these settings are correct - and please note, you IP address for SSH will either be `0.0.0.0/0` or something different than mine.
![](security.png)

***

## 79. Hands-on Exercise

***

## 80. Hands-on Solution

```
$ cd /Users/marshad/Desktop/golang-web-dev/030_sessions/08_expire-sessio
```

```
# Deploying our session example

1. change your port number from 8080 to 80

1. create your binary
  - GOOS=linux GOARCH=amd64 go build -o [some-name]

1. SSH into your server
  - ssh -i /path/to/[your].pem ubuntu@[public-DNS]:

1. create directories to hold your code
  - for example, "wildwest" & "wildwest/templates"

1. copy binary to the server

1. copy your "templates" to the server
  - scp -i /path/to/[your].pem templates/* ubuntu@[public-DNS]:/home/ubuntu/templates

1. chmod permissions on your binary

1. Run your code
  - sudo ./[some-name]
  - check it in a browser at [public-IP]

# Persisting your application

  To run our application after the terminal session has ended, we must do the following:

  1. Create a configuration file
    - sudo nano /etc/systemd/system/```<filename>```.service

  ```
  [Unit]
  Description=Go Server

  [Service]
  ExecStart=/home/<username>/<path-to-exe>/<exe>
  WorkingDirectory=/home/<username>/<exe-working-dir>
  User=root
  Group=root
  Restart=always

  [Install]
  WantedBy=multi-user.target
  ```

  1. Add the service to systemd.
    - sudo systemctl enable ```<filename>```.service
  1. Activate the service.
    - sudo systemctl start ```<filename>```.service
  1. Check if systemd started it.
    - sudo systemctl status ```<filename>```.service
  1. Stop systemd if so desired.
    - sudo systemctl stop ```<filename>```.service

# FOR EXAMPLE
  ```
  [Unit]
  Description=Go Server

  [Service]
  ExecStart=/home/ubuntu/cowboy
  WorkingDirectory=/home/ubuntu
  User=root
  Group=root
  Restart=always

  [Install]
  WantedBy=multi-user.target
```
```

***

## 81. Terminating `AWS` services

***
