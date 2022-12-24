# livebox-banip
Bash script to ban IP on Livebox internet box (from Orange french ISP)

:warning: This script has been tested to configure the firewall but **custom rules added to firewall does not work** on livebox

## Supported livebox

Same support than [sysbus](https://github.com/rene-d/sysbus). Tested only with livebox 4.

## Installation
1. Install `jq` command from package
   * Debian / Ubuntu
       ```bash
       sudo apt-get update
       sudo apt-get install jq
       ```
   * RedHat / Centos / Fedora
       ```bash
       sudo yum install jq
       ```
2. Install `sysbus` command from [GitHub project](https://github.com/rene-d/sysbus) (see [sysbus README](https://github.com/rene-d/sysbus/blob/master/README.md))
    ```bash
    sudo pip3 install sysbus
    ```
3. Copy `livebox-banip` in a folder of your `$PATH` variable (ex: `/usr/local/bin`)
4. Configure `sysbus` (see [sysbus README](https://github.com/rene-d/sysbus/blob/master/README.md))
    ```bash
    sysbus -config -password SECRET [ -url http://192.168.1.1/ ] [ -lversion lb4 ]
    ```
5. Test installation:
    ```
    livebox-banip -l && echo OK || echo ERROR
    ```

## Usage

```
Usage: livebox-banip [OPTIONS] --list|-l
  or:  livebox-banip [OPTIONS] --add <IP>
  or:  livebox-banip [OPTIONS] --remove <IP>
  or:  livebox-banip [OPTIONS] --help|-h
List, add or remove IP address to livebox ban list

      --add=<IP>    add <IP> to ban list
      --destination ban or list ban flow from local network to <IP>
  -h, --help        display this help and exit
  -l, --list        list all ban ip
      --remove=<IP> remove <IP> from ban list
      --source      ban or list ban flow from <IP> to local network (default)
  -v, --verbose     Verbose mode.  Multiple -v options increase the verbosity.
                    The maximum is 2.
                    level 1: output API result json
                    level 2: output jq/sysbus params
```

`<IP>` could be:
* A fixed IPv4 (ex: 192.168.0.32)
* An IPv4 subnet mask in format: IP/CIDR (ex: 192.168.0.0/24)

For now only IP v4 is supported.