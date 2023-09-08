# cp1-criacao-recursos-nuvem
## cloud shell bash

#### Implantação de VM com Azure CLI
<details>
<summary>Ex1 (clique para abrir)</summary>

```bash
# Definir variáveis

vinicius [ ~ ]$ resourceGroupName="DimDimResources"           # Nome do grupo de recursos
location="eastus"                             # Região onde os recursos serão criados
vmName="DimDiRM94266"                         # Nome da máquina virtual
vmSize="Standard_DS2_v2"                      # Tamanho da máquina virtual
image="UbuntuLTS"                             # Imagem do sistema operacional
tags="Ambiente=Desenvolvimento Projeto=DimDimCloud" # Tags para a máquina virtual

# Informações necessárias do úsuario

vinicius [ ~ ]$ read -p "Nome do disco: " diskName             # Nome do disco
read -p "Tamanho do disco em GB: " diskSizeGB  # Tamanho do disco em GB
read -p "Nome da Rede Virtual: " vnetName      # Nome da Rede Virtual
read -p "Nome do Grupo de Segurança de Rede: " nsgName  # Nome do Grupo de Segurança de Rede
read -p "Nome de usuário: " username           # Nome de usuário para a VM
read -s -p "Senha: " password                  # Solicitar senha de forma segura

# Criar grupo de recursos

vinicius [ ~ ]$ az group create --name $resourceGroupName --location $location

# Criar máquina virtual

vinicius [ ~ ]$ az vm create \
  --resource-group $resourceGroupName \
  --name $vmName \
  --image $image \
  --size $vmSize \
  --admin-username $username \
  --admin-password $password \
  --authentication-type password \
  --nsg $nsgName \
  --vnet-name $vnetName \
  --os-disk-size-gb $diskSizeGB \
  --tags $tags

vinicius [ ~ ]$ read -s -p "Senha: " password
Senha: vinicius az vm create \reate \
  --resource-group $resourceGroupName \
  --name $vmName \
  --image $image \
  --size $vmSize \
  --admin-username $username \
  --admin-password $password \
  --authentication-type password \
  --nsg $nsgName \
  --vnet-name $vnetName \
  --os-disk-size-gb $diskSizeGB \
  --tags $tags
Ignite (November) 2023 onwards "az vm/vmss create" command will deploy Gen2-Trusted Launch VM by default. To know more about the default change and Trusted Launch, please visit https://aka.ms/TLaD
It is recommended to use parameter "--public-ip-sku Standard" to create new VM with Standard public IP. Please note that the default public IP used for VM creation will be changed from Basic to Standard in the future.
Consider using the "Ubuntu2204" alias. On April 30, 2023,the image deployed by the "UbuntuLTS" alias reaches its end of life. The "UbuntuLTS" will be removed with the breaking change release of Fall 2023.
{
  "fqdns": "",
  "id": "/subscriptions/5af540a5-2ea7-4479-a2fe-f509ee018f11/resourceGroups/DimDimResources/providers/Microsoft.Compute/virtualMachines/DimDiRM94266",
  "location": "eastus",
  "macAddress": "60-45-BD-D9-E4-99",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "172.173.152.95",
  "resourceGroup": "DimDimResources",
  "zones": ""
}

vinicius [ ~ ]$ ls -la
total 56
drwxr-xr-x 3 vinicius vinicius  4096 Aug 27 19:50 .
drwxrwxrwx 3 root     root      4096 Aug 27 19:47 ..
drwx------ 5 vinicius vinicius  4096 Aug 27 19:52 .azure
-rw------- 1 vinicius vinicius  3921 Aug 27 19:57 .bash_history
-rw-r--r-- 1 vinicius vinicius   178 Jul 21 17:37 .bash_logout
-rw-r--r-- 1 vinicius vinicius   645 Jul 21 17:37 .bash_profile
-rw-r--r-- 1 vinicius vinicius   985 Aug 27 19:47 .bashrc
lrwxrwxrwx 1 vinicius vinicius    22 Aug 27 19:47 clouddrive -> /usr/csuser/clouddrive
-rw-r--r-- 1 vinicius vinicius    42 Aug 27 19:47 .tmux.conf
-rw-r--r-- 1 vinicius vinicius 22287 Jun 17  2022 .zshrc
```

