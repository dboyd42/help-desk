# PowerShell Access Control List Commands

**Author:** David Boyd<br>
**Date:** 2024-11-02

## Table of Contents

## Get-Acl

### List all Security Groups and their Properties' Access Rights

``` powershell
$folderPath = "C:\path\to\folder"

# [Method 1]
# Get The Acl For The Specified Folder And Select Key Properties For Display
(Get-Acl $folderPath).Access | Select-Object IdentityReference, FileSystemRights, AccessControlType | Format-Table -AutoSize

$folderPath = "C:\path\to\folder"

# [Method 2]
Get-Acl $folderPath | ForEach-Object {
  $acl = $_
  # Iterate over each access rule in the Access Control List (ACL)
  ForEach ($accessRule in $acl.Access) {
    # Iterate over each property of the access rule
    ForEach ($property in $accessRule | Get-Member -MemberType Properties) {
      $propertyName = $property.Name
      # Output the property name and its value
      Write-Output "$propertyName : $($accessRule.$propertyName)"
    }
    # Output an empty line for readability
    Write-Output ""
  ```

<!-- References -->
