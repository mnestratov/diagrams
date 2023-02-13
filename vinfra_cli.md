# Administrator Command-Line Reference

This guide describes the syntax and parameters of the `vinfra` command-line tool that can be used to manage Virtuozzo Hybrid Infrastructure from console and automate such management tasks.

To get a list of all supported commands and their descriptions, you can also run `vinfra help`. For help on a specific command, either run `vinfra help <command>` or `vinfra <command> --help`.

## Table of content

- [vinfra usage](#vinfra-usage)
- [vinfra output formatters](#user-content-vinfra-output-formatters)
- [cluster alert delete](#cluster-alert-delete)
- [service compute server create](#service-compute-server-create)

## <a name="vinfra-usage"></a>vinfra usage

```
usage: vinfra [--version] [-v | -q] [-h] [--vinfra-portal <portal>]
              [--vinfra-username <username>] [--vinfra-password <password>]
              [--vinfra-domain <domain>] [--vinfra-project <project>]
			  <subcommand> ...
```

### Optional arguments:

<dl>
  <dt><strong>--version</strong></dt>
  <dd>Show program's version number and exit.</dd>
  <dt>-v, --verbose</dt>
  <dd>Increase verbosity of the output. Can be repeated.</dd>
</dl>

**--version**  
: Show program's version number and exit.

**-v, --verbose**  
: Increase verbosity of the output. Can be repeated.

**-q, --quiet**  
: Suppress the output except warnings and errors.

**-h, --help**  
: Show the help message and exit.

**--vinfra-portal <portal>**  
: The backend hostname or IP address (default: backend-api.svc.vstoragedomain) [Env: `VINFRA_PORTAL`]

**--vinfra-username <username>**  
: The user name to authenticate with (default: "admin") [Env: `VINFRA_USERNAME`]

**--vinfra-password <password>**  
: The user password to authenticate with [Env: `VINFRA_PASSWORD`]

**--vinfra-domain <domain>**  
: The domain name to authenticate with [Env: `VINFRA_DOMAIN`]

**--vinfra-project <project>**  
: The project ID to authenticate with [Env: `VINFRA_PROJECT`]


## vinfra output formatters

### Output formatter options:

**-f {json,table,value,yaml}, --format {json,table,value,yaml}**  
The output format, defaults to `table`.

**-c COLUMN, --column COLUMN**  
Specify the column(s) to include. Can be repeated.

### Table formatter:

**--max-value-length MAX_VALUE_LENGTH**  
Maximum value length. Longer values will be truncated. Set this option to -1 to turn off value truncation. The default is 80.


## <a name="cluster-alert-delete"></a>cluster alert delete

Remove an entry from the alert log.

```
usage: vinfra cluster alert delete [-h] <alert>
```

### Positional arguments:

**<alert>**  
Alert ID

### Optional arguments:

**-h, --help**  
show this help message and exit.


## service compute server create

Create a new compute server.

```
usage: vinfra service compute server create [-h] [--wait] [--timeout <seconds>]
                                            [--description <description>]
                                            [--metadata <metadata>]
                                            [--user-data <user-data>]
                                            [--key-name <key-name>]
                                            [--config-drive] [--count <count>]
                                            --network id|<id=id[,mac=mac,fixed-ip=ip-addr[@subnet]>,
											spoofing-protection-enable,spoofing-protection-disable,
											security-group=secgroup,no-security-group]>
                                            --volume <source=source[,id=id,key1=value1,key2=value2...]>
                                            --flavor <flavor>
                                            [--ha-enabled <ha_enabled>]
                                            [--placements <placements>]
                                            [--allow-live-resize] [--uefi]
                                            <server-name>
```

### Positional arguments:

**<server-name>**  
A new name for the compute server

### Optional arguments:

-h, --help
: Show this help message and exit

--description <description>
: Server description

--metadata <metadata>
: Server metadata in the format key=value. Specify this option multiple times to create multiple metadata records.

--user-data <user-data>
: User data file

--key-name <key-name>
: Key pair to inject

--config-drive
: Use an ephemeral drive

--count <count>
: If count is specified and greater than 1, the 'name' argument is treated as a naming pattern.

--network id|<id=id[,mac=mac,fixed-ip=ip-addr[@subnet]>,spoofing-protection-enable,spoofing-protection-disable,security-group=secgroup,no-security-group]>
: Create a compute server with a specified network.  
Specify this option multiple times to create multiple networks.  
- **id**: attach network interface to a specified network (ID or name);
- **mac**: MAC address for network interface (optional);
- **fixed-ip**: desired IP and/or subnet for network interface. Set IP address to None to allocate IP from desired subnet. (optional);
- **spoofing-protection-enable**: enable spoofing protection (optional);
- **spoofing-protection-disable**: disable spoofing protection (optional);
- **security-group**: security group ID or name. This option can be used multiple times (optional);
- **no-security-group**: do not use security group (optional).

--volume <source=source[,id=id,key1=value1,key2=value2...]>
: Create a compute server with a specified volume.  
Specify this option multiple times to create multiple volumes.
- source
  : source type ('volume', 'image', 'snapshot', or 'blank');
- id
  : resource ID or name for the specified source type (required for source types 'volume', 'image', and 'snapshot');
- size
  : block device size, in gigabytes (required for source types 'image' and 'blank');
- boot-index
  : block device boot index (required for multiple volumes with source type 'volume');
- bus
  : block device controller type ('ide', 'usb', 'virtio', 'scsi, or 'sata') (optional);
- type
  : block device type (disk or cdrom) (optional);
- rm
  : remove block device on compute server termination ('yes' or 'no') (optional);
- storage-policy
  : block device storage policy (optional).

--flavor <flavor>
: Flavor ID or name

--ha-enabled <ha_enabled>
: Enable HA for the compute server

--placements <placements>
: Names or IDs of placements to add the virtual machine to.

--allow-live-resize
: Allow online resize for the compute server

--uefi
: Allow UEFI boot for the compute server. This option can be used for servers created from ISO images.

### Command run options:

Additional command options

--wait
: Wait for the operation to complete (synchronous mode).

--timeout <seconds>
: A timeout for the operation to complete if --wait is specified, in seconds (default: 600)