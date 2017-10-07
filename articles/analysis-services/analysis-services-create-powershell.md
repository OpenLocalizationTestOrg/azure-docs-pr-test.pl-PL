---
title: "aaaCreate serwerem usług Azure Analysis Services przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Azure Analysis Services serwera przy użyciu programu PowerShell"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/01/2017
ms.author: owend
ms.custom: mvc
ms.openlocfilehash: 269b78983410f773d47c4cea34d6d353b19f9e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a>Tworzenie serwera usług Azure Analysis Services przy użyciu programu PowerShell

Tego przewodnika Szybki Start zawiera opis korzystania ze środowiska PowerShell z toocreate wiersza polecenia hello serwerem usług Azure Analysis Services w [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) w Twojej subskrypcji platformy Azure.

Dla tego zadania jest wymagany moduł Azure PowerShell w wersji 4.0 lub nowszej. Wersja hello toofind, uruchom ` Get-Module -ListAvailable AzureRM`. tooinstall lub uaktualniania, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps). 

> [!NOTE]
> Utworzenie serwera może skutkować powstaniem nowej usługi płatnej. toolearn więcej, zobacz [cennik usług Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete tego przewodnika Szybki Start, należy:

* **Subskrypcja platformy Azure**: odwiedź [bezpłatnej wersji próbnej Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate konta.
* **Azure Active Directory**: subskrypcja musi być skojarzona z dzierżawą usługi Azure Active Directory i musisz mieć konto w tym katalogu. toolearn więcej, zobacz [uprawnienia do uwierzytelniania i użytkownik](analysis-services-manage-users.md).

## <a name="import-azurermanalysisservices-module"></a>Importowanie modułu AzureRm.AnalysisServices
toocreate serwera w ramach subskrypcji, użyj hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) składnika modułu. Załaduj moduł AzureRm.AnalysisServices hello do sesji programu PowerShell.

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-tooazure"></a>Zaloguj się tooAzure

Zaloguj się tooyour subskrypcji platformy Azure przy użyciu hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) polecenia. Wykonaj hello wyświetlanymi instrukcjami.

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów
 
[Grupa zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi w formie grupy. Podczas tworzenia serwera musisz podać grupę zasobów w ramach subskrypcji. Jeśli nie masz już grupę zasobów, można utworzyć nową przy użyciu hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) polecenia. Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` hello regionu zachodnie stany USA.

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a>Tworzenie serwera

Tworzenie nowego serwera przy użyciu hello [AzureRmAnalysisServicesServer nowy](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) polecenia. Witaj poniższy przykład tworzy serwer o nazwie MójSerwer w myResourceGroup w hello regionu zachodnie stany USA, w warstwie hello D1 i określa philipc@adventureworks.com jako administrator serwera.

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Można usunąć serwera hello z subskrypcji przy użyciu hello [AzureRmAnalysisServicesServer Usuń](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) polecenia. Jeśli będziesz korzystać z innych przewodników Szybki start i samouczków w tej kolekcji, nie usuwaj serwera. Witaj poniższy przykład umożliwia usunięcie serwera hello utworzony w poprzednim kroku hello.


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a>Następne kroki
[Zarządzanie usługami Azure Analysis Services przy użyciu programu PowerShell](analysis-services-powershell.md)   
[Wdrażanie modelu w programie SSDT](analysis-services-deploy.md)   
[Create a model in Azure portal (preview) (Tworzenie modelu w wersji zapoznawczej witryny Azure Portal)](analysis-services-create-model-portal.md)