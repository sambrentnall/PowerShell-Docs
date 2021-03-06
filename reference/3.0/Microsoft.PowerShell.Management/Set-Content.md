---
description:  
manager:  carmonm
ms.topic:  reference
author:  jpjofre
ms.prod:  powershell
keywords:  powershell,cmdlet
ms.date:  2016-12-12
title: Set-Content
ms.technology:  powershell
schema:   2.0.0
online version:   http://go.microsoft.com/fwlink/?LinkID=113392
external help file:   Microsoft.PowerShell.Commands.Management.dll-Help.xml
---


# Set-Content
## SYNOPSIS
Writes or replaces the content in an item with new content.
## SYNTAX

### Path (Default)
```
Set-Content [-Value] <Object[]> [-PassThru] [-Path] <String[]> [-Filter <String>] [-Include <String[]>]
 [-Exclude <String[]>] [-Force] [-Credential <PSCredential>] [-WhatIf] [-Confirm] [-UseTransaction]
 [-Encoding <FileSystemCmdletProviderEncoding>] [-Stream <String>] [<CommonParameters>]
```

### LiteralPath
```
Set-Content [-Value] <Object[]> [-PassThru] -LiteralPath <String[]> [-Filter <String>] [-Include <String[]>]
 [-Exclude <String[]>] [-Force] [-Credential <PSCredential>] [-WhatIf] [-Confirm] [-UseTransaction]
 [-Encoding <FileSystemCmdletProviderEncoding>] [-Stream <String>] [<CommonParameters>]
```

## DESCRIPTION
The Set-Content cmdlet is a string-processing cmdlet that writes or replaces the content in the specified item, such as a file.
Whereas the Add-Content cmdlet appends content to a file, Set-Content replaces the existing content.
You can type the content in the command or send content through the pipeline to Set-Content.
## EXAMPLES

### Example 1
```
PS C:\> set-content -path C:\Test1\test*.txt -value "Hello, World"
```

This command replaces the contents of all files in the Test1 directory that have names beginning with "test" with "Hello, World".
This example shows how to specify content by typing it in the command.
### Example 2
```
PS C:\> get-date | set-content C:\Test1\date.csv
```

This command creates a comma-separated variable-length (csv) file that contains only the current date and time.
It uses the Get-Date cmdlet to get the current system date and time.
The pipeline operator passes the result to Set-Content, which creates the file and writes the content.

If the Test1 directory does not exist, the command fails, but if the file does not exist, the command will create it.
### Example 3
```
PS C:\> (get-content Notice.txt) | foreach-object {$_ -replace "Warning", "Caution"} | set-content Notice.txt
```

This command replaces all instances of "Warning" with "Caution" in the Notice.txt file.

It uses the Get-Content cmdlet to get the content of Notice.txt.
The pipeline operator sends the results to the ForEach-Object cmdlet, which applies the expression to each line of content in Get-Content.
The expression uses the "$_" symbol to refer to the current item and the Replace parameter to specify the text to be replaced.

Another pipeline operator sends the changed content to Set-Content which replaces the text in Notice.txt with the new content.

The parentheses around the Get-Content command ensure that the Get operation is complete before the Set operation begins.
Without them, the command will fail because the two functions will be trying to access the same file.
## PARAMETERS

### -Encoding
Specifies the file encoding. The default is ASCII.

Valid values are:

-- ASCII:  Uses the encoding for the ASCII (7-bit) character set.
-- BigEndianUnicode:  Encodes in UTF-16 format using the big-endian byte order.
-- Byte:   Encodes a set of characters into a sequence of bytes.
-- String:  Uses the encoding type for a string.
-- Unicode:  Encodes in UTF-16 format using the little-endian byte order.
-- UTF7:   Encodes in UTF-7 format.
-- UTF8:  Encodes in UTF-8 format.
-- Unknown:  The encoding type is unknown or invalid. The data can be treated as binary.

Encoding is a dynamic parameter that the FileSystem provider adds to the Set-Content cmdlet. This parameter works only in file system drives.```yaml
Type: FileSystemCmdletProviderEncoding
Parameter Sets: (All)
Aliases: 
Accepted values: Unknown, String, Unicode, Byte, BigEndianUnicode, UTF8, UTF7, UTF32, Ascii, Default, Oem

Required: False
Position: Named
Default value: ASCII
Accept pipeline input: False
Accept wildcard characters: False
```

