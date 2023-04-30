Power Shell
===========


Help
----

```powershell
# Get Command Help
# https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/get-help
Get-Help <command>
Get-Help <command> -Detailed
Get-Help <command> -Full
```

Remove files and directories (recursively)
------------------------------------------

```powershell
# Remove directory recursively
Remove-Item -Path out/ -recurse -force
Remove-Item -Path E:/TEMP/out -recurse -force

# Find a file/directory
Get-Childitem –Path . -Recurse
Get-ChildItem -Path . -Recurse -File -Include ".clang-format"
Get-Childitem –Path C:\ -Include *HSG* -Exclude *.JPG,*.MP3,*.TMP -File -Recurse -ErrorAction SilentlyContinue

# Find files/directories and show only absolute path as list
Get-ChildItem -Path . -Recurse -Include ".vscode" |  %{$_.FullName}

# Find files/directories, filtered by extension and show only absolute path as list
Get-ChildItem -Path C:\New -Recurse | where {$_.extension -eq ".txt"} | %{$_.FullName}

# Find files/directories and get the full path of files
Get-ChildItem -Path C:\New -Filter *.txt -Recurse | Select-Object -ExpandProperty FullName

# Find files/directories and format the result as table
Get-ChildItem -Path C:\ -Filter *.txt -Recurse | Format-Table FullName

# Get absolute file path of <executable name>
Get-Command <executable name>

# Get file properties
Get-Command <executable name> | Select-Object *

# Configuring UTF-8 encoding
chcp 65001

```

Environment Path
----------------

```powershell
# Print environment variables
Get-ChildItem env:

# Print environment variable: PATH
Get-ChildItem env:PATH

# Print PATH for logged User
[System.Environment]::GetEnvironmentVariable("PATH", "User")

# Set Path
$Env:PATH += ";$pwd"

# Set Path, getting the path separator defined in the environment
$Env:Path += [IO.Path]::PathSeparator + $pwd

# Function to add a patch
function Add-Path($Path) {
    $Path = [Environment]::GetEnvironmentVariable("PATH", "Machine") + [IO.Path]::PathSeparator + $Path
    [Environment]::SetEnvironmentVariable( "Path", $Path, "Machine" )
}
```

# Process

[https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/start-process](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/start-process?view=powershell-7.3)

[https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-process](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-process)

[https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/stop-process](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/stop-process?view=powershell-7.3)

- Get the Process on a local or remote computer
- How to use commands:

```powershell
# Start-Process
Start-Process -FilePath <Executable Filename>

Start-Process -FilePath <Executable Filename> -WorkingDirectory <Filename>

Start-Process -FilePath <Executable Filename> -Wait -WindowStyle Maximized
-WindowStyle Hidden

Start-Process -FilePath <Executable Filename> -ArgumentList <arg 1>, <arg 2>,..., <arg n>
where <arg n> may be between quotes: "dir"

If you use a variable:
	$args = '-noprofile -command "Start-Process cmd.exe -Verb RunAs -args /k"'
Start-Process pwsh.exe -WindowStyle Hidden -AgumentList $args

# Start a process as Administrator
Start-Process -FilePath <Executable Filename> -Verb RunAs

# Get-Process
Get-Process

Get-Process <Process Name>

Get-Process -Name [<Process Name> | <or Masks>]

Get-Process -Id <Id>

# With Format-List
Get-Process <Process Name> | Format-List *

# Libraries loaded
Get-Process <Process Name> -Module

# Owner the process (but it requires Elevated User Rights)
Get-Process <Process Name> -IncludeUserName

# Stop-Process
Stop-Process -Name <Process Name>
Stop-Process -Id <Process Id> -Confirm -PassThru

# Stop a process and detect that it has stopped
$p = Get-Process -Name "calc"
Stop-Process -InputObject $p
Get-Process | Where-Object {$_.HasExited}

# Get Process and Stop it
Get-Process -Name <Process Name> | Stop-Process -Force
```
