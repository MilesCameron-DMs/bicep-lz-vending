# `main.bicep` Parameters

This module is designed to accelerate deployment of landing zones (aka Subscriptions) within an Azure AD Tenant.

These are the input parameters for the Bicep module: [`main.bicep`](./main.bicep)

This is the orchestration module that is used and called by a consumer of the module to deploy a Landing Zone Subscription and its associated resources, based on the parameter input values that are provided to it at deployment time.

> For more information and examples please see the [wiki](https://github.com/Azure/bicep-lz-vending/wiki)

## Parameters

Parameter name | Required | Description
-------------- | -------- | -----------
subscriptionAliasEnabled | No       | Whether to create a new Subscription using the Subscription Alias resource. If `false`, supply an existing Subscription's ID in the parameter named `existingSubscriptionId` instead to deploy resources to an existing Subscription.  - Type: Boolean 
subscriptionDisplayName | No       | The name of the subscription alias. The string must be comprised of a-z, A-Z, 0-9, - and _. The maximum length is 63 characters.  The string must be comprised of `a-z`, `A-Z`, `0-9`, `-`, `_` and ` ` (space). The maximum length is 63 characters.  > The value for this parameter and the parameter named `subscriptionAliasName` are usually set to the same value for simplicity. But they can be different if required for a reason.  > **Not required when providing an existing Subscription ID via the parameter `existingSubscriptionId`**  - Type: String - Default value: `''` *(empty string)* 
subscriptionAliasName | No       | The name of the Subscription Alias, that will be created by this module.  The string must be comprised of `a-z`, `A-Z`, `0-9`, `-`, `_` and ` ` (space). The maximum length is 63 characters.  > **Not required when providing an existing Subscription ID via the parameter `existingSubscriptionId`**  - Type: String - Default value: `''` *(empty string)* 
subscriptionBillingScope | No       | The Billing Scope for the new Subscription alias, that will be created by this module.  A valid Billing Scope starts with `/providers/Microsoft.Billing/billingAccounts/` and is case sensitive.  > See below [example in parameter file](#parameter-file) for an example  > **Not required when providing an existing Subscription ID via the parameter `existingSubscriptionId`**  - Type: String - Default value: `''` *(empty string)* 
subscriptionWorkload | No       | The workload type can be either `Production` or `DevTest` and is case sensitive.  > **Not required when providing an existing Subscription ID via the parameter `existingSubscriptionId`**  - Type: String 
subscriptionTenantId | No       | The Azure Active Directory Tenant ID (GUID) to which the Subscription should be attached to.  > **Leave blank unless following this scenario only [Programmatically create MCA subscriptions across Azure Active Directory tenants](https://learn.microsoft.com/azure/cost-management-billing/manage/programmatically-create-subscription-microsoft-customer-agreement-across-tenants).**  - Type: String - Default value: `''` *(empty string)* 
subscriptionOwnerId | No       | The Azure Active Directory principals object ID (GUID) to whom should be the Subscription Owner.  > **Leave blank unless following this scenario only [Programmatically create MCA subscriptions across Azure Active Directory tenants](https://learn.microsoft.com/azure/cost-management-billing/manage/programmatically-create-subscription-microsoft-customer-agreement-across-tenants).**  - Type: String - Default value: `''` *(empty string)* 
existingSubscriptionId | No       | An existing subscription ID. Use this when you do not want the module to create a new subscription. But do want to manage the management group membership. A subscription ID should be provided in the example format `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`.  - Type: String - Default value: `''` *(empty string)* 
subscriptionManagementGroupAssociationEnabled | No       | Whether to move the Subscription to the specified Management Group supplied in the parameter `subscriptionManagementGroupId`.  - Type: Boolean 
subscriptionManagementGroupId | No       | The destination Management Group ID for the new Subscription that will be created by this module (or the existing one provided in the parameter `existingSubscriptionId`).  **IMPORTANT:** Do not supply the display name of the Management Group. The Management Group ID forms part of the Azure Resource ID. e.g., `/providers/Microsoft.Management/managementGroups/{managementGroupId}`.  > See below [example in parameter file](#parameter-file) for an example  - Type: String - Default value: `''` *(empty string)* 
subscriptionTags | No       | An object of Tag key & value pairs to be appended to a Subscription.  > **NOTE:** Tags will only be overwritten if existing tag exists with same key as provided in this parameter; values provided here win.  - Type: `{}` Object - Default value: `{}` *(empty object)* 
virtualNetworkEnabled | No       | Whether to create a Virtual Network or not.  If set to `true` ensure you also provide values for the following parameters at a minimum:  - `virtualNetworkResourceGroupName` - `virtualNetworkResourceGroupLockEnabled` - `virtualNetworkLocation` - `virtualNetworkName` - `virtualNetworkAddressSpace`  > Other parameters may need to be set based on other parameters that you enable that are listed above. Check each parameters documentation for further information.  - Type: Boolean 
virtualNetworkResourceGroupName | No       | The name of the Resource Group to create the Virtual Network in that is created by this module.  - Type: String - Default value: `''` *(empty string)* 
virtualNetworkResourceGroupTags | No       | An object of Tag key & value pairs to be appended to the Resource Group that the Virtual Network is created in.  > **NOTE:** Tags will only be overwritten if existing tag exists with same key as provided in this parameter; values provided here win.  - Type: `{}` Object - Default value: `{}` *(empty object)* 
virtualNetworkResourceGroupLockEnabled | No       | Enables the deployment of a `CanNotDelete` resource locks to the Virtual Networks Resource Group that is created by this module.  - Type: Boolean 
virtualNetworkLocation | No       | The location of the virtual network. Use region shortnames e.g. `uksouth`, `eastus`, etc. Defaults to the region where the ARM/Bicep deployment is targeted to unless overridden.  - Type: String 
virtualNetworkName | No       | The name of the virtual network. The string must consist of a-z, A-Z, 0-9, -, _, and . (period) and be between 2 and 64 characters in length.  - Type: String - Default value: `''` *(empty string)* 
virtualNetworkTags | No       | An object of tag key/value pairs to be set on the Virtual Network that is created.  > **NOTE:** Tags will be overwritten on resource if any exist already.  - Type: `{}` Object - Default value: `{}` *(empty object)* 
virtualNetworkAddressSpace | No       | The address space of the Virtual Network that will be created by this module, supplied as multiple CIDR blocks in an array, e.g. `["10.0.0.0/16","172.16.0.0/12"]`  - Type: `[]` Array - Default value: `[]` *(empty array)* 
virtualNetworkDnsServers | No       | The custom DNS servers to use on the Virtual Network, e.g. `["10.4.1.4", "10.2.1.5"]`. If left empty (default) then Azure DNS will be used for the Virtual Network.  - Type: `[]` Array - Default value: `[]` *(empty array)* 
virtualNetworkDdosPlanId | No       | The resource ID of an existing DDoS Network Protection Plan that you wish to link to this Virtual Network.  **Example Expected Values:** - `''` (empty string) - DDoS Netowrk Protection Plan Resource ID: `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/xxxxxxxxxx/providers/Microsoft.Network/ddosProtectionPlans/xxxxxxxxxx`  - Type: String - Default value: `''` *(empty string)* 
virtualNetworkPeeringEnabled | No       | Whether to enable peering/connection with the supplied hub Virtual Network or Virtual WAN Virtual Hub.  - Type: Boolean 
hubNetworkResourceId | No       | The resource ID of the Virtual Network or Virtual WAN Hub in the hub to which the created Virtual Network, by this module, will be peered/connected to via Virtual Network Peering or a Virtual WAN Virtual Hub Connection.  **Example Expected Values:** - `''` (empty string) - Hub Virtual Network Resource ID: `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/xxxxxxxxxx/providers/Microsoft.Network/virtualNetworks/xxxxxxxxxx` - Virtual WAN Virtual Hub Resource ID: `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/xxxxxxxxxx/providers/Microsoft.Network/virtualHubs/xxxxxxxxxx`  - Type: String - Default value: `''` *(empty string)* 
virtualNetworkUseRemoteGateways | No       | Enables the use of remote gateways in the specified hub virtual network.  > **IMPORTANT:** If no gateways exist in the hub virtual network, set this to `false`, otherwise peering will fail to create.  - Type: Boolean 
virtualNetworkVwanEnableInternetSecurity | No       | Enables the ability for the Virtual WAN Hub Connection to learn the default route 0.0.0.0/0 from the Hub.  - Type: Boolean 
virtualNetworkVwanAssociatedRouteTableResourceId | No       | The resource ID of the virtual hub route table to associate to the virtual hub connection (this virtual network). If left blank/empty the `defaultRouteTable` will be associated.  - Type: String - Default value: `''` *(empty string)* = Which means if the parameter `virtualNetworkPeeringEnabled` is `true` and also the parameter `hubNetworkResourceId` is not empty then the `defaultRouteTable` will be associated of the provided Virtual Hub in the parameter `hubNetworkResourceId`.     - e.g. `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/xxxxxxxxxx/providers/Microsoft.Network/virtualHubs/xxxxxxxxx/hubRouteTables/defaultRouteTable` 
virtualNetworkVwanPropagatedRouteTablesResourceIds | No       | An array of of objects of virtual hub route table resource IDs to propagate routes to. If left blank/empty the `defaultRouteTable` will be propagated to only.  Each object must contain the following `key`: - `id` = The Resource ID of the Virtual WAN Virtual Hub Route Table IDs you wish to propagate too  > See below [example in parameter file](#parameter-file)  > **IMPORTANT:** If you provide any Route Tables in this array of objects you must ensure you include also the `defaultRouteTable` Resource ID as an object in the array as it is not added by default when a value is provided for this parameter.  - Type: `[]` Array - Default value: `[]` *(empty array)* 
virtualNetworkVwanPropagatedLabels | No       | An array of virtual hub route table labels to propagate routes to. If left blank/empty the default label will be propagated to only.  - Type: `[]` Array - Default value: `[]` *(empty array)* 
vHubRoutingIntentEnabled | No       | Indicates whether routing intent is enabled on the Virtual Hub within the Virtual WAN.  - Type: Boolean
roleAssignmentEnabled | No       | Whether to create role assignments or not. If true, supply the array of role assignment objects in the parameter called `roleAssignments`.  - Type: Boolean 
roleAssignments | No       | Supply an array of objects containing the details of the role assignments to create.  Each object must contain the following `keys`: - `principalId` = The Object ID of the User, Group, SPN, Managed Identity to assign the RBAC role too. - `definition` = The Name of built-In RBAC Roles or a Resource ID of a Built-in or custom RBAC Role Definition. - `relativeScope` = 2 options can be provided for input value:     1. `''` *(empty string)* = Make RBAC Role Assignment to Subscription scope     2. `'/resourceGroups/<RESOURCE GROUP NAME>'` = Make RBAC Role Assignment to specified Resource Group  > See below [example in parameter file](#parameter-file) of various combinations  - Type: `[]` Array - Default value: `[]` *(empty array)* 
disableTelemetry | No       | Disable telemetry collection by this module.  For more information on the telemetry collected by this module, that is controlled by this parameter, see this page in the wiki: [Telemetry Tracking Using Customer Usage Attribution (PID)](https://github.com/Azure/bicep-lz-vending/wiki/Telemetry) 

### subscriptionAliasEnabled

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Whether to create a new Subscription using the Subscription Alias resource. If `false`, supply an existing Subscription's ID in the parameter named `existingSubscriptionId` instead to deploy resources to an existing Subscription.

- Type: Boolean


**Default value**

```text
True
```

### subscriptionDisplayName

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

The name of the subscription alias. The string must be comprised of a-z, A-Z, 0-9, - and _. The maximum length is 63 characters.

The string must be comprised of `a-z`, `A-Z`, `0-9`, `-`, `_` and ` ` (space). The maximum length is 63 characters.

> The value for this parameter and the parameter named `subscriptionAliasName` are usually set to the same value for simplicity. But they can be different if required for a reason.

> **Not required when providing an existing Subscription ID via the parameter `existingSubscriptionId`**

- Type: String
- Default value: `''` *(empty string)*


### subscriptionAliasName

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

The name of the Subscription Alias, that will be created by this module.

The string must be comprised of `a-z`, `A-Z`, `0-9`, `-`, `_` and ` ` (space). The maximum length is 63 characters.

> **Not required when providing an existing Subscription ID via the parameter `existingSubscriptionId`**

- Type: String
- Default value: `''` *(empty string)*


### subscriptionBillingScope

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

The Billing Scope for the new Subscription alias, that will be created by this module.

A valid Billing Scope starts with `/providers/Microsoft.Billing/billingAccounts/` and is case sensitive.

> See below [example in parameter file](#parameter-file) for an example

> **Not required when providing an existing Subscription ID via the parameter `existingSubscriptionId`**

- Type: String
- Default value: `''` *(empty string)*


### subscriptionWorkload

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

The workload type can be either `Production` or `DevTest` and is case sensitive.

> **Not required when providing an existing Subscription ID via the parameter `existingSubscriptionId`**

- Type: String


**Default value**

```text
Production
```

**Allowed values**

```text
DevTest
Production
```

### subscriptionTenantId

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

The Azure Active Directory Tenant ID (GUID) to which the Subscription should be attached to.

> **Leave blank unless following this scenario only [Programmatically create MCA subscriptions across Azure Active Directory tenants](https://learn.microsoft.com/azure/cost-management-billing/manage/programmatically-create-subscription-microsoft-customer-agreement-across-tenants).**

- Type: String
- Default value: `''` *(empty string)*


### subscriptionOwnerId

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

The Azure Active Directory principals object ID (GUID) to whom should be the Subscription Owner.

> **Leave blank unless following this scenario only [Programmatically create MCA subscriptions across Azure Active Directory tenants](https://learn.microsoft.com/azure/cost-management-billing/manage/programmatically-create-subscription-microsoft-customer-agreement-across-tenants).**

- Type: String
- Default value: `''` *(empty string)*


### existingSubscriptionId

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

An existing subscription ID. Use this when you do not want the module to create a new subscription. But do want to manage the management group membership. A subscription ID should be provided in the example format `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`.

- Type: String
- Default value: `''` *(empty string)*


### subscriptionManagementGroupAssociationEnabled

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Whether to move the Subscription to the specified Management Group supplied in the parameter `subscriptionManagementGroupId`.

- Type: Boolean


**Default value**

```text
True
```

### subscriptionManagementGroupId

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

The destination Management Group ID for the new Subscription that will be created by this module (or the existing one provided in the parameter `existingSubscriptionId`).

**IMPORTANT:** Do not supply the display name of the Management Group. The Management Group ID forms part of the Azure Resource ID. e.g., `/providers/Microsoft.Management/managementGroups/{managementGroupId}`.

> See below [example in parameter file](#parameter-file) for an example

- Type: String
- Default value: `''` *(empty string)*


### subscriptionTags

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

An object of Tag key & value pairs to be appended to a Subscription.

> **NOTE:** Tags will only be overwritten if existing tag exists with same key as provided in this parameter; values provided here win.

- Type: `{}` Object
- Default value: `{}` *(empty object)*


### virtualNetworkEnabled

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Whether to create a Virtual Network or not.

If set to `true` ensure you also provide values for the following parameters at a minimum:

- `virtualNetworkResourceGroupName`
- `virtualNetworkResourceGroupLockEnabled`
- `virtualNetworkLocation`
- `virtualNetworkName`
- `virtualNetworkAddressSpace`

> Other parameters may need to be set based on other parameters that you enable that are listed above. Check each parameters documentation for further information.

- Type: Boolean


**Default value**

```text
False
```

### virtualNetworkResourceGroupName

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

The name of the Resource Group to create the Virtual Network in that is created by this module.

- Type: String
- Default value: `''` *(empty string)*


### virtualNetworkResourceGroupTags

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

An object of Tag key & value pairs to be appended to the Resource Group that the Virtual Network is created in.

> **NOTE:** Tags will only be overwritten if existing tag exists with same key as provided in this parameter; values provided here win.

- Type: `{}` Object
- Default value: `{}` *(empty object)*


### virtualNetworkResourceGroupLockEnabled

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Enables the deployment of a `CanNotDelete` resource locks to the Virtual Networks Resource Group that is created by this module.

- Type: Boolean


**Default value**

```text
True
```

### virtualNetworkLocation

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

The location of the virtual network. Use region shortnames e.g. `uksouth`, `eastus`, etc. Defaults to the region where the ARM/Bicep deployment is targeted to unless overridden.

- Type: String


**Default value**

```text
[deployment().location]
```

### virtualNetworkName

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

The name of the virtual network. The string must consist of a-z, A-Z, 0-9, -, _, and . (period) and be between 2 and 64 characters in length.

- Type: String
- Default value: `''` *(empty string)*


### virtualNetworkTags

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

An object of tag key/value pairs to be set on the Virtual Network that is created.

> **NOTE:** Tags will be overwritten on resource if any exist already.

- Type: `{}` Object
- Default value: `{}` *(empty object)*


### virtualNetworkAddressSpace

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

The address space of the Virtual Network that will be created by this module, supplied as multiple CIDR blocks in an array, e.g. `["10.0.0.0/16","172.16.0.0/12"]`

- Type: `[]` Array
- Default value: `[]` *(empty array)*


### virtualNetworkDnsServers

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

The custom DNS servers to use on the Virtual Network, e.g. `["10.4.1.4", "10.2.1.5"]`. If left empty (default) then Azure DNS will be used for the Virtual Network.

- Type: `[]` Array
- Default value: `[]` *(empty array)*


### virtualNetworkDdosPlanId

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

The resource ID of an existing DDoS Network Protection Plan that you wish to link to this Virtual Network.

**Example Expected Values:**
- `''` (empty string)
- DDoS Netowrk Protection Plan Resource ID: `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/xxxxxxxxxx/providers/Microsoft.Network/ddosProtectionPlans/xxxxxxxxxx`

- Type: String
- Default value: `''` *(empty string)*


### virtualNetworkPeeringEnabled

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Whether to enable peering/connection with the supplied hub Virtual Network or Virtual WAN Virtual Hub.

- Type: Boolean


**Default value**

```text
False
```

### hubNetworkResourceId

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

The resource ID of the Virtual Network or Virtual WAN Hub in the hub to which the created Virtual Network, by this module, will be peered/connected to via Virtual Network Peering or a Virtual WAN Virtual Hub Connection.

**Example Expected Values:**
- `''` (empty string)
- Hub Virtual Network Resource ID: `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/xxxxxxxxxx/providers/Microsoft.Network/virtualNetworks/xxxxxxxxxx`
- Virtual WAN Virtual Hub Resource ID: `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/xxxxxxxxxx/providers/Microsoft.Network/virtualHubs/xxxxxxxxxx`

- Type: String
- Default value: `''` *(empty string)*


### virtualNetworkUseRemoteGateways

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Enables the use of remote gateways in the specified hub virtual network.

> **IMPORTANT:** If no gateways exist in the hub virtual network, set this to `false`, otherwise peering will fail to create.

- Type: Boolean


**Default value**

```text
True
```

### virtualNetworkVwanEnableInternetSecurity

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Enables the ability for the Virtual WAN Hub Connection to learn the default route 0.0.0.0/0 from the Hub.

- Type: Boolean


**Default value**

```text
True
```

### virtualNetworkVwanAssociatedRouteTableResourceId

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

The resource ID of the virtual hub route table to associate to the virtual hub connection (this virtual network). If left blank/empty the `defaultRouteTable` will be associated.

- Type: String
- Default value: `''` *(empty string)* = Which means if the parameter `virtualNetworkPeeringEnabled` is `true` and also the parameter `hubNetworkResourceId` is not empty then the `defaultRouteTable` will be associated of the provided Virtual Hub in the parameter `hubNetworkResourceId`.
    - e.g. `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/xxxxxxxxxx/providers/Microsoft.Network/virtualHubs/xxxxxxxxx/hubRouteTables/defaultRouteTable`


### virtualNetworkVwanPropagatedRouteTablesResourceIds

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

An array of of objects of virtual hub route table resource IDs to propagate routes to. If left blank/empty the `defaultRouteTable` will be propagated to only.

Each object must contain the following `key`:
- `id` = The Resource ID of the Virtual WAN Virtual Hub Route Table IDs you wish to propagate too

> See below [example in parameter file](#parameter-file)

> **IMPORTANT:** If you provide any Route Tables in this array of objects you must ensure you include also the `defaultRouteTable` Resource ID as an object in the array as it is not added by default when a value is provided for this parameter.

- Type: `[]` Array
- Default value: `[]` *(empty array)*


### virtualNetworkVwanPropagatedLabels

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

An array of virtual hub route table labels to propagate routes to. If left blank/empty the default label will be propagated to only.

- Type: `[]` Array
- Default value: `[]` *(empty array)*

### vHubRoutingIntentEnabled 

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Indicates whether routing intent is enabled in the virtual hub. If it is enabled and this is not set the deployment will fail.

- Type: Boolean

**Default value**

```text
False
```

### roleAssignmentEnabled

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Whether to create role assignments or not. If true, supply the array of role assignment objects in the parameter called `roleAssignments`.

- Type: Boolean


**Default value**

```text
False
```

### roleAssignments

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Supply an array of objects containing the details of the role assignments to create.

Each object must contain the following `keys`:
- `principalId` = The Object ID of the User, Group, SPN, Managed Identity to assign the RBAC role too.
- `definition` = The Name of built-In RBAC Roles or a Resource ID of a Built-in or custom RBAC Role Definition.
- `relativeScope` = 2 options can be provided for input value:
    1. `''` *(empty string)* = Make RBAC Role Assignment to Subscription scope
    2. `'/resourceGroups/<RESOURCE GROUP NAME>'` = Make RBAC Role Assignment to specified Resource Group

> See below [example in parameter file](#parameter-file) of various combinations

- Type: `[]` Array
- Default value: `[]` *(empty array)*


### disableTelemetry

![Parameter Setting](https://img.shields.io/badge/parameter-optional-green?style=flat-square)

Disable telemetry collection by this module.

For more information on the telemetry collected by this module, that is controlled by this parameter, see this page in the wiki: [Telemetry Tracking Using Customer Usage Attribution (PID)](https://github.com/Azure/bicep-lz-vending/wiki/Telemetry)


**Default value**

```text
False
```

## Outputs

Name | Type | Description
---- | ---- | -----------
subscriptionId | string | The Subscription ID that has been created or provided.
subscriptionResourceId | string | The Subscription Resource ID that has been created or provided.
subscriptionAcceptOwnershipState | string | The Subscription Owner State. Only used when creating MCA Subscriptions across tenants
subscriptionAcceptOwnershipUrl | string | The Subscription Ownership URL. Only used when creating MCA Subscriptions across tenants

## Snippets

### Parameter file

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "metadata": {
        "template": null
    },
    "parameters": {
        "subscriptionAliasEnabled": {
            "value": true
        },
        "subscriptionDisplayName": {
            "value": "sub-bicep-lz-vending-example-001"
        },
        "subscriptionAliasName": {
            "value": "sub-bicep-lz-vending-example-001"
        },
        "subscriptionBillingScope": {
            "value": "providers/Microsoft.Billing/billingAccounts/1234567/enrollmentAccounts/123456"
        },
        "subscriptionWorkload": {
            "value": "Production"
        },
        "subscriptionTenantId": {
            "value": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        },
        "subscriptionOwnerId": {
            "value": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        },
        "existingSubscriptionId": {
            "value": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        },
        "subscriptionManagementGroupAssociationEnabled": {
            "value": true
        },
        "subscriptionManagementGroupId": {
            "value": "alz-landingzones-corp"
        },
        "subscriptionTags": {
            "value": {
                "tagKey1": "value",
                "tag-key-2": "value"
            }
        },
        "virtualNetworkEnabled": {
            "value": true
        },
        "virtualNetworkResourceGroupName": {
            "value": "rg-networking-001"
        },
        "virtualNetworkResourceGroupTags": {
            "value": {
                "tagKey1": "value",
                "tag-key-2": "value"
            }
        },
        "virtualNetworkResourceGroupLockEnabled": {
            "value": true
        },
        "virtualNetworkLocation": {
            "value": "uksouth"
        },
        "virtualNetworkName": {
            "value": "vnet-example-001"
        },
        "virtualNetworkTags": {
            "value": {
                "tagKey1": "value",
                "tag-key-2": "value"
            }
        },
        "virtualNetworkAddressSpace": {
            "value": [
                "10.0.0.0/16"
            ]
        },
        "virtualNetworkDnsServers": {
            "value": [
                "10.4.1.4",
                "10.2.1.5"
            ]
        },
        "virtualNetworkDdosPlanId": {
            "value": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/xxxxxxxxxx/providers/Microsoft.Network/ddosProtectionPlans/xxxxxxxxxx"
        },
        "virtualNetworkPeeringEnabled": {
            "value": true
        },
        "hubNetworkResourceId": {
            "value": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/xxxxxxxxxx/providers/Microsoft.Network/virtualNetworks/xxxxxxxxxx"
        },
        "virtualNetworkUseRemoteGateways": {
            "value": true
        },
        "virtualNetworkVwanEnableInternetSecurity": {
            "value": true
        },
        "virtualNetworkVwanAssociatedRouteTableResourceId": {
            "value": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/xxxxxxxxxx/providers/Microsoft.Network/virtualHubs/xxxxxxxxx/hubRouteTables/xxxxxxxxx"
        },
        "virtualNetworkVwanPropagatedRouteTablesResourceIds": {
            "value": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/xxxxxxxxxx/providers/Microsoft.Network/virtualHubs/xxxxxxxxx/hubRouteTables/defaultRouteTable"
                },
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/xxxxxxxxxx/providers/Microsoft.Network/virtualHubs/xxxxxxxxx/hubRouteTables/xxxxxxxxx"
                }
            ]
        },
        "virtualNetworkVwanPropagatedLabels": {
            "value": [
                "default",
                "anotherLabel"
            ]
        },
        "roleAssignmentEnabled": {
            "value": true
        },
        "roleAssignments": {
            "value": [
                {
                    "principalId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
                    "definition": "Contributor",
                    "relativeScope": ""
                },
                {
                    "principalId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
                    "definition": "/providers/Microsoft.Authorization/roleDefinitions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
                    "relativeScope": ""
                },
                {
                    "principalId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
                    "definition": "Reader",
                    "relativeScope": "/resourceGroups/rsg-networking-001"
                },
                {
                    "principalId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
                    "definition": "/providers/Microsoft.Authorization/roleDefinitions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
                    "relativeScope": "/resourceGroups/rsg-networking-001"
                }
            ]
        },
        "disableTelemetry": {
            "value": false
        }
    }
}
```