</details>
  
#### Implantação de Recursos de Aplicação Web .net com Azure CLI

<details>
<summary>Ex2 (clique para abrir)</summary>
  
```bash
felipe [ ~ ]$ #criando grupo de recurso
felipe [ ~ ]$ az group create --name DimDimAppResources --location westeurope
{
  "id": "/subscriptions/da9a6d86-ab87-497a-8d8a-d98185d23cea/resourceGroups/DimDimAppResources",
  "location": "westeurope",
  "managedBy": null,
  "name": "DimDimAppResources",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
felipe [ ~ ]$ #Criando serviço de aplicativo
felipe [ ~ ]$ az appservice plan create --name DimDimAppPlan --resource-group DimDimAppResources --sku FREE
{
  "elasticScaleEnabled": false,
  "extendedLocation": null,
  "freeOfferExpirationTime": null,
  "geoRegion": "West Europe",
  "hostingEnvironmentProfile": null,
  "hyperV": false,
  "id": "/subscriptions/da9a6d86-ab87-497a-8d8a-d98185d23cea/resourceGroups/DimDimAppResources/providers/Microsoft.Web/serverfarms/DimDimAppPlan",
  "isSpot": false,
  "isXenon": false,
  "kind": "app",
  "kubeEnvironmentProfile": null,
  "location": "westeurope",
  "maximumElasticWorkerCount": 1,
  "maximumNumberOfWorkers": 0,
  "name": "DimDimAppPlan",
  "numberOfSites": 0,
  "numberOfWorkers": 0,
  "perSiteScaling": false,
  "provisioningState": "Succeeded",
  "reserved": false,
  "resourceGroup": "DimDimAppResources",
  "sku": {
    "capabilities": null,
    "capacity": 0,
    "family": "F",
    "locations": null,
    "name": "F1",
    "size": "F1",
    "skuCapacity": null,
    "tier": "Free"
  },
  "spotExpirationTime": null,
  "status": "Ready",
  "subscription": "da9a6d86-ab87-497a-8d8a-d98185d23cea",
  "tags": null,
  "targetWorkerCount": 0,
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null,
  "zoneRedundant": false
}
felipe [ ~ ]$ az webapp list-runtimes --os-type windows
[
  "dotnet:7",
  "dotnet:6",
  "ASPNET:V4.8",
  "ASPNET:V3.5",
  "NODE:18LTS",
  "NODE:16LTS",
  "java:1.8:Java SE:8",
  "java:11:Java SE:11",
  "java:17:Java SE:17",
  "java:1.8:TOMCAT:10.0",
  "java:11:TOMCAT:10.0",
  "java:17:TOMCAT:10.0",
  "java:1.8:TOMCAT:9.0",
  "java:11:TOMCAT:9.0",
  "java:17:TOMCAT:9.0",
  "java:1.8:TOMCAT:8.5",
  "java:11:TOMCAT:8.5",
  "java:17:TOMCAT:8.5"
]
felipe [ ~ ]$ az webapp create --name WebAppRM94266e --resource-group DimDimAppResources --plan DimDimAppPlan --runtime "dotnet:7"
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "clientCertExclusionPaths": null,
  "clientCertMode": "Required",
  "cloningInfo": null,
  "containerSize": 0,
  "customDomainVerificationId": "EE71DDAE164806A5409EF03B4B10766153DA1768306685C710957DFB7DCAD3EE",
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "webapprm94266e.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "webapprm94266e.azurewebsites.net",
    "webapprm94266e.scm.azurewebsites.net"
  ],
  "extendedLocation": null,
  "ftpPublishingUrl": "ftps://waws-prod-am2-485.ftp.azurewebsites.windows.net/site/wwwroot",
  "hostNameSslStates": [
    {
      "certificateResourceId": null,
      "hostType": "Standard",
      "ipBasedSslResult": null,
      "ipBasedSslState": "NotConfigured",
      "name": "webapprm94266e.azurewebsites.net",
      "sslState": "Disabled",
      "thumbprint": null,
      "toUpdate": null,
      "toUpdateIpBasedSsl": null,
      "virtualIp": null
    },
    {
      "certificateResourceId": null,
      "hostType": "Repository",
      "ipBasedSslResult": null,
      "ipBasedSslState": "NotConfigured",
      "name": "webapprm94266e.scm.azurewebsites.net",
      "sslState": "Disabled",
      "thumbprint": null,
      "toUpdate": null,
      "toUpdateIpBasedSsl": null,
      "virtualIp": null
    }
  ],
  "hostNames": [
    "webapprm94266e.azurewebsites.net"
  ],
  "hostNamesDisabled": false,
  "hostingEnvironmentProfile": null,
  "httpsOnly": false,
  "hyperV": false,
  "id": "/subscriptions/da9a6d86-ab87-497a-8d8a-d98185d23cea/resourceGroups/DimDimAppResources/providers/Microsoft.Web/sites/WebAppRM94266e",
  "identity": null,
  "inProgressOperationId": null,
  "isDefaultContainer": null,
  "isXenon": false,
  "keyVaultReferenceIdentity": "SystemAssigned",
  "kind": "app",
  "lastModifiedTimeUtc": "2023-09-07T17:11:44.576666",
  "location": "West Europe",
  "maxNumberOfWorkers": null,
  "name": "WebAppRM94266e",
  "outboundIpAddresses": "20.76.202.176,20.76.202.219,20.76.202.251,20.76.203.229,20.76.205.16,20.76.205.70,20.50.2.79",
  "possibleOutboundIpAddresses": "20.76.202.176,20.76.202.219,20.76.202.251,20.76.203.229,20.76.205.16,20.76.205.70,20.101.200.78,20.101.200.94,20.101.200.121,20.101.200.155,20.101.200.187,20.101.200.225,20.101.200.231,20.101.200.232,20.101.201.11,20.101.201.21,20.101.201.31,20.101.201.33,20.101.201.34,20.101.201.38,20.101.201.60,20.101.201.73,20.101.201.110,20.101.200.229,20.101.200.244,20.101.200.245,20.101.201.1,20.101.201.4,20.101.201.5,20.101.201.14,20.50.2.79",
  "publicNetworkAccess": null,
  "redundancyMode": "None",
  "repositorySiteName": "WebAppRM94266e",
  "reserved": false,
  "resourceGroup": "DimDimAppResources",
  "scmSiteAlsoStopped": false,
  "serverFarmId": "/subscriptions/da9a6d86-ab87-497a-8d8a-d98185d23cea/resourceGroups/DimDimAppResources/providers/Microsoft.Web/serverfarms/DimDimAppPlan",
  "siteConfig": {
    "acrUseManagedIdentityCreds": false,
    "acrUserManagedIdentityId": null,
    "alwaysOn": false,
    "antivirusScanEnabled": null,
    "apiDefinition": null,
    "apiManagementConfig": null,
    "appCommandLine": null,
    "appSettings": null,
    "autoHealEnabled": null,
    "autoHealRules": null,
    "autoSwapSlotName": null,
    "azureMonitorLogCategories": null,
    "azureStorageAccounts": null,
    "connectionStrings": null,
    "cors": null,
    "customAppPoolIdentityAdminState": null,
    "customAppPoolIdentityTenantState": null,
    "defaultDocuments": null,
    "detailedErrorLoggingEnabled": null,
    "documentRoot": null,
    "elasticWebAppScaleLimit": 0,
    "experiments": null,
    "fileChangeAuditEnabled": null,
    "ftpsState": null,
    "functionAppScaleLimit": null,
    "functionsRuntimeScaleMonitoringEnabled": null,
    "handlerMappings": null,
    "healthCheckPath": null,
    "http20Enabled": false,
    "http20ProxyFlag": null,
    "httpLoggingEnabled": null,
    "ipSecurityRestrictions": [
      {
        "action": "Allow",
        "description": "Allow all access",
        "headers": null,
        "ipAddress": "Any",
        "name": "Allow all",
        "priority": 2147483647,
        "subnetMask": null,
        "subnetTrafficTag": null,
        "tag": null,
        "vnetSubnetResourceId": null,
        "vnetTrafficTag": null
      }
    ],
    "ipSecurityRestrictionsDefaultAction": null,
    "javaContainer": null,
    "javaContainerVersion": null,
    "javaVersion": null,
    "keyVaultReferenceIdentity": null,
    "limits": null,
    "linuxFxVersion": "",
    "loadBalancing": null,
    "localMySqlEnabled": null,
    "logsDirectorySizeLimit": null,
    "machineKey": null,
    "managedPipelineMode": null,
    "managedServiceIdentityId": null,
    "metadata": null,
    "minTlsCipherSuite": null,
    "minTlsVersion": null,
    "minimumElasticInstanceCount": 0,
    "netFrameworkVersion": null,
    "nodeVersion": null,
    "numberOfWorkers": 1,
    "phpVersion": null,
    "powerShellVersion": null,
    "preWarmedInstanceCount": null,
    "publicNetworkAccess": null,
    "publishingPassword": null,
    "publishingUsername": null,
    "push": null,
    "pythonVersion": null,
    "remoteDebuggingEnabled": null,
    "remoteDebuggingVersion": null,
    "requestTracingEnabled": null,
    "requestTracingExpirationTime": null,
    "routingRules": null,
    "runtimeADUser": null,
    "runtimeADUserPassword": null,
    "scmIpSecurityRestrictions": [
      {
        "action": "Allow",
        "description": "Allow all access",
        "headers": null,
        "ipAddress": "Any",
        "name": "Allow all",
        "priority": 2147483647,
        "subnetMask": null,
        "subnetTrafficTag": null,
        "tag": null,
        "vnetSubnetResourceId": null,
        "vnetTrafficTag": null
      }
    ],
    "scmIpSecurityRestrictionsDefaultAction": null,
    "scmIpSecurityRestrictionsUseMain": null,
    "scmMinTlsVersion": null,
    "scmType": null,
    "sitePort": null,
    "storageType": null,
    "supportedTlsCipherSuites": null,
    "tracingOptions": null,
    "use32BitWorkerProcess": null,
    "virtualApplications": null,
    "vnetName": null,
    "vnetPrivatePortsCount": null,
    "vnetRouteAllEnabled": null,
    "webSocketsEnabled": null,
    "websiteTimeZone": null,
    "winAuthAdminState": null,
    "winAuthTenantState": null,
    "windowsConfiguredStacks": null,
    "windowsFxVersion": null,
    "xManagedServiceIdentityId": null
  },
  "slotSwapStatus": null,
  "state": "Running",
  "storageAccountRequired": false,
  "suspendedTill": null,
  "tags": null,
  "targetSwapSlot": null,
  "trafficManagerHostNames": null,
  "type": "Microsoft.Web/sites",
  "usageState": "Normal",
  "virtualNetworkSubnetId": null,
  "vnetContentShareEnabled": false,
  "vnetImagePullEnabled": false,
  "vnetRouteAllEnabled": false
}
felipe [ ~ ]$ az group list --output table
Name                        Location    Status
--------------------------  ----------  ---------
DimDimAppResources          westeurope  Succeeded
cloud-shell-storage-eastus  eastus      Succeeded
felipe [ ~ ]$ az group show --name DimDimAppResources
{
  "id": "/subscriptions/da9a6d86-ab87-497a-8d8a-d98185d23cea/resourceGroups/DimDimAppResources",
  "location": "westeurope",
  "managedBy": null,
  "name": "DimDimAppResources",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
felipe [ ~ ]$ az appservice plan list --resource-group DimDimAppResources
[
  {
    "elasticScaleEnabled": false,
    "extendedLocation": null,
    "freeOfferExpirationTime": null,
    "hostingEnvironmentProfile": null,
    "hyperV": false,
    "id": "/subscriptions/da9a6d86-ab87-497a-8d8a-d98185d23cea/resourceGroups/DimDimAppResources/providers/Microsoft.Web/serverfarms/DimDimAppPlan",
    "isSpot": false,
    "isXenon": false,
    "kind": "app",
    "kubeEnvironmentProfile": null,
    "location": "West Europe",
    "maximumElasticWorkerCount": 1,
    "maximumNumberOfWorkers": 1,
    "name": "DimDimAppPlan",
    "numberOfSites": 1,
    "numberOfWorkers": 0,
    "perSiteScaling": false,
    "provisioningState": "Succeeded",
    "reserved": false,
    "resourceGroup": "DimDimAppResources",
    "sku": {
      "capabilities": null,
      "capacity": 0,
      "family": "F",
      "locations": null,
      "name": "F1",
      "size": "F1",
      "skuCapacity": null,
      "tier": "Free"
    },
    "spotExpirationTime": null,
    "status": "Ready",
    "tags": null,
    "targetWorkerCount": 0,
    "targetWorkerSizeId": 0,
    "type": "Microsoft.Web/serverfarms",
    "workerTierName": null,
    "zoneRedundant": false
  }
]
felipe [ ~ ]$ az webapp list --resource-group DimDimAppResources
[
  {
    "appServicePlanId": "/subscriptions/da9a6d86-ab87-497a-8d8a-d98185d23cea/resourceGroups/DimDimAppResources/providers/Microsoft.Web/serverfarms/DimDimAppPlan",
    "availabilityState": "Normal",
    "clientAffinityEnabled": true,
    "clientCertEnabled": false,
    "clientCertExclusionPaths": null,
    "clientCertMode": "Required",
    "cloningInfo": null,
    "containerSize": 0,
    "customDomainVerificationId": "EE71DDAE164806A5409EF03B4B10766153DA1768306685C710957DFB7DCAD3EE",
    "dailyMemoryTimeQuota": 0,
    "defaultHostName": "webapprm94266.azurewebsites.net",
    "enabled": true,
    "enabledHostNames": [
      "webapprm94266.azurewebsites.net",
      "webapprm94266.scm.azurewebsites.net"
    ],
    "extendedLocation": null,
    "hostNameSslStates": [
      {
        "certificateResourceId": null,
        "hostType": "Standard",
        "ipBasedSslResult": null,
        "ipBasedSslState": "NotConfigured",
        "name": "webapprm94266.azurewebsites.net",
        "sslState": "Disabled",
        "thumbprint": null,
        "toUpdate": null,
        "toUpdateIpBasedSsl": null,
        "virtualIp": null
      },
      {
        "certificateResourceId": null,
        "hostType": "Repository",
        "ipBasedSslResult": null,
        "ipBasedSslState": "NotConfigured",
        "name": "webapprm94266.scm.azurewebsites.net",
        "sslState": "Disabled",
        "thumbprint": null,
        "toUpdate": null,
        "toUpdateIpBasedSsl": null,
        "virtualIp": null
      }
    ],
    "hostNames": [
      "webapprm94266.azurewebsites.net"
    ],
    "hostNamesDisabled": false,
    "hostingEnvironmentProfile": null,
    "httpsOnly": false,
    "hyperV": false,
    "id": "/subscriptions/da9a6d86-ab87-497a-8d8a-d98185d23cea/resourceGroups/DimDimAppResources/providers/Microsoft.Web/sites/WebAppRM94266",
    "identity": null,
    "inProgressOperationId": null,
    "isDefaultContainer": null,
    "isXenon": false,
    "keyVaultReferenceIdentity": "SystemAssigned",
    "kind": "app",
    "lastModifiedTimeUtc": "2023-09-07T17:09:06.340000",
    "location": "West Europe",
    "maxNumberOfWorkers": null,
    "name": "WebAppRM94266",
    "outboundIpAddresses": "20.76.202.176,20.76.202.219,20.76.202.251,20.76.203.229,20.76.205.16,20.76.205.70,20.50.2.79",
    "possibleOutboundIpAddresses": "20.76.202.176,20.76.202.219,20.76.202.251,20.76.203.229,20.76.205.16,20.76.205.70,20.101.200.78,20.101.200.94,20.101.200.121,20.101.200.155,20.101.200.187,20.101.200.225,20.101.200.231,20.101.200.232,20.101.201.11,20.101.201.21,20.101.201.31,20.101.201.33,20.101.201.34,20.101.201.38,20.101.201.60,20.101.201.73,20.101.201.110,20.101.200.229,20.101.200.244,20.101.200.245,20.101.201.1,20.101.201.4,20.101.201.5,20.101.201.14,20.50.2.79",
    "publicNetworkAccess": null,
    "redundancyMode": "None",
    "repositorySiteName": "WebAppRM94266",
    "reserved": false,
    "resourceGroup": "DimDimAppResources",
    "scmSiteAlsoStopped": false,
    "siteConfig": {
      "acrUseManagedIdentityCreds": false,
      "acrUserManagedIdentityId": null,
      "alwaysOn": false,
      "antivirusScanEnabled": null,
      "apiDefinition": null,
      "apiManagementConfig": null,
      "appCommandLine": null,
      "appSettings": null,
      "autoHealEnabled": null,
      "autoHealRules": null,
      "autoSwapSlotName": null,
      "azureMonitorLogCategories": null,
      "azureStorageAccounts": null,
      "connectionStrings": null,
      "cors": null,
      "customAppPoolIdentityAdminState": null,
      "customAppPoolIdentityTenantState": null,
      "defaultDocuments": null,
      "detailedErrorLoggingEnabled": null,
      "documentRoot": null,
      "elasticWebAppScaleLimit": null,
      "experiments": null,
      "fileChangeAuditEnabled": null,
      "ftpsState": null,
      "functionAppScaleLimit": 0,
      "functionsRuntimeScaleMonitoringEnabled": null,
      "handlerMappings": null,
      "healthCheckPath": null,
      "http20Enabled": true,
      "http20ProxyFlag": null,
      "httpLoggingEnabled": null,
      "ipSecurityRestrictions": null,
      "ipSecurityRestrictionsDefaultAction": null,
      "javaContainer": null,
      "javaContainerVersion": null,
      "javaVersion": null,
      "keyVaultReferenceIdentity": null,
      "limits": null,
      "linuxFxVersion": "",
      "loadBalancing": null,
      "localMySqlEnabled": null,
      "logsDirectorySizeLimit": null,
      "machineKey": null,
      "managedPipelineMode": null,
      "managedServiceIdentityId": null,
      "metadata": null,
      "minTlsCipherSuite": null,
      "minTlsVersion": null,
      "minimumElasticInstanceCount": 0,
      "netFrameworkVersion": null,
      "nodeVersion": null,
      "numberOfWorkers": 1,
      "phpVersion": null,
      "powerShellVersion": null,
      "preWarmedInstanceCount": null,
      "publicNetworkAccess": null,
      "publishingPassword": null,
      "publishingUsername": null,
      "push": null,
      "pythonVersion": null,
      "remoteDebuggingEnabled": null,
      "remoteDebuggingVersion": null,
      "requestTracingEnabled": null,
      "requestTracingExpirationTime": null,
      "routingRules": null,
      "runtimeADUser": null,
      "runtimeADUserPassword": null,
      "scmIpSecurityRestrictions": null,
      "scmIpSecurityRestrictionsDefaultAction": null,
      "scmIpSecurityRestrictionsUseMain": null,
      "scmMinTlsVersion": null,
      "scmType": null,
      "sitePort": null,
      "storageType": null,
      "supportedTlsCipherSuites": null,
      "tracingOptions": null,
      "use32BitWorkerProcess": null,
      "virtualApplications": null,
      "vnetName": null,
      "vnetPrivatePortsCount": null,
      "vnetRouteAllEnabled": null,
      "webSocketsEnabled": null,
      "websiteTimeZone": null,
      "winAuthAdminState": null,
      "winAuthTenantState": null,
      "windowsConfiguredStacks": null,
      "windowsFxVersion": null,
      "xManagedServiceIdentityId": null
    },
    "slotSwapStatus": null,
    "state": "Running",
    "storageAccountRequired": false,
    "suspendedTill": null,
    "tags": null,
    "targetSwapSlot": null,
    "trafficManagerHostNames": null,
    "type": "Microsoft.Web/sites",
    "usageState": "Normal",
    "virtualNetworkSubnetId": null,
    "vnetContentShareEnabled": false,
    "vnetImagePullEnabled": false,
    "vnetRouteAllEnabled": false
  }
]
```
</details>

