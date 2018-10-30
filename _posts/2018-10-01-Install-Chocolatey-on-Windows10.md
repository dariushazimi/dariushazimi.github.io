# Install awscli and python3 with chocolatey on Windows 10

Start powershell and run as admin

Run the following on powershell command prompt:

    `Get-ExecutionPolicy`

If it returns Restricted do the following:

    `Set-ExecutionPolicy Bypass -Scope Process`

Now run the following command:

    `Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))`


Restart powershell and run as admin again.

To install awscli:
    `choco install awscli -y`

Install python3 and git

    `choco install python3 -y`
    `choco install git -y`

Install openssh

    `choco install openssh -y -params "/SSHAgentFeature"`

Restart your windows and you should not have python and git and all other installed components.

Open powershell and do:

    `python -v`




