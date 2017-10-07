---
title: "zmiany tooprevent zasobów Azure aaaLock | Dokumentacja firmy Microsoft"
description: "Uniemożliwić użytkownikom aktualizowanie lub usuwanie kluczowych zasobów platformy Azure, stosując blokady dla wszystkich użytkowników i ról."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 1f0d8911b2b129069bd2f01a9a4ec0a3cf700118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="lock-resources-tooprevent-unexpected-changes"></a>Blokowanie zasobów tooprevent nieoczekiwane zmiany 
Jako administrator może być konieczne toolock subskrypcji, grupy zasobów lub tooprevent zasobów innym użytkownikom w organizacji przypadkowo usuwanie i modyfikowanie kluczowych zasobów. Można ustawić poziomu blokady hello także**CanNotDelete** lub **tylko do odczytu**. 

* **CanNotDelete** oznacza, że autoryzowani użytkownicy mogą nadal odczytywać i modyfikować zasobu, ale nie można ich usunąć hello zasobu. 
* **Tylko do odczytu** oznacza, że autoryzowani użytkownicy mogą odczytywać zasobu, ale nie można usunąć lub zaktualizować zasobu hello. Zastosowanie Ta blokada jest podobne toorestricting wszystkich uprawnień użytkowników toohello uprawnienia przyznane przez hello **czytnika** roli. 

## <a name="how-locks-are-applied"></a>Sposób stosowania blokad

Po zastosowaniu blokady w zakresie nadrzędnym, wszystkie zasoby w tym zakresie dziedziczą hello tego samego blokady. Nawet zasoby, które później zostaną dodane Dziedzicz blokady hello hello nadrzędnej. Witaj najbardziej restrykcyjne blokady w dziedziczeniu hello pierwszeństwo.

W przeciwieństwie do kontroli dostępu opartej na rolach możesz użyć tooapply blokady zarządzania ograniczenie we wszystkich użytkowników i ról. toolearn o ustawianiu uprawnień dla użytkowników i ról, zobacz [kontroli dostępu opartej na roli Azure](../active-directory/role-based-access-control-configure.md).

Menedżer zasobów blokad zastosować tylko toooperations to zrobić w płaszczyźnie zarządzania hello, która składa się z operacji wysłany`https://management.azure.com`. Hello blokad nie ograniczają jak zasoby wykonywanie własnych funkcji. Zmiany zasobu jest ograniczony, ale operacje zasobów nie są ograniczone. Na przykład blokady w bazie danych SQL tylko do odczytu uniemożliwia usuwanie lub modyfikowanie hello bazy danych, ale nie uniemożliwiać tworzenie, aktualizowanie lub usuwanie danych hello bazy danych. Transakcje danych są dozwolone, ponieważ te operacje nie są wysyłane za`https://management.azure.com`.

Stosowanie **tylko do odczytu** może prowadzić toounexpected wyników, ponieważ niektóre operacje, które się wydawać odczytu operacje rzeczywiście wymagają dodatkowych czynności. Na przykład wprowadzenie **tylko do odczytu** blokady na koncie magazynu uniemożliwia wyświetlanie kluczy hello wszystkich użytkowników. Lista Hello operacji kluczy jest obsługiwana za pomocą żądania POST, ponieważ hello zwrócił się, że klucze są dostępne do zapisu. Innym przykładem umieszczenie **tylko do odczytu** blokada na zasób usługi aplikacji — uniemożliwia wyświetlanie plików hello zasobu, ponieważ dostęp do zapisu wymaga interakcji Eksploratora serwera w usłudze Visual Studio.

## <a name="who-can-create-or-delete-locks-in-your-organization"></a>Który można utworzyć lub usunąć blokady w organizacji
toocreate lub usunięcia blokady zarządzania, należy mieć dostęp zbyt`Microsoft.Authorization/*` lub `Microsoft.Authorization/locks/*` akcje. Witaj wbudowanych ról, tylko **właściciela** i **Administrator dostępu użytkowników** otrzymują te akcje.

