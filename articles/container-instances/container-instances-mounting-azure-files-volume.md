---
title: "Instalowanie plików Azure woluminu w wystąpień kontenera platformy Azure"
description: "Dowiedz się, jak można zainstalować woluminu plików Azure, aby utrwalić stanu z wystąpień kontenera platformy Azure"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 4248a3769ba8a0fb067b3904d55d487fe67e5778
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a><span data-ttu-id="d6607-103">Instalowanie udziału plików na platformę Azure z wystąpień kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d6607-103">Mounting an Azure file share with Azure Container Instances</span></span>

<span data-ttu-id="d6607-104">Domyślnie bezstanowe są wystąpień kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d6607-104">By default, Azure Container Instances are stateless.</span></span> <span data-ttu-id="d6607-105">Kontener ulegnie awarii lub przestanie, wszystkie jego stan zostanie utracone.</span><span class="sxs-lookup"><span data-stu-id="d6607-105">If the container crashes or stops, all of its state is lost.</span></span> <span data-ttu-id="d6607-106">Aby zachować stan poza okres istnienia kontenera, można zainstalować woluminu z magazynu zewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="d6607-106">To persist state beyond the lifetime of the container, you must mount a volume from an external store.</span></span> <span data-ttu-id="d6607-107">W tym artykule przedstawiono sposób instalacji udziału plików na platformę Azure do użycia z wystąpień kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d6607-107">This article shows how to mount an Azure file share for use with Azure Container Instances.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="d6607-108">Tworzenie udziału plików na platformę Azure</span><span class="sxs-lookup"><span data-stu-id="d6607-108">Create an Azure file share</span></span>

<span data-ttu-id="d6607-109">Przed rozpoczęciem korzystania z udziału plików na platformę Azure z wystąpień kontenera platformy Azure, należy utworzyć ją.</span><span class="sxs-lookup"><span data-stu-id="d6607-109">Before using an Azure file share with Azure Container Instances, you must create it.</span></span> <span data-ttu-id="d6607-110">Uruchom następujący skrypt, aby utworzyć konto magazynu do obsługi udziałów plików i udziału.</span><span class="sxs-lookup"><span data-stu-id="d6607-110">Run the following script to create a storage account to host the file share and the share itself.</span></span> <span data-ttu-id="d6607-111">Zauważ, że nazwa konta magazynu musi być unikatowe globalnie, więc skrypt dodaje losowych wartości do podstawowej ciąg.</span><span class="sxs-lookup"><span data-stu-id="d6607-111">Note that the storage account name must be globally unique, so the script adds a random value to the base string.</span></span>

```azurecli-interactive
# Change these four parameters
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
ACI_PERS_RESOURCE_GROUP=myResourceGroup
ACI_PERS_LOCATION=eastus
ACI_PERS_SHARE_NAME=acishare

# Create the storage account with the parameters
az storage account create -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -l $ACI_PERS_LOCATION --sku Standard_LRS

# Export the connection string as an environment variable, this is used when creating the Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -o tsv`

