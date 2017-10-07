---
title: "aaaAzure dostawców zasobów i typów zasobów | Dokumentacja firmy Microsoft"
description: "Zawiera opis dostawcy zasobów hello obsługujących usługi Resource Manager, schematów i dostępne wersje interfejsu API i regiony hello może obsługiwać zasoby hello."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 3c7a6fe4-371a-40da-9ebe-b574f583305b
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 23db1d3808a20166f3b44ec801e1bcc46fbb9bd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resource-providers-and-types"></a>Dostawcy zasobów i typów

W przypadku wdrażania zasobów, należy często tooretrieve informacji na temat hello dostawców zasobów i typów. W tym artykule dowiesz się:

* Wyświetlanie wszystkich dostawców zasobów na platformie Azure
* Sprawdzaj stan rejestracji dostawcy zasobów
* Rejestrowanie dostawcy zasobów
* Wyświetlanie typów zasobów dla dostawcy zasobów
* Prawidłowe lokalizacje widoku dla typu zasobu
* Widok prawidłowych wersji interfejsu API dla typu zasobu

Można wykonywać następujące czynności, za pośrednictwem portalu hello, programu PowerShell lub wiersza polecenia platformy Azure.

## <a name="powershell"></a>PowerShell

toosee wszystkich dostawców zasobów platformy Azure i hello stan rejestracji subskrypcji, należy użyć:

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

Która zwróci wyniki podobne do:

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

Rejestrowanie dostawcy zasobów umożliwia skonfigurowanie toowork Twojej subskrypcji hello dostawcy zasobów. zakres Hello rejestracji jest zawsze hello subskrypcji. Domyślnie automatycznie zarejestrowano wielu dostawców zasobów. Jednak może być konieczne toomanually zarejestrować niektórzy dostawcy zasobów. tooregister dostawcy zasobów, musi mieć uprawnienie tooperform hello `/register/action` operacji hello dostawcy zasobów. Ta operacja jest dołączony do hello współautora i ról właściciela.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

Która zwróci wyniki podobne do:

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

Nie można wyrejestrować dostawcy zasobów, gdy nadal masz typów zasobów z tego dostawcy zasobów w ramach subskrypcji.

informacje toosee dla dostawcy określonego zasobu, użyj:

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

Która zwróci wyniki podobne do:

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

typy zasobów hello toosee dostawcy zasobów, należy użyć:

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

Polecenie to zwraca:

```powershell
batchAccounts
operations
locations
locations/quotas
```

wersja interfejsu API Hello odpowiada tooa wersji operacji interfejsu API REST, które są wydawane przez dostawcę zasobów hello. Jak dostawca zasobów umożliwia korzystanie z nowych funkcji, zwalnia nowej wersji hello interfejsu API REST. 

Użyj tooget hello dostępne wersje interfejsu API dla typu zasobu:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

Polecenie to zwraca:

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

Menedżer zasobów jest obsługiwane we wszystkich regionach, ale hello zasoby, które można wdrożyć mogą nie być obsługiwane we wszystkich regionach. Ponadto może być mają zastosowanie ograniczenia dotyczące subskrypcji, które uniemożliwić korzystanie z niektórych regionach, które obsługują hello zasobów. 

Użyj tooget hello obsługiwane lokalizacje dla typu zasobu.

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

Polecenie to zwraca:

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure
toosee wszystkich dostawców zasobów platformy Azure i hello stan rejestracji subskrypcji, należy użyć:

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

Która zwróci wyniki podobne do:

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

Rejestrowanie dostawcy zasobów umożliwia skonfigurowanie toowork Twojej subskrypcji hello dostawcy zasobów. zakres Hello rejestracji jest zawsze hello subskrypcji. Domyślnie automatycznie zarejestrowano wielu dostawców zasobów. Jednak może być konieczne toomanually zarejestrować niektórzy dostawcy zasobów. tooregister dostawcy zasobów, musi mieć uprawnienie tooperform hello `/register/action` operacji hello dostawcy zasobów. Ta operacja jest dołączony do hello współautora i ról właściciela.

```azurecli
az provider register --namespace Microsoft.Batch
```

Która zwraca komunikat do tej rejestracji jest w toku.

Nie można wyrejestrować dostawcy zasobów, gdy nadal masz typów zasobów z tego dostawcy zasobów w ramach subskrypcji.

informacje toosee dla dostawcy określonego zasobu, użyj:

```azurecli
az provider show --namespace Microsoft.Batch
```

Która zwróci wyniki podobne do:

