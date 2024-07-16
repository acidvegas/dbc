# Dropbear Connect
> A secure & efficient way to manage your remote connections with Dropbear!

DBC is a simple script to manage your SSH connections with [Dropbear](https://github.com/mkj/dropbear)
, which is an alternative to OpenSSH for remote connections.

## Introduction
Dropbear does not have built-in support for an `.ssh/config` file, and even with OpenSSH, storing all your remote infrastructure in plain-text might not be a good idea.

Dropbear does not have support for encrypted SSH private keys, and even with OpenSSH, storing your private keys *(even if encrypted)* in the default `.ssh` directory might not be a good idea.

DBC is really simple & meant to run side-by-side with [pass](https://github.com/acidvegas/pass) securely store your `.ssh/config` & your SSH private keys.

You can securely manage & organize your SSH connections now. Your SSH private key is temporarily decrypted in RAM & used to connect. Once connected, the key is wiped.

## Usage
1. Store your Dropbear configurations in your password store under the name `dropbear` in the following format:

```
NAME USER HOST PORT JUMP
```

JUMP is optional and can be used to specify a host that should use your jump host.

If JUMP is set to x, the script will use the jump host to connect to the end host.

There should only be one jump host in the config file and it should be named `jump`.

###### Example
```
jump    acidvegas 68.192.37.5   5902
hatebox acidvegas 100.151.45.10 2023 x
aws     admin     45.16.150.203 22
```

2. Store your Dropbear private key in your password store under the name `dropbear_key`.

3. Run the script with the name of the host you want to connect to:

```shell
./dbc hatebox
```

## Useful Commands

- Git usage: `git config core.sshCommand "dbclient -i ~/.ssh/key"`
- Generate private key: `dropbearkey -t ed25519 -f ~/.dropbear/key | grep "ssh-ed25519"`
- Get public key: `dropbearkey -y -f ~/.dropbear/key | head -n 2 | tail -n 1`

___

###### Mirrors for this repository: [acid.vegas](https://git.acid.vegas/dbc) • [SuperNETs](https://git.supernets.org/acidvegas/dbc) • [GitHub](https://github.com/acidvegas/dbc) • [GitLab](https://gitlab.com/acidvegas/dbc) • [Codeberg](https://codeberg.org/acidvegas/dbc)
