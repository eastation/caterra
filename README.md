# Download

| File     | Описание |
| ---      | ---       |
| [caterra_1.0.0_windows_x86_64.zip](https://cloudadvisor.ru/r/) | Windows executable         |
| [caterra_1.0.0_macos_arm.zip](https://cloudadvisor.ru/r/) | Mac OS executable         |
| [caterra_1.0.0_linux_x86_64.zip](https://cloudadvisor.ru/r/) | CentOS Linux         |
| [caterra_1.0.0_freebsd_x86_64.zip](https://cloudadvisor.ru/r/) | FreeBSD  |

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


## Ignoring Warnings

You may wish to ignore some warnings. If you'd like to do so, you can
simply add a comment containing `tfsec:ignore:<rule>` to the offending
line in your templates. If the problem refers to a block of code, such
as a multiline string, you can add the comment on the line above the
block, by itself.

For example, to ignore an open security group rule:

```hcl
resource "aws_security_group_rule" "my-rule" {
    type = "ingress"
    cidr_blocks = ["0.0.0.0/0"] #tfsec:ignore:aws-vpc-no-public-ingress-sgr
}
```

...or...

```hcl
resource "aws_security_group_rule" "my-rule" {
    type = "ingress"
    #tfsec:ignore:aws-vpc-no-public-ingress-sgr
    cidr_blocks = ["0.0.0.0/0"]
}
```

If you're not sure which line to add the comment on, just check the
tfsec output for the line number of the discovered problem.

You can ignore multiple rules by concatenating the rules on a single line:

```hcl
#tfsec:ignore:aws-s3-enable-bucket-encryption tfsec:ignore:aws-s3-enable-bucket-logging
resource "aws_s3_bucket" "my-bucket" {
  bucket = "foobar"
  acl    = "private"
}
```

### Expiration Date
You can set expiration date for `ignore` with `yyyy-mm-dd` format. This is a useful feature when you want to ensure ignored issue won't be forgotten and should be revisited in the future.
```
#tfsec:ignore:aws-s3-enable-bucket-encryption:exp:2022-01-02
```
Ignore like this will be active only till `2022-01-02`, after this date it will be deactivated.

### Workspace Ignores
Ignoring checks can be scoped to a workspace level. If you add the `ws:` declaration to your ignore it will only be honoured for that workspace.

```hcl
# tfsec:ignore:AWS006:exp:2221-01-02 #tfsec:ignore:AWS018:ws:development
resource "aws_security_group_rule" "my-rule" {
    type        = "ingress"
	
    cidr_blocks = ["0.0.0.0/0"]
}
```

In the example above, when tfsec is run with the `--workspace` flag set to development, this ignore will be honoured, but otherwise will be disregarded.

```bash
tfsec --workspace development .
```

### Ignoring specific values

We have recently added support for ignoring based on the value that has been provided. This is particularly relevant when using `for_each` and you want to allow certain values. 

```hcl
locals {
  rules = {
    http = 80
    https = 443 
  }
}

#tfsec:ignore:aws-vpc-no-public-ingress-sgr[from_port=443]
resource "aws_security_group_rule" "this" {
      for_each = local.rules
      type = "ingress"
      description     = "test"
      from_port       = each.value 
      to_port         = each.value
      protocol        = "tcp"
      cidr_blocks     = ["0.0.0.0/0"]

}
```

In the example above, the `aws-vpc-no-public-ingress-sgr` check will fail for `80` but when it creates the rule for `443` the check will pass.

This feature is experimental - while it works successfully, please raise issues through [GitHub Issues]

[Github Issues]: https://github.com/aquasecurity/tfsec/issues

