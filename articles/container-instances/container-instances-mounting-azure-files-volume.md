---
title: "aaaMounting woluminu plików Azure w wystąpień kontenera platformy Azure"
description: "Dowiedz się, jak toomount platformy Azure pliki stanu toopersist woluminu z wystąpień kontenera platformy Azure"
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
ms.openlocfilehash: d87215e06d5e5af40bfebcad17768ee45ccabbb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a><span data-ttu-id="a2ef1-103">Instalowanie udziału plików na platformę Azure z wystąpień kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a2ef1-103">Mounting an Azure file share with Azure Container Instances</span></span>

<span data-ttu-id="a2ef1-104">Domyślnie bezstanowe są wystąpień kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a2ef1-104">By default, Azure Container Instances are stateless.</span></span> <span data-ttu-id="a2ef1-105">Kontener hello ulega awarii lub przestanie, wszystkie jego stan zostanie utracone.</span><span class="sxs-lookup"><span data-stu-id="a2ef1-105">If hello container crashes or stops, all of its state is lost.</span></span> <span data-ttu-id="a2ef1-106">toopersist stanu poza okres istnienia hello hello kontenera, należy zainstalować wolumin z magazynu zewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="a2ef1-106">toopersist state beyond hello lifetime of hello container, you must mount a volume from an external store.</span></span> <span data-ttu-id="a2ef1-107">W tym artykule opisano, jak toomount plików na platformę Azure udostępnić do użytku z wystąpień kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a2ef1-107">This article shows how toomount an Azure file share for use with Azure Container Instances.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="a2ef1-108">Tworzenie udziału plików na platformę Azure</span><span class="sxs-lookup"><span data-stu-id="a2ef1-108">Create an Azure file share</span></span>

<span data-ttu-id="a2ef1-109">Przed rozpoczęciem korzystania z udziału plików na platformę Azure z wystąpień kontenera platformy Azure, należy utworzyć ją.</span><span class="sxs-lookup"><span data-stu-id="a2ef1-109">Before using an Azure file share with Azure Container Instances, you must create it.</span></span> <span data-ttu-id="a2ef1-110">Uruchom hello następującego skryptu toocreate udział plików hello toohost konta magazynu i hello udostępnianie sam.</span><span class="sxs-lookup"><span data-stu-id="a2ef1-110">Run hello following script toocreate a storage account toohost hello file share and hello share itself.</span></span> <span data-ttu-id="a2ef1-111">Należy pamiętać, że czy nazwa konta magazynu hello musi być unikatowe globalnie, dlatego hello skrypt dodaje ciągu podstawowej toohello losowych wartości.</span><span class="sxs-lookup"><span data-stu-id="a2ef1-111">Note that hello storage account name must be globally unique, so hello script adds a random value toohello base string.</span></span>

```azurecli-interactive
# Change these four parameters
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
ACI_PERS_RESOURCE_GROUP=myResourceGroup
ACI_PERS_LOCATION=eastus
ACI_PERS_SHARE_NAME=acishare

# Create hello storage account with hello parameters
az storage account create -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -l $ACI_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $ACI_PERS_SHARE_NAME
```

## <a name="acquire-storage-account-access-details"></a><span data-ttu-id="a2ef1-112">Możliwość nabycia szczegółów dostępu do konta magazynu</span><span class="sxs-lookup"><span data-stu-id="a2ef1-112">Acquire storage account access details</span></span>

<span data-ttu-id="a2ef1-113">toomount udział plików Azure jako wolumin w wystąpień kontenera platformy Azure, należy trzech wartości: hello nazwy konta magazynu, nazwa udziału hello i klucz dostępu do magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="a2ef1-113">toomount an Azure file share as a volume in Azure Container Instances, you need three values: hello storage account name, hello share name, and hello storage access key.</span></span> 

<span data-ttu-id="a2ef1-114">Jeśli używany jest skrypt hello powyżej, nazwa konta magazynu hello utworzono za pomocą losowych wartości na końcu hello.</span><span class="sxs-lookup"><span data-stu-id="a2ef1-114">If you used hello script above, hello storage account name was created with a random value at hello end.</span></span> <span data-ttu-id="a2ef1-115">Ostatni ciąg hello tooquery (takie jak hello losowe części), użyj hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a2ef1-115">tooquery hello final string (including hello random portion), use hello following commands:</span></span>

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

