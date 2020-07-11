после поднятия стенда порты для открытия можно узнать из вывода по команде:

```
rpcinfo -p|awk '{print $4}'|uniq
```

и открыть их в firewall, т.к. для nfs используется udp, открываем только этот трафик

```
firewall-cmd \
--add-port=50370/udp \
--add-port=52169/udp \
--add-port=20048/udp \
--add-port=2049/udp \
--add-port=42494/udp \
--add-port=41310/udp \
--permanent
firewall-cmd --permanent --add-service=nfs
firewall-cmd --permanent --add-service=mountd
firewall-cmd --permanent --add-service=rpc-bind
firewall-cmd --reload
```

Дополнительно:
http://www.rhd.ru/docs/manuals/enterprise/RHEL-4-Manual/sysadmin-guide/s1-nfs-mount.html
