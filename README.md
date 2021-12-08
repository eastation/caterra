# Getting Started

## Installation

Prebuilt binary (all platforms)

1. Download the ```Caterra``` archive for your platform from this Releases page.
2. Extract the downloaded archive.
3. Move the extracted ```caterra``` binary to somewhere in your PATH:

    === "macOS"

        shell
        mv caterra /usr/local/bin

    === "Linux"

        shell
        sudo mv caterra /usr/local/bin

    === "Windows (cmd)"

        md C:\caterra\bin
        move caterra.exe C:\caterra\bin
        setx PATH "%PATH%;C:\caterra\bin"
    
    === "Windows (PowerShell)"

        powershell
        md C:\caterra\bin
        move caterra.exe C:\caterra\bin
        $env:Path += ";C:\caterra\bin"
        # You can add '$env:Path += ";C:\caterra\bin"' to your profile.ps1 file to
        # persist that change across shell sessions.

4. _Windows users only:_ Close cmd and re-open it so the changes take effect.
5. You can now run `caterra`.

<details>
  <summary>macOS warning</summary>
  
  On some versions of macOS, you might see an error message that "caterra cannot be opened because the developer cannot be verified." You can safely run caterra by taking the following steps:

    1. Select "Cancel" to dismiss the error message.
    2. In macOS, access System Preferences > Security and Privacy.
    3. Select the General tab and click the "Allow Anyway" button.
    4. Run caterra again:

            caterra

    5. macOS will ask you to confirm that you want to open it. Select "Open."
    
    You can now execute caterra commands.

</details>

## Run caterra locally on Terraform IaC

1.  Run caterra 

        regula scan infra_tf


## Add Rule to exclusion  

1. Run caterra 

        regula scan infra_tf


## Add some Resource to exclusion  

1. Run caterra 

        regula scan infra_tf



!> test