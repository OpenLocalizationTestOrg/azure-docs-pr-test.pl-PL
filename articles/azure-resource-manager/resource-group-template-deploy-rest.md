---
title: "aaaDeploy zasobów przy użyciu interfejsu API REST i szablon | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure Resource Manager i interfejsu REST API usługi Resource Manager toodeploy tooAzure zasobów. zasoby Hello są definiowane w szablonie usługi Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 1d8fbd4c-78b0-425b-ba76-f2b7fd260b45
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: 347ad3bdb604429e7291297d448688204af69b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a>Deploy resources with Resource Manager templates and Resource Manager REST API (Wdrażanie zasobów za pomocą szablonów usługi Resource Manager i interfejsu API REST usługi Resource Manager)
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Interfejs wiersza polecenia platformy Azure](resource-group-template-deploy-cli.md)
> * [Portal](resource-group-template-deploy-portal.md)
> * [Interfejs API REST](resource-group-template-deploy-rest.md)
> 
> 

W tym artykule opisano, jak toouse hello interfejsu REST API usługi Resource Manager z toodeploy szablonów usługi Resource Manager tooAzure Twojego zasobów.  

> [!TIP]
> Aby uzyskać pomoc dotyczącą debugowania — błąd podczas wdrażania zobacz:
> 
> * [Wyświetl operacje wdrażania](resource-manager-deployment-operations.md) toolearn uzyskiwanie informacje ułatwiające rozwiązywanie problemów z błędu
> * [Rozwiąż typowe błędy podczas wdrażania tooAzure zasobów z usługi Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn jak tooresolve typowe błędy wdrażania
> 
> 

Szablon może być lokalny plik lub pliku zewnętrznego, który jest dostępny za pomocą identyfikatora URI. Gdy w szablonie znajduje się na koncie magazynu, można ograniczyć dostęp toohello szablonu, a także dostarczają token sygnatury dostępu Współdzielonego dostępu współdzielonego podczas wdrażania.

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a>Wdrażanie z hello interfejsu API REST
1. Ustaw [wspólnych parametrów i nagłówki](https://docs.microsoft.com/rest/api/index), łącznie z tokenami uwierzytelniania.
2. Jeśli nie masz istniejącej grupy zasobów, należy utworzyć grupę zasobów. Podaj Twojego Identyfikatora subskrypcji, nazwę hello hello nowe, lokalizacji i grupy zasobów potrzebnym do rozwiązania. Aby uzyskać więcej informacji, zobacz [Utwórz grupę zasobów](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. Sprawdzanie poprawności wdrożenia przed wykonaniem ją, uruchamiając hello [weryfikowanie wdrożenia szablonu](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operacji. Podczas testowania wdrożenia hello, należy podać parametry, dokładnie tak jak w przypadku wykonywania hello wdrożenia (pokazano w następnym kroku hello).
4. Tworzenie wdrożenia. Podaj identyfikator subskrypcji, hello nazwę grupy zasobów hello nazwa hello hello wdrożenia i szablon tooyour łącza. Informacji o pliku szablonu hello znajduje się w temacie [pliku parametrów](#parameter-file). Aby uzyskać więcej informacji na temat toocreate interfejsu API REST hello grupę zasobów, zobacz [Utwórz wdrożenie szablonu](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate). Powiadomienie hello **tryb** ustawiono zbyt**przyrostowe**. Ustaw toorun ukończenia wdrożenia, **tryb** za**Complete**. Należy zachować ostrożność podczas w trybie hello pełne, jak mogą przypadkowo usunięte zasoby, które nie znajdują się w szablonie.
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
          <common headers>
          {
            "properties": {
              "templateLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
                "contentVersion": "1.0.0.0"
              },
              "mode": "Incremental",
              "parametersLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
                "contentVersion": "1.0.0.0"
              }
            }
          }
   
      Toolog zawartości odpowiedzi i żądania zawartości, należy włączyć **debugSetting** w żądaniu hello.
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      Można skonfigurować sieci toouse konta magazynu tokenu sygnatury dostępu Współdzielonego dostępu współdzielonego. Aby uzyskać więcej informacji, zobacz [Delegowanie dostępu z sygnaturą dostępu współdzielonego](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).
5. Pobierz stan hello hello szablonu wdrożenia. Aby uzyskać więcej informacji, zobacz [uzyskać informacje na temat wdrażania szablonu](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a>Plik parametrów

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a>Następne kroki
* toolearn dotyczące obsługi operacji asynchronicznych REST, zobacz [śledzić operacje asynchroniczne Azure](resource-manager-async-operations.md).
* Na przykład wdrażania zasobów za pomocą biblioteki klienta .NET hello zobacz [wdrażanie zasobów przy użyciu bibliotek .NET oraz szablonu](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Parametry toodefine w szablonie, zobacz [tworzenia szablonów](resource-group-authoring-templates.md#parameters).
* Aby uzyskać wskazówki dotyczące wdrażania środowiska toodifferent rozwiązania, zobacz [środowisk projektowania i testowania na platformie Microsoft Azure](solution-dev-test-environments.md).
* Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).

