# Secure Network using encryption with Azure CLI

### Create a resource group:

1. Start by creating a resource group to hold your network resources.

```js
az group create --name myResourceGroup --location eastus
```

2. Create a virtual network: Use the following command to create a virtual network with a subnet:

```js
az network vnet create \
  --resource-group myResourceGroup \
  --name myVirtualNetwork \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```

3. Create a network security group: Use the following command to create a network security group:

```js
az network nsg create \
  --resource-group myResourceGroup \
  --name myNetworkSecurityGroup
```

4. Create a network security rule: Use the following command to create a network security rule:

```js
az network nsg rule create \
  --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup \
  --name myNetworkSecurityRule \
  --protocol tcp \
  --direction inbound \
  --source-address-prefix 0.0.0.0/0 \
  --source-port-range '*' \
  --destination-address-prefix '*' \
  --destination-port-range 3389 \
  --access allow \
  --priority 1000
```

5. Create a public IP address: Use the following command to create a public IP address:

```js
az network public-ip create \
  --resource-group myResourceGroup \
  --name myPublicIPAddress \
  --sku Standard \
  --allocation-method Dynamic
```

6. Create a virtual network gateway: Use the following command to create a virtual network gateway:

```js
az network vnet-gateway create \
  --name myVirtualNetworkGateway \
  --public-ip-address myPublicIPAddress \
  --resource-group myResourceGroup \
  --vnet myVirtualNetwork \
  --gateway-type Vpn \
  --vpn-type RouteBased \
  --sku VpnGw1 \
  --no-wait
```

7. Create a virtual network gateway connection: Use the following comand to create a virtual network gateway connection: 

```js
az network vpn-connection create \
  --name myVpnConnection \
  --resource-group myResourceGroup \
  --vnet-gateway1 myVirtualNetworkGateway \
  --shared-key mySharedKey \
  --enable-bgp false \
  --location eastus
```

8. Monitor and manage: Use the Azure portal or the Azure CLI to monitor and manage your Azure resources.

>By following these steps, you can create a secure network that is encrypted on Azure using the Azure CLI. Of course, the specific details of your network will depend on your specific requirements, such as the size of your network, the types of applications and data you need to secure, and the compliance requirements you need to meet.