<span data-ttu-id="a2ef1-116">Witaj nazwa udziału jest już znany (jest *acishare* w skrypcie hello powyżej), więc hello pozostaje rzeczą klucz konta magazynu hello, który można znaleźć przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a2ef1-116">hello share name is already known (it is *acishare* in hello script above), so all that remains is hello storage account key, which can be found using hello following command:</span></span>

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a><span data-ttu-id="a2ef1-117">Przechowuj szczegóły dostępu konta magazynu z usługi Azure key vault</span><span class="sxs-lookup"><span data-stu-id="a2ef1-117">Store storage account access details with Azure key vault</span></span>

<span data-ttu-id="a2ef1-118">Klucze konta magazynu ochrony dostępu do danych tooyour, dlatego zalecamy przechowywanie ich w magazynie kluczy Azure.</span><span class="sxs-lookup"><span data-stu-id="a2ef1-118">Storage account keys protect access tooyour data, so we recommend storing them in an Azure key vault.</span></span> 

<span data-ttu-id="a2ef1-119">Utwórz magazyn kluczy o hello wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="a2ef1-119">Create a key vault with hello Azure CLI:</span></span>

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

<span data-ttu-id="a2ef1-120">Witaj `enabled-for-template-deployment` przełącznika umożliwia Azure Resource Manager toopull kluczy tajnych z magazynu kluczy w czasie wdrażania.</span><span class="sxs-lookup"><span data-stu-id="a2ef1-120">hello `enabled-for-template-deployment` switch allows Azure Resource Manager toopull secrets from your key vault at deployment time.</span></span>

<span data-ttu-id="a2ef1-121">Przechowywanie klucza konta magazynu hello jako nowego klucza tajnego w magazynie kluczy hello:</span><span class="sxs-lookup"><span data-stu-id="a2ef1-121">Store hello storage account key as a new secret in hello key vault:</span></span>

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-hello-volume"></a><span data-ttu-id="a2ef1-122">Zainstalować hello woluminu</span><span class="sxs-lookup"><span data-stu-id="a2ef1-122">Mount hello volume</span></span>

<span data-ttu-id="a2ef1-123">Instalowanie udziału plików na platformę Azure jako wolumin w kontenerze jest procesem dwuetapowym.</span><span class="sxs-lookup"><span data-stu-id="a2ef1-123">Mounting an Azure file share as a volume in a container is a two-step process.</span></span> <span data-ttu-id="a2ef1-124">Najpierw należy szczegółowo hello hello udziału w ramach definiowania grupy kontenerów hello, a następnie określ, jak mają być zainstalowane w co najmniej jeden z kontenerów hello w grupie hello woluminu hello.</span><span class="sxs-lookup"><span data-stu-id="a2ef1-124">First, you provide hello details of hello share as part of defining hello container group, then you specify how you want hello volume mounted within one or more of hello containers in hello group.</span></span>

<span data-ttu-id="a2ef1-125">woluminy hello toodefine mają toomake dostępne do zamontowania, Dodaj `volumes` tablicy definicja grupy kontenera toohello hello szablonu usługi Azure Resource Manager, a następnie odwoływać je w definicji hello hello poszczególnych kontenerów.</span><span class="sxs-lookup"><span data-stu-id="a2ef1-125">toodefine hello volumes you want toomake available for mounting, add a `volumes` array toohello container group definition in hello Azure Resource Manager template, then reference them in hello definition of hello individual containers.</span></span>

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

<span data-ttu-id="a2ef1-126">Szablon Hello zawiera nazwy konta magazynu hello i klucz jako parametry, które można podać w pliku parametrów oddzielne.</span><span class="sxs-lookup"><span data-stu-id="a2ef1-126">hello template includes hello storage account name and key as parameters, which can be provided in a separate parameters file.</span></span> <span data-ttu-id="a2ef1-127">plik parametrów hello toopopulate, konieczne będzie trzy wartości: hello nazwy konta magazynu, hello identyfikator zasobu magazynu kluczy Azure i hello nazwa klucza tajnego klucza magazynu użytą toostore hello magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="a2ef1-127">toopopulate hello parameters file, you will need three values: hello storage account name, hello resource ID of your Azure key vault, and hello key vault secret name that you used toostore hello storage key.</span></span> <span data-ttu-id="a2ef1-128">Jeśli powyższe kroki zostały wykonane, te wartości można uzyskać z hello następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="a2ef1-128">If you have followed previous steps, you can get these values with hello following script:</span></span>

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

