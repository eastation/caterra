# Download

| File     | Description |
| ---      | ---       |
| [caterra_1.0.0_windows_x86_64.zip](https://cloudadvisor.ru/r/) | Windows executable         |
| [caterra_1.0.0_macos_arm.zip](https://cloudadvisor.ru/r/) | Mac OS executable         |
| [caterra_1.0.0_linux_x86_64.zip](https://cloudadvisor.ru/r/) | CentOS Linux         |
| [caterra_1.0.0_freebsd_x86_64.zip](https://cloudadvisor.ru/r/) | FreeBSD  |

# Getting Started

## Installation

Prebuilt binary (all platforms)

1. Generate a Caterra access token in the CloudAdvisor console, under Settings > Terraform.
2. Download the ```Caterra``` archive for your platform from this Releases page.
3. Extract the downloaded archive.
4. Move the extracted ```caterra``` binary to somewhere in your PATH:
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
    _Windows users only:_ Close cmd and re-open it so the changes take effect.

    </details>
    <details>
    <summary>Windows (PowerShell)</summary>
  
        powershell
        md C:\caterra\bin
        move caterra.exe C:\caterra\bin
        $env:Path += ";C:\caterra\bin"
        # You can add '$env:Path += ";C:\caterra\bin"' to your profile.ps1 file to
        # persist that change across shell sessions.
    _Windows users only:_ Close cmd and re-open it so the changes take effect.
    </details>

5. You can now run `caterra`.

## Usage

    caterra  scan <TAGET-FOLDER>  [Flags...]

      <TAGET-FOLDER> string
              Set the name of the folder containing terraform iac scripts.

    Flags:
      --token string
              Set the application token to use.

      --format string
              Set the output format: text (default), json.

      --severity
             Set the minimum severity that will result in a non-zero exit code: high, medium, low (default)
 

## Ignoring Warnings

You may wish to ignore some warnings. If you'd like to do so, you can simply add a 
comment containing `ca:ignore:<rules>` to  your templates. 

For example, to ignore a DNS non-compliant bucket name:

```hcl
resource "yandex_storage_bucket" "dns" {
 
  # ca:ignore:TF-YC.OS.0001
  # ca:ignore:TF-YC.OS.0002
 
  bucket = "ca.tf.yc.os.0001-02"
}
```
...or...

You can ignore multiple rules by concatenating the rules on a single line:

```hcl
resource "yandex_storage_bucket" "dns" {
 
  # ca:ignore:TF-YC.OS.0001,TF-YC.OS.0002
 
  bucket = "ca.tf.yc.os.0001-02"
}
```