# Power ASCII
 
**This script will simply print out a random Ascii Art to your terminal screen whenever you launch the terminal.**

> **Note:** This script only works on PowerShell v5.0 or higher

Run through the following steps to use this script.

## Get your PowerShell profile

a. Your profile already exists a notepad will open with it. 
```PowerShell
# The following command will open your profile if it exists
# $PROFILE is a variable that contains a path where your profile should be located
> notepad $PROFILE
```
b. You does not currently have a profile
```PowerShell
# The following command will output a directory where your profile should be located
> echo $PROFILE

# With the following command you can create your profile file with no content
> New-Item -ItemType File -Force -Path DIRECTORY_FROM_PREVIOUS_COMMAND
```

## Setup PowerShell Profile

Put the following code somewhere to your profile
```PowerShell
function Get-Random-Art()
{
    $number = Get-Random 60
    $response = Invoke-WebRequest -Uri "https://raw.githubusercontent.com/zozobalogh0817/ascii-splash-screen/master/art/$number.txt"
    $art = $response.Content
    return $art
}

Write-Host (Get-Random-Art)
```
Save your profile then restart your PowerShell, or type the following command

```
# This command will reload your profile
. $PROFILE
```

#### You ready to rock.


## LITTLE EXTRA

> If you want you could use the following method to print out the Ascii Art

Just simply put the following code somewhere to your profile
```powershell
function FancyWritter([string]$Text){
    $Text.ToCharArray() | ForEach-Object{
        switch -Regex ($_){
            "`r"{break}
            "`n"{Write-Host " "; break}
            "[^ ]"{
                $writeHostOptions = @{
                    # ForegroundColor = ([system.enum]::GetValues([system.consolecolor])) | get-random
                    NoNewLine = $true
                }
                Write-Host $_ @writeHostOptions
                break
            }
            " "{Write-Host " " -NoNewline}
        } 
    }
}

function Get-Random-Art()
{
    $number = Get-Random 60
    $response = Invoke-WebRequest -Uri "https://raw.githubusercontent.com/zozobalogh0817/ascii-splash-screen/master/art/$number.txt"
    $art = $response.Content
    return $art
}
FancyWritter (Get-Random-Art)
```

Thanks to [DanCRichards](https://github.com/DanCRichards)

Based on [DanCRichards/ASCII-Art-Splash-Screen](https://github.com/DanCRichards/ASCII-Art-Splash-Screen)

> Do not use this script for too serious things