### -Force
Allows the cmdlet to set the contents of a file, even if the file is read-only.
Implementation varies from provider to provider.
For more information, see about_Providers.
Even using the Force parameter, the cmdlet cannot override security restrictions.

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

### -Stream
Creates or replaces the content in the specified alternate data stream. If the stream does not yet exist, Set-Content creates it. Enter the stream name. Wildcards are not supported.

Stream is a dynamic parameter that the FileSystem provider adds to the Set-Content cmdlet. This parameter works only in file system drives.

You can use the Set-Content cmdlet to change the content of the Zone.Identifier alternate data stream. However, it is not the recommended way to eliminate security checks that block files that are downloaded from the Internet. If you verify that a downloaded file is safe, use the Unblock-File cmdlet.

This parameter is introduced in Windows PowerShell 3.0.```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Confirm
Prompts you for confirmation before running the cmdlet.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: cf

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -WhatIf
Shows what would happen if the cmdlet runs.
The cmdlet is not run.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: wi

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -UseTransaction
Includes the command in the active transaction.
This parameter is valid only when a transaction is in progress.
For more information, see about_Transactions.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: usetx

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Credential
Specifies a user account that has permission to perform this action.
The default is the current user.

Type a user name, such as "User01" or "Domain01\User01", or enter a PSCredential object, such as one generated by the Get-Credential cmdlet.
If you type a user name, you will be prompted for a password.

This parameter is not supported by any providers installed with Windows PowerShell.

```yaml
Type: PSCredential
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: Current user
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Exclude
Omits the specified items.
The value of this parameter qualifies the Path parameter.
Enter a path element or pattern, such as "*.txt".
Wildcards are permitted.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: True
```

### -Filter
Specifies a filter in the provider's format or language.
The value of this parameter qualifies the Path parameter.
The syntax of the filter, including the use of wildcards, depends on the provider.
Filters are more efficient than other parameters, because the provider applies them when retrieving the objects, rather than having Windows PowerShell filter the objects after they are retrieved.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: True
```

### -Include
Changes only the specified items.
The value of this parameter qualifies the Path parameter.
Enter a path element or pattern, such as "*.txt".
Wildcards are permitted.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: True
```

### -LiteralPath
Specifies the path to the item that will receive the content.
Unlike Path, the value of LiteralPath is used exactly as it is typed.
No characters are interpreted as wildcards.
If the path includes escape characters, enclose it in single quotation marks.
Single quotation marks tell Windows PowerShell not to interpret any characters as escape sequences.

```yaml
Type: String[]
Parameter Sets: LiteralPath
Aliases: PSPath

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -PassThru
Returns an object representing the content.
By default, this cmdlet does not generate any output.

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

### -Path
Specifies the path to the item that will receive the content.
Wildcards are permitted.

```yaml
Type: String[]
Parameter Sets: Path
Aliases: 

Required: True
Position: 1
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: True
```

### -Value
Specifies the new content for the item.

```yaml
Type: Object[]
Parameter Sets: (All)
Aliases: 

Required: True
Position: 2
Default value: None
Accept pipeline input: True (ByPropertyName, ByValue)
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
## INPUTS

### System.Object
You can pipe an object that contains the new value for the item to Set-Content.
## OUTPUTS

### None or System.String
When you use the Passthru parameter, Set-Content generates a System.String object representing the content.
Otherwise, this cmdlet does not generate any output.
## NOTES
* You can also refer to Set-Content by its built-in alias, "sc". For more information, see about_Aliases.

  Set-Content is designed for string processing.
If you pipe non-string objects to Set-Content, it converts the object to a string before writing it.
To write objects to files, use Out-File.

  The Set-Content cmdlet is designed to work with the data exposed by any provider.
To list the providers available in your session, type "Get-PsProvider".
For more information, see about_Providers.

*
## RELATED LINKS

[Add-Content](Add-Content.md)

[Clear-Content](Clear-Content.md)

[Get-Content](Get-Content.md)

[about_Providers](../Microsoft.PowerShell.Core/About/about_Providers.md)


