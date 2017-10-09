---
title: "aaaDeploy szablonu platformy Azure z tokenu sygnatury dostępu Współdzielonego i programu PowerShell | Dokumentacja firmy Microsoft"
description: "Usługi Azure Resource Manager i programu Azure PowerShell tooAzure zasobów toodeploy z szablonu, który jest chroniony za pomocą tokenu sygnatury dostępu Współdzielonego."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: b95e096591d6213f8ef79235c8cd85705c4b79ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a>Wdrażanie prywatnej szablonu usługi Resource Manager z tokenu sygnatury dostępu Współdzielonego i programu Azure PowerShell

Gdy w szablonie znajduje się na koncie magazynu, można ograniczyć dostęp toohello szablonu, a także dostarczają token sygnatury dostępu Współdzielonego dostępu współdzielonego podczas wdrażania. W tym temacie opisano sposób toouse programu Azure PowerShell z tooprovide szablonów usługi Resource Manager tokenu sygnatury dostępu Współdzielonego, podczas wdrażania. 

## <a name="add-private-template-toostorage-account"></a>Dodaj konto toostorage prywatnej szablonu

Można dodać konta magazynu tooa szablony, a następnie połącz toothem podczas wdrażania z tokenem sygnatury dostępu Współdzielonego.

> [!IMPORTANT]
> Wykonując poniższe kroki hello hello obiektu blob zawierającego szablon hello jest właściciela konta hello tooonly dostępny. Podczas tworzenia tokenu SAS obiektu blob hello hello obiektu blob jest jednak dostępne tooanyone z tym identyfikatorem URI. Inny użytkownik przechwytuje hello identyfikatora URI, który jest możliwe tooaccess hello szablonu. Za pomocą tokenu sygnatury dostępu Współdzielonego jest dobrym sposobem ograniczenia dostępu tooyour szablonów, ale nie może zawierać dane poufne, takie jak hasła, bezpośrednio w szablonie hello.
> 
> 

Witaj poniższy przykład ustawia kontener konta magazynu prywatnych i przekazuje szablonu:
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a>Podaj token sygnatury dostępu Współdzielonego podczas wdrażania
toodeploy prywatnej szablonu na koncie magazynu wygenerowania tokenu sygnatury dostępu Współdzielonego i uwzględnić go w hello URI hello szablonu. Ustaw tooallow czas wygaśnięcia hello wdrożenia hello toocomplete wystarczająco dużo czasu.
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get hello URI with hello SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

Na przykład za pomocą tokenu sygnatury dostępu Współdzielonego przy użyciu szablonów połączonych, zobacz [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).


## <a name="next-steps"></a>Następne kroki
* Wprowadzenie toodeploying szablonów, zobacz [wdrażanie zasobów przy użyciu szablonów usługi Resource Manager i programu Azure PowerShell](resource-group-template-deploy.md).
* Zakończenie przykładowego skryptu, który wdraża szablonu, zobacz [skryptu szablonu wdrażania Menedżera zasobów](resource-manager-samples-powershell-deploy.md)
* Parametry toodefine w szablonie, zobacz [tworzenia szablonów](resource-group-authoring-templates.md#parameters).
* Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).

