## Tue 23/06/20
### Stopping certain port on windows
```bash
C:\> netstat -ano -p TCP | find /I "listening" | find /I "5000"
    TCP    127.0.0.1:5000         0.0.0.0:0              LISTENING       7148
```

```bash
C:\> taskkill /F /PID 7148
    SUCCESS: The process with PID 7148 has been terminated.
```

---