# Create the share
az storage share create -n $ACI_PERS_SHARE_NAME
```

## <a name="acquire-storage-account-access-details"></a><span data-ttu-id="d6607-112">Możliwość nabycia szczegółów dostępu do konta magazynu</span><span class="sxs-lookup"><span data-stu-id="d6607-112">Acquire storage account access details</span></span>

<span data-ttu-id="d6607-113">Aby zainstalować udział plików na platformę Azure jako wolumin w wystąpień kontenera platformy Azure, potrzebne są trzy wartości: Nazwa konta magazynu, nazwa udziału i klucz dostępu do magazynu.</span><span class="sxs-lookup"><span data-stu-id="d6607-113">To mount an Azure file share as a volume in Azure Container Instances, you need three values: the storage account name, the share name, and the storage access key.</span></span> 

<span data-ttu-id="d6607-114">Jeśli używany jest skrypt powyżej, nazwa konta magazynu został utworzony z losowych wartości na końcu.</span><span class="sxs-lookup"><span data-stu-id="d6607-114">If you used the script above, the storage account name was created with a random value at the end.</span></span> <span data-ttu-id="d6607-115">Aby sprawdzić, ostatni ciąg (w tym losowe części), użyj następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="d6607-115">To query the final string (including the random portion), use the following commands:</span></span>

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

<span data-ttu-id="d6607-116">Nazwa udziału jest już znany (jest *acishare* w skrypcie powyżej), więc wszystko, że pozostaje jest klucz konta magazynu, który można znaleźć przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d6607-116">The share name is already known (it is *acishare* in the script above), so all that remains is the storage account key, which can be found using the following command:</span></span>

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a><span data-ttu-id="d6607-117">Przechowuj szczegóły dostępu konta magazynu z usługi Azure key vault</span><span class="sxs-lookup"><span data-stu-id="d6607-117">Store storage account access details with Azure key vault</span></span>

<span data-ttu-id="d6607-118">Klucze konta magazynu ochrony dostępu do danych, dlatego zalecamy przechowywanie ich w magazynie kluczy Azure.</span><span class="sxs-lookup"><span data-stu-id="d6607-118">Storage account keys protect access to your data, so we recommend storing them in an Azure key vault.</span></span> 

<span data-ttu-id="d6607-119">Utwórz magazyn kluczy z wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="d6607-119">Create a key vault with the Azure CLI:</span></span>

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

<span data-ttu-id="d6607-120">`enabled-for-template-deployment` Przełącznika umożliwia usługi Azure Resource Manager do kluczy tajnych ściągnięcia z magazynu kluczy w czasie wdrażania.</span><span class="sxs-lookup"><span data-stu-id="d6607-120">The `enabled-for-template-deployment` switch allows Azure Resource Manager to pull secrets from your key vault at deployment time.</span></span>

<span data-ttu-id="d6607-121">Magazyn klucz konta magazynu, jako nowego klucza tajnego w magazynie kluczy:</span><span class="sxs-lookup"><span data-stu-id="d6607-121">Store the storage account key as a new secret in the key vault:</span></span>

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-the-volume"></a><span data-ttu-id="d6607-122">Zainstalowania woluminu</span><span class="sxs-lookup"><span data-stu-id="d6607-122">Mount the volume</span></span>

<span data-ttu-id="d6607-123">Instalowanie udziału plików na platformę Azure jako wolumin w kontenerze jest procesem dwuetapowym.</span><span class="sxs-lookup"><span data-stu-id="d6607-123">Mounting an Azure file share as a volume in a container is a two-step process.</span></span> <span data-ttu-id="d6607-124">Najpierw podaj szczegóły udziału w ramach definiowania grupy kontenerów, a następnie można określić sposób wolumin zainstalowany w co najmniej jeden z kontenerów w grupie.</span><span class="sxs-lookup"><span data-stu-id="d6607-124">First, you provide the details of the share as part of defining the container group, then you specify how you want the volume mounted within one or more of the containers in the group.</span></span>

<span data-ttu-id="d6607-125">Aby zdefiniować woluminy mają być dostępne na potrzeby instalacji, należy dodać `volumes` tablicy do kontenera grupy definicji szablonu usługi Azure Resource Manager, a następnie odwoływać je w definicji poszczególnych kontenerów.</span><span class="sxs-lookup"><span data-stu-id="d6607-125">To define the volumes you want to make available for mounting, add a `volumes` array to the container group definition in the Azure Resource Manager template, then reference them in the definition of the individual containers.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "type": "string"
    },
    "storageaccountkey": {
      "type": "securestring"
    }
  },
  "resources":[{
    "name": "hellofiles",
    "type": "Microsoft.ContainerInstance/containerGroups",
    "apiVersion": "2017-08-01-preview",
    "location": "[resourceGroup().location]",
    "properties": {
      "containers": [{
        "name": "hellofiles",
        "properties": {
          "image": "seanmckenna/aci-hellofiles",
          "resources": {
            "requests": {
              "cpu": 1,
              "memoryInGb": 1.5
            }
          },
          "ports": [{
            "port": 80
          }],
          "volumeMounts": [{
            "name": "myvolume",
            "mountPath": "/aci/logs/"
          }]
        }  
      }],
      "osType": "Linux",
      "ipAddress": {
        "type": "Public",
        "ports": [{
          "protocol": "tcp",
          "port": "80"
        }]
      },
      "volumes": [{
        "name": "myvolume",
        "azureFile": {
          "shareName": "acishare",
          "storageAccountName": "[parameters('storageaccountname')]",
          "storageAccountKey": "[parameters('storageaccountkey')]"
        }
      }]
    }
  }]
}
```

