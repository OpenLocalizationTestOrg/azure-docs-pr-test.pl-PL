---
title: "aaaManage Azure rozwiązania przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Użyj programu Azure PowerShell i Menedżera zasobów toomanage zasobów."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 47a91af8d7eb59585bcfd43571ce76b90a0d7971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a>Zarządzanie zasobami za pomocą programu Azure PowerShell i Menedżera zasobów
> [!div class="op_single_selector"]
> * [Portal](resource-group-portal.md)
> * [Interfejs wiersza polecenia platformy Azure](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [Interfejs API REST](resource-manager-rest-api.md)
>
>

W tym artykule dowiesz się, jak toomanage rozwiązań z programu Azure PowerShell i Menedżera zasobów Azure. Jeśli nie masz doświadczenia z usługą Resource Manager, zobacz [omówienie Resource Manager](resource-group-overview.md). Ten temat koncentruje się na zadań zarządzania. Wykonasz następujące zadania:

1. Tworzenie grupy zasobów
2. Dodaj grupę zasobów toohello zasobów
3. Dodaj zasób toohello tag
4. Wykonywanie zapytań względem zasobów na podstawie nazw lub wartości tagów
5. Zastosuj i Usuń blokadę hello zasobów
6. Usuń grupę zasobów

W tym artykule nie pokazuje sposób toodeploy subskrypcji tooyour szablonu usługi Resource Manager. Informacje, zobacz [wdrażanie zasobów przy użyciu szablonów usługi Resource Manager i programu Azure PowerShell](resource-group-template-deploy.md).

## <a name="get-started-with-azure-powershell"></a>Wprowadzenie do programu Azure PowerShell

Jeśli nie zainstalowano programu Azure PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

W przeszłości hello mieć zainstalowany program Azure PowerShell, ale nie zaktualizowano on niedawno, można zainstalować hello najnowszej wersji. Można aktualizować wersji hello za pośrednictwem hello tej samej metody używane tooinstall go. Na przykład jeśli użyto hello Instalatora platformy sieci Web, uruchom ją ponownie i wyszukać aktualizację.

Użyj wersji hello modułu zasobów Azure toocheck hello poniższe polecenie cmdlet:

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

Ten temat został zaktualizowany na potrzeby wersji 3.3.0. Jeśli masz starszą wersję środowiska mogą nie odpowiadać hello kroki opisane w tym temacie. Aby uzyskać dokumentację poleceń cmdlet hello w tej wersji, zobacz [AzureRM.Resources modułu](/powershell/module/azurerm.resources).

## <a name="log-in-tooyour-azure-account"></a>Zaloguj się za tooyour konto platformy Azure
Przed rozpoczęciem pracy rozwiązania, należy zalogować się tooyour konta.

toolog w tooyour konto platformy Azure, użyj hello **Login-AzureRmAccount** polecenia cmdlet.

```powershell
Login-AzureRmAccount
```

polecenia cmdlet Hello monituje o hello poświadczenia logowania dla konta platformy Azure. Po zalogowaniu pobraniu ustawienia konta tak, aby były dostępne tooAzure środowiska PowerShell.

polecenia cmdlet Hello zwraca informacje dotyczące Twojego konta i hello toouse subskrypcji hello zadań.

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

Jeśli masz więcej niż jedną subskrypcję, możesz przełączyć tooa innej subskrypcji. Po pierwsze Zobacz wszystkie subskrypcje powitania dla Twojego konta.

```powershell
Get-AzureRmSubscription
```

Zwraca włączyć i wyłączyć subskrypcje.

```powershell
SubscriptionName : Example Subscription One
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Two
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Three
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Disabled
```

tooswitch tooa inną subskrypcję, podaj nazwę subskrypcji hello z hello **Set-AzureRmContext** polecenia cmdlet.

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów
Przed wdrożeniem żadnej subskrypcji tooyour zasobów, należy utworzyć grupę zasobów, która będzie zawierać hello zasobów.

toocreate grupę zasobów, użyj hello **New-AzureRmResourceGroup** polecenia cmdlet. polecenie Hello używa hello **nazwa** toospecify parametru nazwę grupy zasobów hello i hello **lokalizacji** toospecify parametru jego lokalizacji.

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

dane wyjściowe Hello znajduje się w hello następującego formatu:

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

Grupa zasobów tooretrieve hello później, należy użyć hello następującego polecenia cmdlet:

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

tooget hello wszystkich grup zasobów w ramach subskrypcji, nie należy określać nazwy:

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-tooa-resource-group"></a>Dodaj grupę zasobów tooa zasobów
tooadd grupę zasobów toohello zasobów, można użyć hello **AzureRmResource nowy** polecenia cmdlet lub polecenia cmdlet, który jest typem toohello określonego zasobu tworzysz (takich jak **New-AzureRmStorageAccount**). Może być łatwiejsze toouse polecenia cmdlet, które jest tooa określonego typu zasobu, ponieważ zawiera on parametrów hello właściwości, które są potrzebne dla nowego zasobu hello. toouse **AzureRmResource nowy**, musisz znać wszystkie tooset właściwości hello bez monitowania o nich.

Jednak dodawanie zasobów za pomocą poleceń cmdlet może spowodować przyszłych pomyłek, ponieważ hello nowy zasób nie istnieje w szablonie usługi Resource Manager. Firma Microsoft zaleca Definiowanie hello infrastrukturę Twojego rozwiązania Azure w ramach szablonu usługi Resource Manager. Szablony umożliwiają tooreliably i wielokrotnie wdrażać rozwiązania. W tym temacie Tworzenie konta magazynu za pomocą polecenia cmdlet programu PowerShell, ale później wygenerowanie szablonu z grupy zasobów.

Witaj następujące polecenie cmdlet tworzy konto magazynu. Zamiast przy użyciu nazwy hello pokazano w przykładzie hello, Podaj unikatową nazwę konta magazynu hello. Nazwa Hello musi należeć do zakresu od 3 do 24 znaków i zawierać tylko cyfry i małe litery. Jeśli używasz nazwę hello pokazano w przykładzie hello, wystąpi błąd, ponieważ ta nazwa jest już używana.

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

Tooretrieve tego zasobu później, należy użyć hello następującego polecenia cmdlet:

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a>Dodaj tag

Znaczniki umożliwiają tooorganize zasobów zgodnie z toodifferent właściwości. Na przykład organizacja może mieć kilka zasoby w różnych grup zasobów należących toohello samego działu. Możesz zastosować działu tagu i wartość toothose zasobów toomark ich jako należące toohello tej samej kategorii. Alternatywnie można oznaczyć, czy zasób jest używany w środowisku produkcyjnym lub testowym. W tym temacie należy zastosować tagi tooonly jeden zasób, ale w danym środowisku prawdopodobnie sens się, że tooapply znaczniki tooall zasobów.

Witaj następującego polecenia cmdlet stosuje się dwa konta magazynu tooyour tagów:

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

Tagi są aktualizowane jako pojedynczego obiektu. tooadd tag zasobu tooa, która zawiera już znaczników, najpierw pobrać hello znaczników. Dodaj hello nowego tagu toohello obiekt, który zawiera hello znaczników i zastosuj je ponownie wszystkie hello tagi toohello zasobów.

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a>Wyszukaj zasoby

Użyj hello **AzureRmResource Znajdź** zasoby tooretrieve polecenia cmdlet dla różnych warunki.

* tooget zasobów według nazwy, podaj hello **ResourceNameContains** parametru:

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* tooget wszystkie zasoby hello w grupie zasobów, zawierają hello **ResourceGroupNameContains** parametru:

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* tooget wszystkie zasoby hello o nazwie tagu i wartości, zawierają hello **TagName** i **TagValue** parametry:

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* zasoby hello tooall z określonego typu zasobu, zawierają hello **ResourceType** parametru:

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a>Zablokowanie zasobu

Gdy potrzebne są toomake się, że krytycznego zasobu nie zostanie przypadkowo usunięty lub zmodyfikowany, zastosuj toohello zablokować zasobu. Można określić **CanNotDelete** lub **tylko do odczytu**.

toocreate lub usunięcia blokady zarządzania, należy mieć dostęp zbyt`Microsoft.Authorization/*` lub `Microsoft.Authorization/locks/*` akcje. Witaj wbudowanych ról tylko właściciel i Administrator dostępu użytkowników są przyznawane te akcje.

tooapply blokady, użyj następującego polecenia cmdlet hello:

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

Witaj zablokowane w hello poprzedzających przykład nie można usunąć zasobu do momentu usunięcia blokady hello. tooremove blokady, należy użyć:

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

Aby uzyskać więcej informacji na temat ustawienie blokady, zobacz [blokowania zasobów z usługi Azure Resource Manager](resource-group-lock-resources.md).

## <a name="remove-resources-or-resource-group"></a>Usuwanie zasobów lub grupy zasobów
Można usunąć zasób lub grupa zasobów. Usuń grupę zasobów, należy również usunąć wszystkie zasoby hello w tej grupie zasobów.

* toodelete zasobów z hello grupy zasobów, użyj hello **AzureRmResource Usuń** polecenia cmdlet. To polecenie cmdlet usuwa hello zasobów, ale nie powoduje usunięcia hello grupy zasobów.

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* toodelete grupy zasobów i wszystkie jego zasoby, używać hello **Remove-AzureRmResourceGroup** polecenia cmdlet.

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

Dla obu poleceń cmdlet, zostanie wyświetlona prośba tooconfirm mają tooremove hello zasób lub grupa zasobów. Jeśli operacja hello pomyślnie usuwa hello zasób lub grupa zasobów, zwraca **True**.

## <a name="run-resource-manager-scripts-with-azure-automation"></a>Uruchamianie skryptów Menedżera zasobów w usłudze Automatyzacja Azure

W tym temacie opisano sposób tooperform podstawowe operacje na zasoby przy użyciu programu Azure PowerShell. W przypadku bardziej zaawansowanych scenariuszy zarządzania są zazwyczaj mają toocreate skryptu i ponownie użyć tego skryptu, zgodnie z potrzebami lub zgodnie z harmonogramem. [Automatyzacja Azure](../automation/automation-intro.md) umożliwia możesz tooautomate często używane skryptów, które zarządzają rozwiązań platformy Azure.

Witaj poniższe tematy przedstawiają sposób wykonywania zadań zarządzania toouse usługi Automatyzacja Azure Resource Manager i tooeffectively środowiska PowerShell:

- Aby uzyskać informacje dotyczące tworzenia elementu runbook, zobacz [Moje pierwszego elementu runbook programu PowerShell](../automation/automation-first-runbook-textual-powershell.md).
- Aby uzyskać informacje na temat pracy z galerii skryptów, zobacz [galerie elementów Runbook i modułów w automatyzacji Azure](../automation/automation-runbook-gallery.md).
- Dla elementów runbook uruchamianie i zatrzymywanie maszyn wirtualnych, zobacz [scenariusz automatyzacji Azure: toocreate formacie JSON przy użyciu tagów harmonogram uruchamiania maszyny Wirtualnej platformy Azure i zamykania](../automation/automation-scenario-start-stop-vm-wjson-tags.md).
- Dla elementów runbook uruchamianie i zatrzymywanie maszyn wirtualnych po godzinach pracy, zobacz [uruchamiania/zatrzymywania maszyn wirtualnych, podczas rozwiązania poza godzinami szczytu w automatyzacji](../automation/automation-solution-vm-management.md).

## <a name="next-steps"></a>Następne kroki
* toolearn o tworzeniu szablonów usługi Resource Manager, zobacz [Authoring Azure Resource Manager szablony](resource-group-authoring-templates.md).
* toolearn o wdrażanie szablonów, zobacz [wdrażanie aplikacji przy użyciu szablonu usługi Resource Manager Azure](resource-group-template-deploy.md).
* Można przenieść istniejące zasoby tooa nową grupę zasobów. Aby uzyskać przykłady, zobacz [tooNew przeniesienia zasobów grupy zasobów lub subskrypcji](resource-group-move-resources.md).
* Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).