<span data-ttu-id="a2ef1-129">Wstaw hello wartości w pliku parametrów hello:</span><span class="sxs-lookup"><span data-stu-id="a2ef1-129">Insert hello values into hello parameters file:</span></span>

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

## <a name="deploy-hello-container-and-manage-files"></a><span data-ttu-id="a2ef1-130">Wdrażanie kontenera hello i zarządzanie plikami</span><span class="sxs-lookup"><span data-stu-id="a2ef1-130">Deploy hello container and manage files</span></span>

<span data-ttu-id="a2ef1-131">Zdefiniowanego szablonu hello możesz utworzyć kontener hello i zainstalować jej woluminu przy użyciu hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a2ef1-131">With hello template defined, you can create hello container and mount its volume using hello Azure CLI.</span></span> <span data-ttu-id="a2ef1-132">Przy założeniu, że hello pliku szablonu nosi nazwę *azuredeploy.json* i nosi nazwę tego pliku parametrów hello *azuredeploy.parameters.json*, jest hello wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="a2ef1-132">Assuming that hello template file is named *azuredeploy.json* and that hello parameters file is named *azuredeploy.parameters.json*, then hello command line is:</span></span>

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

<span data-ttu-id="a2ef1-133">Po kontenera hello jest uruchamiany, możesz użyć aplikacji prostego powitania wdrażane za pomocą hello **seanmckenna/aci-hellofiles** obrazu, toohello zarządzania plikami w udziale plików na platformę Azure hello na ścieżkę instalacji hello określony.</span><span class="sxs-lookup"><span data-stu-id="a2ef1-133">Once hello container starts up, you can use hello simple web app deployed via hello **seanmckenna/aci-hellofiles** image, toohello manage files in hello Azure file share at hello mount path that you specified.</span></span> <span data-ttu-id="a2ef1-134">Uzyskaj adres ip hello hello aplikacji sieci web za pomocą następujących hello:</span><span class="sxs-lookup"><span data-stu-id="a2ef1-134">Obtain hello ip address for hello web app via hello following:</span></span>

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

<span data-ttu-id="a2ef1-135">Można użyć narzędzia, takiego jak hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com) tooretrieve i zbadać udziału plików toohello hello pliku writen.</span><span class="sxs-lookup"><span data-stu-id="a2ef1-135">You can use a tool like hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) tooretrieve and inspect hello file writen toohello file share.</span></span>

>[!NOTE]
> <span data-ttu-id="a2ef1-136">toolearn więcej informacji na temat przy użyciu szablonów usługi Azure Resource Manager, pliki parametrów i wdrażanie z hello wiersza polecenia platformy Azure, zobacz [wdrożenie zasobów z szablonami usługi Resource Manager i interfejsu wiersza polecenia Azure](../azure-resource-manager/resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a2ef1-136">toolearn more about using Azure Resource Manager templates, parameter files, and deploying with hello Azure CLI, see [Deploy resources with Resource Manager templates and Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2ef1-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a2ef1-137">Next steps</span></span>

- <span data-ttu-id="a2ef1-138">Wdrażanie dla Twojego pierwszego kontenera za pomocą wystąpień kontenera Azure hello [szybki start](container-instances-quickstart.md)</span><span class="sxs-lookup"><span data-stu-id="a2ef1-138">Deploy for your first container using hello Azure Container Instances [quick start](container-instances-quickstart.md)</span></span>
- <span data-ttu-id="a2ef1-139">Dowiedz się więcej o hello [relacja między wystąpieniami kontenera Azure i kontener orchestrators](container-instances-orchestrator-relationship.md)</span><span class="sxs-lookup"><span data-stu-id="a2ef1-139">Learn about hello [relationship between Azure Container Instances and container orchestrators](container-instances-orchestrator-relationship.md)</span></span>
