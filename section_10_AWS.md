## 75. Overview

***

## 76. Creating a virtual server instance on `AWS EC2`

### Create an instance

* Create an `AWS Account`
 - enter credit card info

* Sign into console

* 1. Create a new `EC2` instance
    - services / EC2
    - `Launch Instance`
    - choose your instance (`t2.micro`)
    - add storage / 30GB free 
    - add tags / web-server-mm-dd-yyyy
    - security / ssh / http
    - launch
    - create new key-pair (`kp-mm-dd-yyyy`) / download

***

## 77. Hello World on `AWS`

### Deploy your binary

```
$ mv ~/Downloads/kp-mm-dd-yyyy.pem ~/.ssh
```

```
$ sudo chmod 400 kp-mm-dd-yyy.pem
```

### Build Hello World
```
$ cd ~/Desktop/.../032_AWS
$ GOOS=linux GOARCH=amd64 go build -o mybinary
```

### Copy your binary to the sever
```
$ scp -i /path/to/[your].pem ./main ec2-user@[public-DNS]:
 - "ec2-user" might be "ubuntu" depending upon your machine
 - say "yes" to The authenticity of host ... can't be established.
```

### SSH into your server

```
$ ssh -i /path/to/[your].pem ec2-user@[public-DNS]
```

### Run your code
```
$ sudo yum update??
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
    - init.d
    - upstart
    - system.d

* `System.d`

```
# Create a configuration file
$ cd /etc/systemd/system/
$ sudo nano ```<filename>```.service
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

### Add the service to systemd.

```
$ sudo systemctl enable ```<filename>```.service
```

### Activate the service.

```
$ sudo systemctl start ```<filename>```.service
```

### Check if systemd started it.

```
$ sudo systemctl status ```<filename>```.service
```

### Stop systemd if so desired.

```
$ sudo systemctl stop ```<filename>```.service
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
    - nano .bashrc

export GOROOT=/home/ubuntu/go
export GOPATH=/home/ubuntu/goworkspace
export PATH=$PATH:/home/ubuntu/goworkspace/bin
export PATH=$PATH:/home/ubuntu/go/bin
```

```
* refresh environment variables
  - source ~/.bashrc
* confirm installation
  - go version
* get machine GOOS & GOARCH info
  - go env
```

### Troubleshooting

Sometimes students miss setting port openings in security. If you are having issues, check to make sure these settings are correct - and please note, you IP address for SSH will either be 0.0.0.0/0 or something different than mine.
![](security.png)

***

## 79. Hands-on Exercise

***

## 80. Hands-on Solution

***

## 81. Terminating `AWS` services

***
