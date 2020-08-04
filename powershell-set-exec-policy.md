# PowerShell 

By default, Windows *PowerShell* would not run a `.ps1` script... because security:

```PowerShell
PS C:\Local\resume\python-junior-mid> .\build.ps1
.\build.ps1 : File C:\Local\resume\python-junior-mid\build.ps1 cannot be loaded because
running scripts is disabled on this system. For more information, see
about_Execution_Policies at https:/go.microsoft.com/fwlink/?LinkID=135170.
At line:1 char:1
+ .\build.ps1
+ ~~~~~~~~~~~
    + CategoryInfo          : SecurityError: (:) [], PSSecurityException
    + FullyQualifiedErrorId : UnauthorizedAccess
PS C:\Local\resume\python-junior-mid>
```

## Remediation

To relax the security permissions *for the current PowerShell window only* run:

```
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted
```

Now I can run my script:

```
PS > .\build.ps1
```

Without any security errors!

I don't do much work in PowerShell at all so I am fine with having to enable scripts manually for each PowerShell window that I start.

## Moar!

* PowerShell [Set-ExecutionPolicy](https://docs.microsoft.com/en-gb/powershell/module/microsoft.powershell.security/set-executionpolicy?view=powershell-7)

&mdash; Oliver Frolovs, 2020