#### Implantação de Recurso IoT Hub com Azure CLI
<details>
<summary>Ex3 (clique para abrir)</summary>

```bash
vinicius [ ~ ]$ #Varieavel com nome do recurso:
vinicius [ ~ ]$ RESOURCE_NAME="DimDimIoTHubRM92895"
vinicius [ ~ ]$ #Informar o nome do user:
vinicius [ ~ ]$ read -p "Informe o nome do recurso: " RESOURCE_NAME
Informe o nome do recurso: DimDimIoTHubRM92895
vinicius [ ~ ]$ #Variavel com nome da região:
vinicius [ ~ ]$ REGION="brazilsouth"
vinicius [ ~ ]$ #Variavel com tipo de serviço:
vinicius [ ~ ]$ SERVICE_TYPE="IoTHub"
vinicius [ ~ ]$ #Variavel com camada de preço:
vinicius [ ~ ]$ SKU="F0" 
vinicius [ ~ ]$ #Criando o recurso
vinicius [ ~ ]$ az group create --name DimDimIoTHubRM92895 --location brazilsouth
{
  "id": "/subscriptions/84633a21-b3c2-4be7-8c94-37a90bb8f650/resourceGroups/DimDimIoTHubRM92895",
  "location": "brazilsouth",
  "managedBy": null,
  "name": "DimDimIoTHubRM92895",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
vinicius [ ~ ]$ az cognitiveservices account create --resource-group DimDimIoTHubRM92895 --name DimDimIoTHubRM92895 --sku $SKU --kind $SERVICE_TYPE --location $REGION
Resource provider 'Microsoft.CognitiveServices' used by this operation is not registered. We are registering for you.
Registration succeeded.
(InvalidApiSetId) The account type 'IoTHub' is either invalid or unavailable in given region.
Code: InvalidApiSetId
Message: The account type 'IoTHub' is either invalid or unavailable in given region.
```
</details>

