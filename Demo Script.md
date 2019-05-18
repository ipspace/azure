# Azure Workshop Demo Script

This demo script lists the commands used in Azure Networking Workshop demos.

## Create a resource group and start a VM

* Login into shell.azure.vm

```
simple/list-locations
setup/create-rg Simple
simple/create-vm-a
ssh azure@...
```

## Create another VM in the same subnet

```
simple/create-vm-b
```

### Cleanup

```
setup/delete-rg
```

## Create application environments with two subnets

```
setup/create-rg Net
network/create-vnet
network/create-vm
ssh azure@...
setup/delete-rg
```

### Cleanup

```
setup/delete-rg
```

## Create Network Security Groups

```
setup/create-rg NSG
network/create-vnet
nsg/create-vm
nsg/create-web-nsg
nsg/create-db-nsg
az network nsg list -o table
az network nsg rule list -g NSG --nsg-name Web-NSG -o table
az network nsg rule list -g NSG --nsg-name Web-NSG -o table --include-default
ssh azure@...
nsg/apply-nsg
```

### Test NSG

```
scp ../.ssh/id_rsa azure@...:.ssh/
ssh azure@...
ssh azure@DB
```

Remove SSH entry from DB-NSG using portal. Recheck with SSH

```
nsg/fix-db-nsg
ssh azure@DB
telnet DB 3306
telnet DB 3300
```

### Cleanup

```
setup/delete-rg
```

## Application Security Groups Demo

```
setup/create-rg ASG
network/create-vnet
asg/create-asg
asg/create-vm
asg/create-db-nsg
asg/create-web-nsg
ssh azure@...
nsg/apply-nsg
az network nic list-effective-nsg -g ASG -n DBVMNic
```

## Route table demo

```
setup/create-rg rt
network/create-vnet
network/create-vm
ssh azure@...
scp /home/ivan/.ssh/id_rsa azure@40.121.111.118:.ssh/
```

Test outbound Internet connectivity from DB

```
ssh azure@...
A> ssh azure@172.16.2.4
B> curl www.example.com
```

Display routing tables in DBNet

```
az network nic show-effective-route-table -g Net -n DBVMNic -o table
```

Create a custom route table

```
rt/create-rt
rt/apply-rt
```

Display routing tables in DBNet

```
az network nic show-effective-route-table -g Net -n DBVMNic -o table
```
