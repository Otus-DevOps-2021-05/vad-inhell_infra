# vad-inhell_infra
vad-inhell Infra repository

1. SSH
bastion_IP = 178.154.254.38
someinternalhost_IP = 10.130.0.31

touch ~/.ssh/config внего вносим:

appuser@stud:~$ cat ~/.ssh/config
host someinternalhost
   Hostname 10.130.0.31
   User appuser
   Identityfile ~/.ssh/appuser
   Port 22
   ProxyCommand ssh -i ~/.ssh/appuser -A appuser@178.154.254.38 -p 22 -W %h:%p
appuser@stud:~$

2. после настройки впн сервера , на сервере необходимо настроить iptables:
root@bastion:~# history |grep iptables
  134  sudo iptables -A INPUT -p udp -m udp --sport 9700 --dport 1025:65355 -j ACCEPT
  135  sudo iptables -A INPUT -p tcp -m tcp --sport 9700 --dport 1025:65355 -j ACCEPT
