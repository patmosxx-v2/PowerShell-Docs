---
ms.date:  10/18/2018
schema:  2.0.0
locale:  en-us
keywords:  powershell,cmdlet
online version:  http://go.microsoft.com/fwlink/?LinkId=821580
external help file:  Microsoft.PowerShell.Commands.Management.dll-Help.xml
title:  Get-ChildItem
---
# Get-ChildItem

## SYNOPSIS
Gets the items and child items in one or more specified locations.

## SYNTAX

### Items (Default)
```
Get-ChildItem [[-Path] <String[]>] [[-Filter] <String>] [-Include <String[]>] [-Exclude <String[]>] [-Recurse]
 [-Depth <UInt32>] [-Force] [-Name]
 [-Attributes <System.Management.Automation.FlagsExpression`1[System.IO.FileAttributes]>] [-FollowSymlink]
 [-Directory] [-File] [-Hidden] [-ReadOnly] [-System] [<CommonParameters>]
```

### LiteralItems
```
Get-ChildItem -LiteralPath <String[]> [[-Filter] <String>] [-Include <String[]>] [-Exclude <String[]>]
 [-Recurse] [-Depth <UInt32>] [-Force] [-Name]
 [-Attributes <System.Management.Automation.FlagsExpression`1[System.IO.FileAttributes]>] [-FollowSymlink]
 [-Directory] [-File] [-Hidden] [-ReadOnly] [-System] [<CommonParameters>]
```

## DESCRIPTION
The `Get-ChildItem` cmdlet gets the items in one or more specified locations.
If the item is a container, it gets the items inside the container, known as child items.
You can use the `-Recurse` parameter to get items in all child containers and use the `-Depth` parameter to limit the number of levels to recurse.

A location can be a file system location, such as a directory, or a location exposed by a different PowerShell provider, such as a registry hive or a certificate store.

## EXAMPLES

### Example 1: Get child items in the current directory

This command gets the child items in the current location.
If the location is a file system directory, it gets the files and sub-directories in the current directory.
If the item does not have child items, this command returns to the command prompt without displaying anything.

The default display lists the mode (attributes), last write time, file size (length), and the name of the file.
The valid values for mode are `d` (directory), `a` (archive), `r` (read-only), `h` (hidden), and `s` (system).

```powershell
Get-ChildItem
```

### Example 2: Get all files with the specified file extension in the current directory and subdirectories

This command gets all of the ".txt" files in the current directory and its subdirectories.
The `-Recurse` parameter directs PowerShell to get objects recursively, and it indicates that the subject of the command is the specified directory and its contents.
The `-Force` parameter adds hidden files to the display.

```powershell
Get-ChildItem -Path *.txt -Recurse -Force
```

### Example 3: Get all child items using an inclusion and exclusion

This command lists the ".txt" files in the "Logs" subdirectory, except for those whose names start with the letter 'A'.
It uses the wildcard character (`*`) to indicate the contents of the "Logs" subdirectory, not the directory container.
Because the command does not include the `-Recurse` parameter, `Get-ChildItem` does not include the content of sub-directories automatically; you need to specify it.

```powershell
Get-ChildItem -Path C:\Windows\Logs\* -Include *.txt -Exclude A*
```

### Example 4: Get all registry keys in a specific key

This command gets all of the registry keys in the "HKEY_LOCAL_MACHINE\SOFTWARE" key in the registry of the local computer.

```powershell
Get-ChildItem -Path HKLM:\Software
```

### Example 5: Get the name of items in the current directory

This command gets only the names of items in the current directory.

```powershell
Get-ChildItem -Name
```

### Example 6: Get all certificates in a certification drive that have code-signing authority

This command gets all of the certificates in the PowerShell `Cert:` drive that have code-signing authority.

This command uses the `Get-ChildItem` cmdlet.

- The value of the `-Path` parameter is the Cert: drive.
- The `-Recurse` parameter requests a recursive search.
- The `-CodeSigningCert` parameter is a dynamic parameter that the Certificate provider adds to the `Get-ChildItem` cmdlet. This parameter gets only certificates that have code-signing authority.

For more information about the Certificate provider and the Cert: drive, go to [Certificate Provider](../microsoft.powershell.security/About/about_Certificate_Provider.md) or use the `Update-Help` cmdlet to download the help files for the Microsoft.PowerShell.Security module and then type `Get-Help Certificate`.

```powershell
Get-ChildItem -Path Cert:\* -Recurse -CodeSigningCert
```

### Example 7: Get all items in the specified directory and its subdirectories that have an inclusion and exclusion

This command gets all of the items in the "C:\Windows" directory and its subdirectories that have "mouse" in the file name, except for those with a ".png" file name extension.

```powershell
Get-ChildItem -Path C:\Windows -Include *mouse* -Exclude *.png
```

### Example 8: Get all items in the specified directory and its subdirectories limited by the Depth parameter

This command gets all of the items in the "C:\Windows" directory and its subdirectories up to 2 level below in depth.

```powershell
Get-ChildItem -Path C:\Windows -Depth 2
```

## Parameters

### -Attributes

Gets files and folders with the specified attributes. This parameter supports all attributes and lets you specify complex combinations of attributes.

For example, to get non-system files (not directories) that are encrypted or compressed, type:

`Get-ChildItem -Attributes !Directory+!System+Encrypted, !Directory+!System+Compressed`

To find files and folders with commonly used attributes, you can use the `-Attributes` parameter, or the `-Directory`, `-File`, `-Hidden`, `-ReadOnly`, and `-System` switch parameters.

The `-Attributes` parameter supports the following attributes:

- **Archive**
- **Compressed**
- **Device**
- **Directory**
- **Encrypted**
- **Hidden**
- **IntegrityStream**
- **Normal**
- **NoScrubData**
- **NotContentIndexed**
- **Offline**
- **ReadOnly**
- **ReparsePoint**
- **SparseFile**
- **System**
- **Temporary**

For a description of these attributes, see the [FileAttributes Enumeration](/dotnet/api/system.io.fileattributes).

Use the following operators to combine attributes:

- `!`   (NOT)
- `+`   (AND)
- `,`   (OR)

No spaces are permitted between an operator and its attribute. However, spaces are permitted before commas.

You can use the following abbreviations for commonly used attributes:

- `D`   (Directory)
- `H`   (Hidden)
- `R`   (Read-only)
- `S`   (System)

```yaml
Type: System.Management.Automation.FlagsExpression`1[System.IO.FileAttributes]
Parameter Sets: (All)
Aliases:
Accepted values: ReadOnly, Hidden, System, Directory, Archive, Device, Normal, Temporary, SparseFile, ReparsePoint, Compressed, Offline, NotContentIndexed, Encrypted, IntegrityStream, NoScrubData

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Depth

This parameter, added in Windows Powershell 5.0 enables you to control the depth of recursion.
You use both the `-Recurse` and the `-Depth` parameter to limit the recursion.

```yaml
Type: UInt32
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Directory

Gets directories (folders).

To get only directories, use the `-Directory` parameter and omit the `-File` parameter. To exclude directories, use the `-File` parameter and omit the `-Directory` parameter, or use the `-Attributes` parameter.

To get directories, use the Directory parameter, its `ad` alias, or the Directory attribute of the `-Attributes` parameter.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: ad, d

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Exclude

Specifies, as a string array, a property or property that this cmdlet excludes from the operation.
The value of this parameter qualifies the **Path** parameter.
Enter a path element or pattern, such as "*.txt".
Wildcard characters are permitted.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -File

Gets files.

To get only files, use the `-File` parameter and omit the Directory parameter. To exclude files, use the `-Directory` parameter and omit the `-File` parameter, or use the `-Attributes` parameter.

To get files, use the File parameter, its `af` alias, or the File value of the `-Attributes` parameter.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: af

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Filter

Specifies a filter in the format or language of the provider.
The value of this parameter qualifies the **Path** parameter.

The syntax of the filter, including the use of wildcard characters, depends on the provider.
Filters are more efficient than other parameters, because the provider applies them when the cmdlet gets the objects rather than having PowerShell filter the objects after they are retrieved.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -FollowSymlink
{{Fill FollowSymlink Description}}

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -FollowSymlink

By default, the `Get-ChildItem` cmdlet displays symbolic links to directories found during recursion, but does not recurse into them.
Use the **FollowSymlink** switch to search the directories that those symbolic links target.
The **FollowSymlink** is a dynamic parameter and it is supported only in the FileSystem provider.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Force

Allows the cmdlet to get items that cannot otherwise not be accessed by the user, such as hidden or system files.
Implementation varies among providers.

For more information, see [about_Provider](../Microsoft.PowerShell.Core/About/about_Providers.md).

Even when using the `-Force` parameter, the cmdlet cannot override security restrictions.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Hidden

Gets only hidden files and directories (folders).  By default, `Get-ChildItem` gets only non-hidden items, but you can use the `-Force` parameter to include hidden items in the results.

To get only hidden items, use the `-Hidden` parameter, its `h` or `ah` aliases, or the Hidden value of the `-Attributes` parameter. To exclude hidden items, omit the `-Hidden` parameter or use the `-Attributes` parameter.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: ah, h

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Include

Specifies, as a string array, an item or items that this cmdlet includes in the operation.
The value of this parameter qualifies the **Path** parameter.
Enter a path element or pattern, such as "*.txt".
Wildcard characters are permitted.

The `-Include` parameter is effective only when the command includes the `-Recurse` parameter or the path leads to the contents of a directory, such as C:\Windows\*, where the "`*`" wildcard character specifies the contents of the C:\Windows directory.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -LiteralPath

Specifies a path to one or more locations.
Unlike the **Path** parameter, the value of **LiteralPath** is used exactly as it is typed.
No characters are interpreted as wildcards.
If the path includes escape characters, enclose it in single quotation marks.
Single quotation marks tell PowerShell not to interpret any characters as escape sequences.

```yaml
Type: String[]
Parameter Sets: LiteralItems
Aliases: PSPath

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Name

Gets only the names of the items in the locations.
If you pipe the output of this command to another command, only the item names are sent.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path

Specifies a path to one or more locations.
Wildcards are permitted.
The default location is the current directory (`.`).

```yaml
Type: String[]
Parameter Sets: Items
Aliases:

Required: False
Position: 0
Default value: Current directory
Accept pipeline input: True (ByPropertyName, ByValue)
Accept wildcard characters: False
```

### -ReadOnly

Gets only read-only files and directories (folders).

To get only read-only items, use the `-ReadOnly` parameter, its `ar` alias, or the ReadOnly value of the `-Attributes` parameter. To exclude read-only items, use the `-Attributes` parameter.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: ar

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Recurse

Gets the items in the specified locations and in all child items of the locations.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: s

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -System

Gets only system files and directories (folders).

To get only system files and folders, use the `-System` parameter, its `as` alias, or the System value of the `-Attributes` parameter. To exclude system files and folders, use the `-Attributes` parameter.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: as

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### System.String

You can pipe a string that contains a path to `Get-ChildItem`.

## OUTPUTS

### System.Object

The type of object that `Get-ChildItem` returns is determined by the objects in the provider drive path.

### System.String

If you use the `-Name` parameter, `Get-ChildItem` returns the object names as strings.

## NOTES

You can also refer to `Get-ChildItem` by its built-in aliases, `ls`, `dir`, and `gci`. For more information, see [about_Aliases](../Microsoft.PowerShell.Core/About/about_Aliases.md).

`Get-ChildItem` does not get hidden items by default.
To get hidden items, use the `-Force` parameter.

The `Get-ChildItem` cmdlet is designed to work with the data exposed by any provider.
To list the providers available in your session, type `Get-PSProvider`.

For more information, see [about_Providers](../Microsoft.PowerShell.Core/About/about_Providers.md).

## RELATED LINKS

[Get-Alias](../Microsoft.PowerShell.Utility/Get-Alias.md)

[Get-Item](Get-Item.md)

[Get-Location](Get-Location.md)

[Get-Process](Get-Process.md)

[Get-PSProvider](Get-PSProvider.md)

[about_Providers](../Microsoft.PowerShell.Core/About/about_Providers.md)
