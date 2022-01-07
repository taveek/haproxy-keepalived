# เตรียมเครื่อง

```sh
vagrant up
```

# Execution

```sh
ansible-playbook -i hosts playbook.yaml
```

# ทดสอบ

```sh
curl http://10.10.0.10
```

# check vip

```sh
vagrant ssh haproxy1 -c "ip --brief add"
```

# ทดสอบ failover

```sh
# down server1
vagrant ssh haproxy1 -c "sudo ip link set enp0s8 down"

# vip backup is on
vagrant ssh haproxy2 -c "ip --brief add"

# bringback server1
vagrant ssh haproxy1 -c "sudo ip link set enp0s8 up"

# vip master is on
vagrant ssh haproxy1 -c "ip --brief add"

# down server1 and server2
vagrant ssh haproxy1 -c "sudo ip link set enp0s8 down"
vagrant ssh haproxy2 -c "sudo ip link set enp0s8 down"

# failed
curl http://10.10.0.10
```


# References

* [Configure Highly Available HAProxy with Keepalived on Ubuntu 20.04](https://kifarunix.com/configure-highly-available-haproxy-with-keepalived-on-ubuntu-20-04/)
* [An Introduction to HAProxy and Load Balancing Concepts](https://www.digitalocean.com/community/tutorials/an-introduction-to-haproxy-and-load-balancing-concepts)