```azurecli
{
    "id": "/subscriptions/####-####/providers/Microsoft.Batch",
    "namespace": "Microsoft.Batch",
    "registrationsState": "Registering",
    "resourceTypes:" [
        ...
    ]
}
```

typy zasobów hello toosee dostawcy zasobów, należy użyć:

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

Polecenie to zwraca:

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

wersja interfejsu API Hello odpowiada tooa wersji operacji interfejsu API REST, które są wydawane przez dostawcę zasobów hello. Jak dostawca zasobów umożliwia korzystanie z nowych funkcji, zwalnia nowej wersji hello interfejsu API REST. 

Użyj tooget hello dostępne wersje interfejsu API dla typu zasobu:

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

Polecenie to zwraca:

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

Menedżer zasobów jest obsługiwane we wszystkich regionach, ale hello zasoby, które można wdrożyć mogą nie być obsługiwane we wszystkich regionach. Ponadto może być mają zastosowanie ograniczenia dotyczące subskrypcji, które uniemożliwić korzystanie z niektórych regionach, które obsługują hello zasobów. 

Użyj tooget hello obsługiwane lokalizacje dla typu zasobu.

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

Polecenie to zwraca:

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a>Portal

Wybierz wszystkich dostawców zasobów platformy Azure i hello stanu rejestracji subskrypcji toosee **subskrypcje**.

![Wybierz subskrypcje](./media/resource-manager-supported-services/select-subscriptions.png)

Wybierz hello tooview subskrypcji.

![Określ subskrypcję](./media/resource-manager-supported-services/subscription.png)

Wybierz **dostawców zasobów** i wyświetlanie hello listy dostępnych dostawców zasobów.

![Pokaż dostawców zasobów](./media/resource-manager-supported-services/show-resource-providers.png)

Rejestrowanie dostawcy zasobów umożliwia skonfigurowanie toowork Twojej subskrypcji hello dostawcy zasobów. zakres Hello rejestracji jest zawsze hello subskrypcji. Domyślnie automatycznie zarejestrowano wielu dostawców zasobów. Jednak może być konieczne toomanually zarejestrować niektórzy dostawcy zasobów. tooregister dostawcy zasobów, musi mieć uprawnienie tooperform hello `/register/action` operacji hello dostawcy zasobów. Ta operacja jest dołączony do hello współautora i ról właściciela. Wybierz tooregister dostawcę zasobów **zarejestrować**.

![Rejestrowanie dostawcy zasobów](./media/resource-manager-supported-services/register-provider.png)

Nie można wyrejestrować dostawcy zasobów, gdy nadal masz typów zasobów z tego dostawcy zasobów w ramach subskrypcji.

Wybierz informacje toosee dla dostawcy określonego zasobu, **więcej usług**.

![Wybierz więcej usług](./media/resource-manager-supported-services/more-services.png)

Wyszukaj **Eksploratora zasobów** i wybierz ją z hello dostępnych opcji.

![Wybierz Eksploratora zasobów](./media/resource-manager-supported-services/select-resource-explorer.png)

Wybierz **dostawców**.

![Wybierz dostawców](./media/resource-manager-supported-services/select-providers.png)

Dostawca zasobów wybierz hello i zasobu typu, które mają tooview.

![Wybierz typ zasobu](./media/resource-manager-supported-services/select-resource-type.png)

Menedżer zasobów jest obsługiwane we wszystkich regionach, ale hello zasoby, które można wdrożyć mogą nie być obsługiwane we wszystkich regionach. Ponadto może być mają zastosowanie ograniczenia dotyczące subskrypcji, które uniemożliwić korzystanie z niektórych regionach, które obsługują hello zasobów. Eksplorator zasobów Hello Wyświetla prawidłowe lokalizacje dla typu zasobu hello.

![Pokaż lokalizacje](./media/resource-manager-supported-services/show-locations.png)

wersja interfejsu API Hello odpowiada tooa wersji operacji interfejsu API REST, które są wydawane przez dostawcę zasobów hello. Jak dostawca zasobów umożliwia korzystanie z nowych funkcji, zwalnia nowej wersji hello interfejsu API REST. Eksplorator zasobów Hello Wyświetla prawidłowych wersji interfejsu API dla typu zasobu hello.

![Pokaż wersje interfejsu API](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a>Następne kroki
* toolearn o tworzeniu szablonów usługi Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* toolearn dotyczących wdrażania zasobów, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).
* operacje hello tooview dla dostawcy zasobów, zobacz [interfejsu API REST Azure](/rest/api/).

