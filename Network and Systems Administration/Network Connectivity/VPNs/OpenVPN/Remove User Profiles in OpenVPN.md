# How to Remove User Profiles in OpenVPN

**Author:** David Boyd<br>
**Updated:** 2023-08-03

## Remove Profiles

The purpose of removing profiles was to initially act as a workaround to
prevent default profiles from acting on their own and/or to ensure importing
profiles to overwrite same names. Nevertheless, knowing the location of these
profiles can prove beneficial for other means.

1. Open PowerShell and run the following command:

``` powershell
Remove-Item -Recurse -Force %USER%\OpenVPN\config\<profile>
```


