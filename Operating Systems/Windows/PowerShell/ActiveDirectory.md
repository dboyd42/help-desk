# PowerShell's Active Directory

**Author:** David Boyd<br>
**Date:** 2024-11-02

## Table of Contents

## Installation

### Windows Server or Windows 10/11 with RSAT

:pencil: *RSAT = Remote Server Administration Tools*

1. Install the RSAT Tools

    `Add-WindowsCapability -Online -Name Rsat.ActiveDirectory.DS-LDS.Tools~~~~0.0.1.0`

2. Enable RSAT Active Directory

    `Add-WindowsFeature -Name "RSAT-AD-PowerShell`

3. Import the Module

    `Import-Module ActiveDirectory`

### PowerShell Core

:computer: Use the **Active Directory Cross-Platform Module**

  1. `Install-Module -Name DirectoryServices`
  2. `Import-Module DirectoryServices`


## PowerShell Basics

``` powershell
# Variables
$var = "string"

# Arrays
$arr = @("one", "banana")

# AD-Object Emails
$email = "smtp:user@company.com"
```

## AD-User

``` powershell

$user = "flast"  # first name, last name

# Retrieve AD User by Name
Get-ADUser -Filter { Name -like "*$user*" }

# Retrieve AD User by SamAccountName
Get-ADUser -Filter { SamAccountName -like "*$user*" }

# Retrieve and list group memberships of a user
Get-ADUser -Identity $user -Properties MemberOf | ForEach-Object {
  $_.MemberOf | ForEach-Object {
    Get-ADGroup -Identity $_ | Select-Object -ExpandProperty Name
  }
}

# Filter group memberships by pattern
$pattern = "*egnyte*"
Get-ADUser -Identity $user -Properties MemberOf | ForEach-Object {
  $_.MemberOf | ForEach-Object {
    $group = Get-ADGroup -Identity $_
    if ($group.Name -like $pattern) {
      $group.Name
    }
  }
}

# Another method to filter group memberships by pattern
$pattern = "a_string"
Get-ADUser -Identity $user -Properties MemberOf | ForEach-Object {
  $_.MemberOf | Where-Object {
    $_ -like "*$pattern*"
  } | ForEach-Object {
    Get-ADGroup -Identity $_ | Select-Object -ExpandProperty Name
  }
}
```

## ProxyAddresses

``` powershell
$newEmail = "smtp:user@company.com"

# Retrieve the proxyAddresses property for a user
Get-ADUser -Identity $user -Properties proxyAddresses | Select-Object -ExpandProperty proxyAddresses

# Another method to retrieve proxyAddresses
(Get-ADUser -Identity $user -Properties proxyAddresses).proxyAddresses

# Add a new email address to the proxyAddresses property
Set-ADUser -Identity $user -Add @{proxyAddresses=$newEmail}
```

## Passwords

``` powershell
# Calculate days until password expiry
([datetime]::FromFileTime((Get-ADUser -Identity $user -Properties "msDS-UserPasswordExpiryTimeComputed")."msDS-UserPasswordExpiryTimeComputed") - (Get-Date)).Days

$pass = "myPassword"
# Set a new password for the user
Set-ADAccountPassword -Identity $user -NewPassword (ConvertTo-SecureString -AsPlainText $pass -Force)

# Unlock the user's account
Unlock-ADAccount -Identity $user
```


## Groups

``` powershell
# Fetch the members' names (type: strings)
(Get-ADGroupMember -Identity "AGroupName").Name

# Fetch the members' properties (type: objects)
$members = Get-ADGroupMember -Identity $group

# Search for a member through the list of objects
$members.Name | Select-String -Pattern "a_pattern"

# Add a user to a group
Add-ADGroupMember -Identity $group -Members $user
```
<!-- References -->
