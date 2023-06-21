# Show All Wi-Fi Passwords with the Command Prompt

> Author: David Boyd<br>
> Updated: 2023-03-31

## Command Prompt

``` batch
# Print all profiles and their properties
for /f "skip=9 tokens=1,2 delims=:" %i in ('netsh wlan show profiles') do @echo %j | findstr -i -v echo | netsh wlan show profiles %j key=clear
```

### Powershell & Cmd Prompt
```
# 1. Show Saved Profile
netsh wlan show profiles

# 2. Show password
netsh wlan show profile <ESSID> key=clear
```

