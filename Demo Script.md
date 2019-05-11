# Azure Workshop Demo Script

## Create a resource group and a VM

* Login into shell.azure.vm

```
simple/list-locations
setup/create-rg
simple/create-vm-a
ssh azure@...
```

## Create another VM

```
simple/create-vm-b
```

## Cleanup

```
setup/delete-rg
```