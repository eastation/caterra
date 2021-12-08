# Getting Started

## Installation

Prebuilt binary (all platforms)

1. Download the ```Caterra``` archive for your platform from this Releases page.
2. Extract the downloaded archive.
3. Move the extracted ```caterra``` binary to somewhere in your PATH:
    <details>
    <summary>macOS</summary>
    
    
        shell
        mv caterra /usr/local/bin

    On some versions of macOS, you might see an error message that "caterra cannot be opened because the developer cannot be verified." You can safely run caterra by taking the following steps:

    1. Select "Cancel" to dismiss the error message.
    2. In macOS, access System Preferences > Security and Privacy.
    3. Select the General tab and click the "Allow Anyway" button.
    4. Run caterra again:

            caterra

    5. macOS will ask you to confirm that you want to open it. Select "Open."
    
    You can now execute caterra commands.

    </details>
    <details>
    <summary>Linux</summary>
  
        shell
        sudo mv caterra /usr/local/bin

    </details>
    <details>
    <summary>Windows (cmd)</summary>
  
        md C:\caterra\bin
        move caterra.exe C:\caterra\bin
        setx PATH "%PATH%;C:\caterra\bin"

    </details>
    <details>
    <summary>Windows (PowerShell)</summary>
  
        powershell
        md C:\caterra\bin
        move caterra.exe C:\caterra\bin
        $env:Path += ";C:\caterra\bin"
        # You can add '$env:Path += ";C:\caterra\bin"' to your profile.ps1 file to
        # persist that change across shell sessions.

    </details>

4. _Windows users only:_ Close cmd and re-open it so the changes take effect.
5. You can now run `caterra`.

## Run caterra locally on Terraform IaC

1.  Run caterra 

        caterra scan infra_tf


## Add Rule to exclusion  

1. Run caterra 

        caterra scan infra_tf


## Add some Resource to exclusion  

1. Run caterra 

        caterra scan infra_tf



!> test