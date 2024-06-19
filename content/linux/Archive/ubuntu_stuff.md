---
title: How to Get Putty to Work in Ubuntu
date: 2023-11-06T06:20:36-07:00
draft: true
---
**Add this stuff to the top of /etc/ssh/ssh_config**

KexAlgorithms=+diffie-hellman-group1-sha1

Ciphers aes128-ctr,aes192-ctr,aes256-ctr,aes128-cbc,3des-cbc

HostKeyAlgorithms ssh-rsa

PubkeyAcceptedKeyTypes ssh-rsa

# Getting putty to work in Ubuntu

sudo apt-get update

sudo apt install putty

Go to fonts menu and change fonts to Ubuntu.
