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
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a>Instalowanie udziału plików na platformę Azure z wystąpień kontenera platformy Azure

Domyślnie bezstanowe są wystąpień kontenera platformy Azure. Kontener hello ulega awarii lub przestanie, wszystkie jego stan zostanie utracone. toopersist stanu poza okres istnienia hello hello kontenera, należy zainstalować wolumin z magazynu zewnętrznego. W tym artykule opisano, jak toomount plików na platformę Azure udostępnić do użytku z wystąpień kontenera platformy Azure.

## <a name="create-an-azure-file-share"></a>Tworzenie udziału plików na platformę Azure

Przed rozpoczęciem korzystania z udziału plików na platformę Azure z wystąpień kontenera platformy Azure, należy utworzyć ją. Uruchom hello następującego skryptu toocreate udział plików hello toohost konta magazynu i hello udostępnianie sam. Należy pamiętać, że czy nazwa konta magazynu hello musi być unikatowe globalnie, dlatego hello skrypt dodaje ciągu podstawowej toohello losowych wartości.

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

## <a name="acquire-storage-account-access-details"></a>Możliwość nabycia szczegółów dostępu do konta magazynu

toomount udział plików Azure jako wolumin w wystąpień kontenera platformy Azure, należy trzech wartości: hello nazwy konta magazynu, nazwa udziału hello i klucz dostępu do magazynu hello. 

Jeśli używany jest skrypt hello powyżej, nazwa konta magazynu hello utworzono za pomocą losowych wartości na końcu hello. Ostatni ciąg hello tooquery (takie jak hello losowe części), użyj hello następującego polecenia:

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

Witaj nazwa udziału jest już znany (jest *acishare* w skrypcie hello powyżej), więc hello pozostaje rzeczą klucz konta magazynu hello, który można znaleźć przy użyciu następującego polecenia:

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a>Przechowuj szczegóły dostępu konta magazynu z usługi Azure key vault

Klucze konta magazynu ochrony dostępu do danych tooyour, dlatego zalecamy przechowywanie ich w magazynie kluczy Azure. 

Utwórz magazyn kluczy o hello wiersza polecenia platformy Azure:

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

Witaj `enabled-for-template-deployment` przełącznika umożliwia Azure Resource Manager toopull kluczy tajnych z magazynu kluczy w czasie wdrażania.

Przechowywanie klucza konta magazynu hello jako nowego klucza tajnego w magazynie kluczy hello:

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-hello-volume"></a>Zainstalować hello woluminu

Instalowanie udziału plików na platformę Azure jako wolumin w kontenerze jest procesem dwuetapowym. Najpierw należy szczegółowo hello hello udziału w ramach definiowania grupy kontenerów hello, a następnie określ, jak mają być zainstalowane w co najmniej jeden z kontenerów hello w grupie hello woluminu hello.

woluminy hello toodefine mają toomake dostępne do zamontowania, Dodaj `volumes` tablicy definicja grupy kontenera toohello hello szablonu usługi Azure Resource Manager, a następnie odwoływać je w definicji hello hello poszczególnych kontenerów.

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

Szablon Hello zawiera nazwy konta magazynu hello i klucz jako parametry, które można podać w pliku parametrów oddzielne. plik parametrów hello toopopulate, konieczne będzie trzy wartości: hello nazwy konta magazynu, hello identyfikator zasobu magazynu kluczy Azure i hello nazwa klucza tajnego klucza magazynu użytą toostore hello magazynu kluczy. Jeśli powyższe kroki zostały wykonane, te wartości można uzyskać z hello następującego skryptu:

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

Wstaw hello wartości w pliku parametrów hello:

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

## <a name="deploy-hello-container-and-manage-files"></a>Wdrażanie kontenera hello i zarządzanie plikami

Zdefiniowanego szablonu hello możesz utworzyć kontener hello i zainstalować jej woluminu przy użyciu hello wiersza polecenia platformy Azure. Przy założeniu, że hello pliku szablonu nosi nazwę *azuredeploy.json* i nosi nazwę tego pliku parametrów hello *azuredeploy.parameters.json*, jest hello wiersza polecenia:

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

Po kontenera hello jest uruchamiany, możesz użyć aplikacji prostego powitania wdrażane za pomocą hello **seanmckenna/aci-hellofiles** obrazu, toohello zarządzania plikami w udziale plików na platformę Azure hello na ścieżkę instalacji hello określony. Uzyskaj adres ip hello hello aplikacji sieci web za pomocą następujących hello:

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

Można użyć narzędzia, takiego jak hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com) tooretrieve i zbadać udziału plików toohello hello pliku writen.

>[!NOTE]
> toolearn więcej informacji na temat przy użyciu szablonów usługi Azure Resource Manager, pliki parametrów i wdrażanie z hello wiersza polecenia platformy Azure, zobacz [wdrożenie zasobów z szablonami usługi Resource Manager i interfejsu wiersza polecenia Azure](../azure-resource-manager/resource-group-template-deploy-cli.md).

## <a name="next-steps"></a>Następne kroki

- Wdrażanie dla Twojego pierwszego kontenera za pomocą wystąpień kontenera Azure hello [szybki start](container-instances-quickstart.md)
- Dowiedz się więcej o hello [relacja między wystąpieniami kontenera Azure i kontener orchestrators](container-instances-orchestrator-relationship.md)
