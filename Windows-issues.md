## Mon 12/10/20
### PostgreSQL Windows Installation Problem running post-install step. Installation may not complete correctly.

- Uninstall PostgreSQL (If installed incorrectly)
- Run command: `net user postgres /delete` [*Deletes **postgres** user if it already exists*]
- Open **Control Panel** -> **User Accounts** -> **Configure advanced user profile properties** -> delete all *Unknown User* instances that seem to be left from PostgreSQL installation.
- Run command: `net user postgres dbpass /add` [*Creates another new user **postgres** with password **dbpass** *]
- Run: `compmgmt.msc` -> Click **Local Users and Groups** -> **Users** -> *postgres* -> Click **Member of** Tab -> **Add…** -> **Administrators** -> **OK**
- Run: `runas /user:postgres cmd.exe` to login as user *postgres* -> `cd \` -> `postgresql-13.0-1-windows-x64.exe` -> Installed successfully without errors. Checked data folder and confirmed files created successfully.
- Now Run: `compmgmt.msc` -> **Local Users and Groups** -> **Users** -> *postgres* -> **Member of** -> **Administrators** -> **Remove**
- Again Run: `compmgmt.msc` -> **Local Users and Groups** -> **Users** -> *postgres* -> **Member of** -> **Add…** -> **Power Users** -> **OK**
- Finally set **Environment Variable PATH** `C:\Program Files\PostgreSQL\13\bin;C:\Program Files\PostgreSQL\13\lib;`

---

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