#### Integração do Azure Computer Vision em um App Mobile
<details>
<summary>Ex4 (clique para abrir)</summary>

```bash
vinicius [ ~ ]$ #Varieavel com nome do recurso:
vinicius [ ~ ]$ RESOURCE_NAME="DimDimCVRM94266"
vinicius [ ~ ]$ #Informar o nome do user:
vinicius [ ~ ]$ read -p "Informe o nome do recurso: " RESOURCE_NAME
Informe o nome do recurso: DimDimCVRM94266
vinicius [ ~ ]$ #Variavel com nome da região:
vinicius [ ~ ]$ REGION="brazilsouth"
vinicius [ ~ ]$ #Variavel com tipo de serviço:
vinicius [ ~ ]$ SERVICE_TYPE="ComputerVision"
vinicius [ ~ ]$ #Tipo do serviço:
vinicius [ ~ ]$ SERVICE_TYPE="ComputerVision"
vinicius [ ~ ]$ #Variavel com camada de preço:
vinicius [ ~ ]$ SKU="F0"   
vinicius [ ~ ]$ #Criando o recurso
vinicius [ ~ ]$ az group create --name DimDimCVRM94266 --location brazilsouth
{
  "id": "/subscriptions/5af540a5-2ea7-4479-a2fe-f509ee018f11/resourceGroups/DimDimCVRM94266",
  "location": "brazilsouth",
  "managedBy": null,
  "name": "DimDimCVRM94266",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
vinicius [ ~ ]$ az cognitiveservices account create --resource-group DimDimCVRM94266 --name DimDimCVRM94266 --sku $SKU --kind $SERVICE_TYPE --location $REGION
{
  "etag": "\"020052ab-0000-0b00-0000-64fa37b70000\"",
  "id": "/subscriptions/5af540a5-2ea7-4479-a2fe-f509ee018f11/resourceGroups/DimDimCVRM94266/providers/Microsoft.CognitiveServices/accounts/DimDimCVRM94266",
  "identity": null,
  "kind": "ComputerVision",
  "location": "brazilsouth",
  "name": "DimDimCVRM94266",
  "properties": {
    "abusePenalty": null,
    "allowedFqdnList": null,
    "apiProperties": null,
    "callRateLimit": null,
    "capabilities": [
      {
        "name": "VirtualNetworks",
        "value": null
      },
      {
        "name": "Container",
        "value": "ComputerVision.VideoAnalytics,ComputerVision.ComputerVisionRead,ComputerVision.ocr,ComputerVision.readfile,ComputerVision.readfiledsd,ComputerVision.recognizetext,ComputerVision.ComputerVision,ComputerVision.ocrlayoutworker,ComputerVision.ocrcontroller,ComputerVision.ocrdispatcher,ComputerVision.ocrbillingprocessor,ComputerVision.ocranalyzer,ComputerVision.ocrpagesplitter,ComputerVision.ocrapi,ComputerVision.ocrengineworker"
      }
    ],
    "commitmentPlanAssociations": null,
    "customSubDomainName": null,
    "dateCreated": "2023-09-07T20:51:03.4616943Z",
    "deletionDate": null,
    "disableLocalAuth": null,
    "dynamicThrottlingEnabled": null,
    "encryption": null,
    "endpoint": "https://brazilsouth.api.cognitive.microsoft.com/",
    "endpoints": {
      "Computer Vision": "https://brazilsouth.api.cognitive.microsoft.com/",
      "Container": "https://brazilsouth.api.cognitive.microsoft.com/"
    },
    "internalId": "b9303b17a0b1460e8a188013919c0f39",
    "isMigrated": false,
    "locations": null,
    "migrationToken": null,
    "networkAcls": null,
    "privateEndpointConnections": [],
    "provisioningState": "Succeeded",
    "publicNetworkAccess": "Enabled",
    "quotaLimit": null,
    "restore": null,
    "restrictOutboundNetworkAccess": null,
    "scheduledPurgeDate": null,
    "skuChangeInfo": null,
    "userOwnedStorage": null
  },
  "resourceGroup": "DimDimCVRM94266",
  "sku": {
    "capacity": null,
    "family": null,
    "name": "F0",
    "size": null,
    "tier": null
  },
  "systemData": {
    "createdAt": "2023-09-07T20:51:02.888832+00:00",
    "createdBy": "RM94266@fiap.com.br",
    "createdByType": "User",
    "lastModifiedAt": "2023-09-07T20:51:02.888832+00:00",
    "lastModifiedBy": "RM94266@fiap.com.br",
    "lastModifiedByType": "User"
  },
  "tags": null,
  "type": "Microsoft.CognitiveServices/accounts"
}
```
</details>
