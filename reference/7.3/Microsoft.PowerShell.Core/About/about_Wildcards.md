---
description: Describes how to use wildcard characters in PowerShell.
Locale: en-US
ms.date: 01/26/2022
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.core/about/about_wildcards?view=powershell-7.3&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about Wildcards
---

# about_Wildcards

## Short description

Describes how to use wildcard characters in PowerShell.

## Long description

Wildcard characters represent one or many characters. You can use them to
create word patterns in commands. Wildcard expressions are used with the
`-like` operator or with any parameter that accepts wildcards.

For example, to match all the files in the `C:\Techdocs` directory with a
`.ppt` file name extension, type:

```powershell
Get-ChildItem C:\Techdocs\*.ppt
```

In this case, the asterisk (`*`) wildcard character represents any characters
that appear before the `.ppt` file name extension.

Wildcard expressions are simpler than regular expressions. For more
information, see [about_Regular_Expressions](./about_Regular_Expressions.md).

PowerShell supports the following wildcard characters:

| Wildcard |                         Description                         |   Example   |      Match       | No Match |
| -------- | ----------------------------------------------------------- | ----------- | ---------------- | -------- |
| `*`      | Match zero or more characters                               | `a*`        | aA, ag, Apple    | banana   |
| `?`      | Match one character in that position                        | `?n`        | an, in, on       | ran      |
| `[ ]`    | Match a range of characters                                 | `[a-l\]ook` | book, cook, look | took     |
| `[ ]`    | Match specific characters                                   | `[bc]ook`   | book, cook       | hook     |
| `` `* `` | Match any character as a literal (not a wildcard character) | ``12`*4``   | 12*4             | 1234     |

You can include multiple wildcard characters in the same word pattern. For
example, to find text files with names that begin with the letters **a**
through **l**, type:

```powershell
Get-ChildItem C:\Techdocs\[a-l]*.txt
```

There may be cases where you want to match the literal character rather than
treat it as a wildcard character. In those cases you can use the backtick
(`` ` ``) character to escape the wildcard character so that it is compared
using the literal character value. For example, ``'*hello`?*'`` matches strings
containing "hello?".

Many cmdlets accept wildcard characters in parameter values. The Help topic for
each cmdlet describes which parameters accept wildcard characters. For
parameters that accept wildcard characters, their use is case-insensitive.

You can use wildcard characters in commands and script blocks, such as to
create a word pattern that represents property values. For example, the
following command gets services in which the **ServiceType** property value
includes **Interactive**.

```powershell
Get-Service | Where-Object {$_.ServiceType -Like "*Interactive*"}
```

In the following example, the `If` statement includes a condition that uses
wildcard characters to find property values. If the restore point's
**Description** includes **PowerShell**, the command adds the value of the
restore point's **CreationTime** property to a log file.

```powershell
$p = Get-ComputerRestorePoint
foreach ($point in $p) {
  if ($point.description -like "*PowerShell*") {
    Add-Content -Path C:\TechDocs\RestoreLog.txt "$($point.CreationTime)"
  }
}
```

## See also

- [about_If](about_If.md)
- [about_Language_Keywords](about_Language_Keywords.md)
- [about_Script_Blocks](about_Script_Blocks.md)
