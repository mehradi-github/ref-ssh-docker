# Enabling SSH within a Docker Container

```Dockerfile
FROM ubuntu:latest

RUN apt update && apt install  openssh-server sudo -y

RUN useradd -rm -d /home/ubuntu -s /bin/bash -g root -G sudo -u 1000 test 

RUN  echo 'test:test' | chpasswd

RUN service ssh start

EXPOSE 22

CMD ["/usr/sbin/sshd","-D"]
```
## ssh
```sh
docker build -t [IMAGE_NAME] .
docker run -dit --name [Container Name] -p [PORT]:22 [IMAGE_NAME]
ssh test@[ip_address of Docker Host OS] -p [PORT]

```
## Ansible
```yaml
- name: Change ssh port to [PORT]
  set_fact:
    ansible_port: [PORT]
```