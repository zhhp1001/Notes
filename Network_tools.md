
# ERR_CONNECTION_REFUSED
**Reference**: https://stackoverflow.com/questions/21206995/cant-connect-to-a-computer-that-i-can-ping

Try connecting to the peer with `telnet <ip> <port>`. If it says Connection refused, it is likely that the other host is reachable, but there is nothing listening on the port. If there is no response (packet is dropped), it is likely a filter blocking the connection.
## traceroute
To see the intermediate hosts
```bash
traceroute -n <ip>
```
### Windows CMD
```bash
tracert <ip>
```

## nmap
This will tell you which ports are open and blocked.
```bash
nmap <ip>
```

