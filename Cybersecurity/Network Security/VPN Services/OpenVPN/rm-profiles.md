# How to Remove Profiles in OpenVPN

**Author:** David Boyd<br>
**Updated:** 2023-06-24

## Windows

### PowerShell

``` PowerShell
Remove-Item -Recurse -Force %USER%\OpenVPN\config\<profile>
```