## <a name="portal"></a>Portal
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a>Szablon
Witaj poniższy przykład przedstawia szablon, który tworzy blokady na koncie magazynu. Konto magazynu Hello, na które tooapply blokady hello jest podać jako parametr. Witaj nazwy blokady hello jest tworzony przez łączenie hello Nazwa zasobu z **/Microsoft.Authorization/** i hello w takim przypadku nazwa blokady hello **myLock**.

podano typ Hello jest toohello określonego typu zasobu. W przypadku magazynu wartość too"Microsoft.Storage/storageaccounts/providers/locks typu hello".

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="powershell"></a>PowerShell
Zablokuj należy wdrożyć zasobów przy użyciu programu Azure PowerShell przy użyciu hello [AzureRmResourceLock nowy](/powershell/module/azurerm.resources/new-azurermresourcelock) polecenia.

toolock zasobu, podaj nazwę hello hello zasobów, jego typ zasobu i jego nazwa grupy zasobów.

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

toolock grupę zasobów, podaj nazwę hello hello grupy zasobów.

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

tooget informacji na temat blokowania, użyj [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock). tooget Użyj wszystkich blokad hello w Twojej subskrypcji:

```powershell
Get-AzureRmResourceLock
```

tooget wszystkie blokady dla zasobu, należy użyć:

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

tooget wszystkie blokady dla grupy zasobów, należy użyć:

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

Program Azure PowerShell udostępnia inne polecenia blokad pracy, takich jak [AzureRmResourceLock zestaw](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate blokady, i [AzureRmResourceLock Usuń](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete blokady.

## <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure

Zablokuj należy wdrożyć zasobów przy użyciu wiersza polecenia platformy Azure przy użyciu hello [utworzyć blokady az](/cli/azure/lock#create) polecenia.

toolock zasobu, podaj nazwę hello hello zasobów, jego typ zasobu i jego nazwa grupy zasobów.

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

toolock grupę zasobów, podaj nazwę hello hello grupy zasobów.

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

tooget informacji na temat blokowania, użyj [listy blokady az](/cli/azure/lock#list). tooget Użyj wszystkich blokad hello w Twojej subskrypcji:

```azurecli
az lock list
```

tooget wszystkie blokady dla zasobu, należy użyć:

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

tooget wszystkie blokady dla grupy zasobów, należy użyć:

```azurecli
az lock list --resource-group exampleresourcegroup
```

Interfejs wiersza polecenia platformy Azure udostępnia innych poleceń blokad pracy, takich jak [az blokady aktualizacji](/cli/azure/lock#update) tooupdate blokady, i [usunąć blokady az](/cli/azure/lock#delete) toodelete blokady.

## <a name="rest-api"></a>Interfejs API REST
Można zablokować wdrożonych zasobów z hello [interfejsu API REST zarządzania blokad](https://docs.microsoft.com/rest/api/resources/managementlocks). Witaj interfejsu API REST umożliwia toocreate i usuwa blokady i pobierania informacji o istniejących blokad.

toocreate blokady, uruchom:

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

zakres Hello może być subskrypcji, grupy zasobów lub zasobów. Witaj Nazwa blokady jest dowolne toocall hello blokady. Wersja interfejsu api, można użyć **2015-01-01**.

W żądaniu hello obejmują obiekt JSON, który określa właściwości hello hello blokady.

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać więcej informacji na temat pracy z blokowania zasobów, zobacz [blokady w dół Your Azure zasobów](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)
* toolearn o logicznego organizowania zasobów, zobacz [używanie tagów tooorganize zasobów](resource-group-using-tags.md)
* toochange grupę zasobów zasób znajduje się w temacie [przeniesienie zasobów toonew zasobów grupy](resource-group-move-resources.md)
* Ograniczenia i konwencje można stosować w subskrypcji z niestandardowych zasad. Aby uzyskać więcej informacji, zobacz [zasady toomanage zasobów i kontroli dostępu](resource-manager-policy.md).
* Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).

