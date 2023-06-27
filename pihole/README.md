# Pihole
## Port 53 problem
If exists problems with port 53 do the following:

```
sudo lsof -i -P -n | grep LISTEN
```
or
```
sudo lsof -i :53
```

This will list connections on the machine and identify the ports being used, there should be port `53` in use, on `systemd-resolved` service.
To solve this, you need to edit a file:

```
sudo nano /etc/systemd/resolved.conf
```

On the file uncomment `DNSStubListener` and ensure it is set to `no`.
Then restart the service with:

```
sudo service systemd-resolved restart
```

After the service restart the problem should be solved.