<span data-ttu-id="d6607-126">Szablon zawiera nazwy konta magazynu i klucz jako parametry, które można podać w pliku parametrów oddzielne.</span><span class="sxs-lookup"><span data-stu-id="d6607-126">The template includes the storage account name and key as parameters, which can be provided in a separate parameters file.</span></span> <span data-ttu-id="d6607-127">Aby wypełnić pliku parametrów, potrzebne są trzy wartości: Nazwa konta magazynu, identyfikator zasobu magazynu kluczy Azure, a nazwa klucza tajnego klucza magazynu używanego do przechowywania klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="d6607-127">To populate the parameters file, you will need three values: the storage account name, the resource ID of your Azure key vault, and the key vault secret name that you used to store the storage key.</span></span> <span data-ttu-id="d6607-128">Jeśli powyższe kroki zostały wykonane, możesz uzyskać tych wartości za pomocą następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="d6607-128">If you have followed previous steps, you can get these values with the following script:</span></span>

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

<span data-ttu-id="d6607-129">Wstaw wartości w pliku parametrów:</span><span class="sxs-lookup"><span data-stu-id="d6607-129">Insert the values into the parameters file:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "value": "<my_storage_account_name>"
    },    
   "storageaccountkey": {
      "reference": {
        "keyVault": {
          "id": "<my_keyvault_id>"
        },
        "secretName": "<my_storage_account_key_secret_name>"
      }
    }
  }
}
```

## <a name="deploy-the-container-and-manage-files"></a><span data-ttu-id="d6607-130">Wdrażanie kontenera i zarządzanie plikami</span><span class="sxs-lookup"><span data-stu-id="d6607-130">Deploy the container and manage files</span></span>

<span data-ttu-id="d6607-131">Z szablonem zdefiniowane można utworzyć kontenera i zainstalować jego woluminu przy użyciu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d6607-131">With the template defined, you can create the container and mount its volume using the Azure CLI.</span></span> <span data-ttu-id="d6607-132">Przy założeniu, że plik szablon ma nazwę *azuredeploy.json* i pliku parametrów o nazwie *azuredeploy.parameters.json*, a następnie w wierszu polecenia jest:</span><span class="sxs-lookup"><span data-stu-id="d6607-132">Assuming that the template file is named *azuredeploy.json* and that the parameters file is named *azuredeploy.parameters.json*, then the command line is:</span></span>

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

<span data-ttu-id="d6607-133">Po uruchomieniu kontenera, korzystając z aplikacji sieci web proste wdrażane za pomocą **seanmckenna/aci-hellofiles** obrazu, aby zarządzanie plikami w udziale plików na platformę Azure w określonej ścieżce instalacji.</span><span class="sxs-lookup"><span data-stu-id="d6607-133">Once the container starts up, you can use the simple web app deployed via the **seanmckenna/aci-hellofiles** image, to the manage files in the Azure file share at the mount path that you specified.</span></span> <span data-ttu-id="d6607-134">Uzyskaj adres ip dla aplikacji sieci web za pomocą następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="d6607-134">Obtain the ip address for the web app via the following:</span></span>

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

<span data-ttu-id="d6607-135">Można użyć narzędzia, takiego jak [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com) można pobrać i zbadać writen plików do udziału plików.</span><span class="sxs-lookup"><span data-stu-id="d6607-135">You can use a tool like the [Microsoft Azure Storage Explorer](http://storageexplorer.com) to retrieve and inspect the file writen to the file share.</span></span>

>[!NOTE]
> <span data-ttu-id="d6607-136">Aby dowiedzieć się więcej o korzystaniu z szablonów usługi Azure Resource Manager, pliki parametrów i wdrożenie z wiersza polecenia platformy Azure, zobacz [wdrożenie zasobów z szablonami usługi Resource Manager i interfejsu wiersza polecenia Azure](../azure-resource-manager/resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d6607-136">To learn more about using Azure Resource Manager templates, parameter files, and deploying with the Azure CLI, see [Deploy resources with Resource Manager templates and Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6607-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d6607-137">Next steps</span></span>

- <span data-ttu-id="d6607-138">Wdrażanie dla Twojego pierwszego kontenera za pomocą wystąpień kontenera Azure [szybki start](container-instances-quickstart.md)</span><span class="sxs-lookup"><span data-stu-id="d6607-138">Deploy for your first container using the Azure Container Instances [quick start](container-instances-quickstart.md)</span></span>
- <span data-ttu-id="d6607-139">Dowiedz się więcej o [relacja między wystąpieniami kontenera Azure i kontener orchestrators](container-instances-orchestrator-relationship.md)</span><span class="sxs-lookup"><span data-stu-id="d6607-139">Learn about the [relationship between Azure Container Instances and container orchestrators](container-instances-orchestrator-relationship.md)</span></span>
