winget
======

**Ref.** [https://learn.microsoft.com/en-us/windows/package-manager/](https://learn.microsoft.com/en-us/windows/package-manager/)

```powershell
winget install <Package Name>
winget install pandoc
winget install ntop

# Installation Path: "C:\Users\user\AppData\Local\Microsoft\WinGet\Packages"
# Pandoc is installed in "C:\Users\user\AppData\Local\Pandoc" but shouldn't it be
# created under "C:\Users\user\AppData\Local\Microsoft\WinGet\Links"?
# In case of "ntop", it's installed under "# C:\Users\user\AppData\Local\Microsoft\WinGet\Packages"
# and there's a link in  "# C:\Users\user\AppData\Local\Microsoft\WinGet\Links"

# Question: How can I add this installation path to the Environment PATH variable?
# Answer: add "C:\Users\user\AppData\Local\Microsoft\WinGet\Packages" to the PATH variable
#         under "My Computer" advanced properties.

winget show <Package Name>

```
