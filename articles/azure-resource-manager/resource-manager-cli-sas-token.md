---
title: "aaaDeploy szablonu platformy Azure z tokenu sygnatury dostępu Współdzielonego i interfejsu wiersza polecenia Azure | Dokumentacja firmy Microsoft"
description: "Usługi Azure Resource Manager i interfejsu wiersza polecenia Azure tooAzure zasobów toodeploy z szablonu, który jest chroniony za pomocą tokenu sygnatury dostępu Współdzielonego."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: 59c64616d6e1f5e456d88a72854d0ed99e1bdc0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-cli"></a>Wdrażanie prywatnej szablonu usługi Resource Manager z tokenu sygnatury dostępu Współdzielonego i wiersza polecenia platformy Azure

Gdy w szablonie znajduje się na koncie magazynu, można ograniczyć dostęp toohello szablonu, a także dostarczają token sygnatury dostępu Współdzielonego dostępu współdzielonego podczas wdrażania. W tym temacie opisano sposób toouse programu Azure PowerShell z tooprovide szablonów usługi Resource Manager tokenu sygnatury dostępu Współdzielonego, podczas wdrażania. 

## <a name="add-private-template-toostorage-account"></a>Dodaj konto toostorage prywatnej szablonu

Można dodać konta magazynu tooa szablony, a następnie połącz toothem podczas wdrażania z tokenem sygnatury dostępu Współdzielonego.

> [!IMPORTANT]
> Wykonując poniższe kroki hello hello obiektu blob zawierającego szablon hello jest właściciela konta hello tooonly dostępny. Podczas tworzenia tokenu SAS obiektu blob hello hello obiektu blob jest jednak dostępne tooanyone z tym identyfikatorem URI. Inny użytkownik przechwytuje hello identyfikatora URI, który jest możliwe tooaccess hello szablonu. Za pomocą tokenu sygnatury dostępu Współdzielonego jest dobrym sposobem ograniczenia dostępu tooyour szablonów, ale nie może zawierać dane poufne, takie jak hasła, bezpośrednio w szablonie hello.
> 
> 

Witaj poniższy przykład ustawia kontener konta magazynu prywatnych i przekazuje szablonu:
   
```azurecli
az group create --name "ManageGroup" --location "South Central US"
az storage account create \
    --resource-group ManageGroup \
    --location "South Central US" \
    --sku Standard_LRS \
    --kind Storage \
    --name {your-unique-name}
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
az storage container create \
    --name templates \
    --public-access Off \
    --connection-string $connection
az storage blob upload \
    --container-name templates \
    --file vmlinux.json \
    --name vmlinux.json \
    --connection-string $connection
```

### <a name="provide-sas-token-during-deployment"></a>Podaj token sygnatury dostępu Współdzielonego podczas wdrażania
toodeploy prywatnej szablonu na koncie magazynu wygenerowania tokenu sygnatury dostępu Współdzielonego i uwzględnić go w hello URI hello szablonu. Ustaw tooallow czas wygaśnięcia hello wdrożenia hello toocomplete wystarczająco dużo czasu.
   
```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
token=$(az storage blob generate-sas \
    --container-name templates \
    --name vmlinux.json \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name vmlinux.json \
    --output tsv \
    --connection-string $connection)
az group deployment create --resource-group ExampleGroup --template-uri $url?$token
```

Na przykład za pomocą tokenu sygnatury dostępu Współdzielonego przy użyciu szablonów połączonych, zobacz [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).

## <a name="next-steps"></a>Następne kroki
* Wprowadzenie toodeploying szablonów, zobacz [wdrażanie zasobów przy użyciu szablonów usługi Resource Manager i programu Azure PowerShell](resource-group-template-deploy-cli.md).
* Zakończenie przykładowego skryptu, który wdraża szablonu, zobacz [skryptu szablonu wdrażania Menedżera zasobów](resource-manager-samples-cli-deploy.md)
* Parametry toodefine w szablonie, zobacz [tworzenia szablonów](resource-group-authoring-templates.md#parameters).
* Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).
