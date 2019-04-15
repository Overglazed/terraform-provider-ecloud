# terraform-provider-ecloud

## Provider

**Parameters**

- `api_key`: UKFast API key - read/write permissions for `ecloud` service required. If omitted, will use `UKF_API_KEY` environment variable value

## Resources

### ecloud_virtualmachine

**Schema**

- `cpu`: (Required) CPU count
- `ram`: (Required) Amount of RAM in Gibibytes
- `os_disk`: (Required) Size of primary disk in Gibibytes
- `template`: (Required) Template/OS name
- `name`: Name of VM
- `computername`: Computer name for VM
- `environment`: Environment for VM
- `solution_id`: ID of solution which the VM is a member of
- `datastore_id`: ID of datastore on which to launch VM
- `site_id`: ID of site on which to launch VM
- `network_id`: ID of network on which to launch VM
- `external_ip_required`: Specifies that an external IP address should be allocated
- `power_status`: Power status of VM. Valid values: `Online` (default), `Offline`
- `ssh_keys`: An array of SSH public keys to apply to VM

### ecloud_virtualmachine_tag

**Schema**

- `virtualmachine_id`: (Required) ID of target virtual machine
- `key`: (Required) Key for tag
- `value`: Value for tag

### ecloud_solution_tag

**Schema**

- `solution_id`: (Required) ID of target solution
- `key`: (Required) Key for tag
- `value`: Value for tag

## Data sources

### ecloud_datastore

**Schema**

- `name`: (Required) Name of datastore
- `solution_id`: (Required) ID of solution which the datastore is a member of
- `site_id`: ID of site which the datastore is a member of
- `status`: Status of datastore
- `capacity`: Capacity of datastore

### ecloud_site

**Schema**

- `pod_id`: (Required) ID of Pod which site is a member of
- `solution_id`: (Required) ID of solution which the site is a member of
- `state`: State of the site

### ecloud_solution

**Schema**

- `name`: (Required) Name of solution
- `environment`: Environment for solution

### ecloud_network

**Schema**

- `name`: (Required) Name of network
- `solution_id`: (Required) ID of solution which the network is a member of

## Example

```terraform
provider "ecloud" {
  api_key = "abc"
}

resource "ecloud_virtualmachine" "vm-1" {
    cpu = 2
    ram = 2
    os_disk = 20
    template = "CentOS 7 64-bit"
    name = "vm-1"
    environment = "Hybrid"
    solution_id = 123
}
```
