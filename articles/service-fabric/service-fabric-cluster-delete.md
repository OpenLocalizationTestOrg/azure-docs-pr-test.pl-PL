---
title: "aaaDelete Azure klastra i jego zasobów | Dokumentacja firmy Microsoft"
description: "Dowiedz się, w jaki sposób usuwania toocompletely usługi sieć szkieletowa klastra albo usunięcie grupy zasobów hello zawierające hello klastra lub przez selektywne usuwanie zasobów."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: de422950-2d22-4ddb-ac47-dd663a946a7e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/24/2017
ms.author: chackdan
ms.openlocfilehash: 5c15a4184644da715cd69397f2150de86ab433ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-hello-resources-it-uses"></a>Usuwanie klastra sieci szkieletowej usług Azure i hello zasobów, które są używane
Klastra usługi sieć szkieletowa składa się z wielu zasobów platformy Azure dodatkowo zasobu klastra toohello samej siebie. Dlatego toocompletely Usuwanie klastra sieci szkieletowej usług należy również toodelete hello wszystkie zasoby, które składa się z.
Dostępne są dwie opcje: albo grupa zasobów hello delete hello klastra (który usuwa hello zasobu klastra i innych zasobów w grupie zasobów hello) lub specjalnie usunąć zasobu klastra hello i związany z zasobów (ale nie innych zasoby w grupie zasobów hello).

> [!NOTE]
> Usuwanie zasobu klastra hello **nie** Usuń wszystkie hello inne zasoby, które klastra usługi sieć szkieletowa składa się z.
> 
> 

## <a name="delete-hello-entire-resource-group-rg-that-hello-service-fabric-cluster-is-in"></a>Usuń grupę zasobów całej hello (zarządcy zasobów), który hello klaster znajduje się w sieci szkieletowej usług
Jest to najprostszy tooensure sposób hello, aby usunąć wszystkie zasoby hello skojarzony z klastrem, w tym hello grupy zasobów. Można usunąć grupy zasobów hello przy użyciu programu PowerShell lub za pośrednictwem hello portalu Azure. Jeśli grupa zasobów zawiera zasoby, które nie są powiązane tooService klastra sieci szkieletowej, można usunąć określonych zasobów.

### <a name="delete-hello-resource-group-using-azure-powershell"></a>Usuń grupę zasobów hello przy użyciu programu Azure PowerShell
Można również usunąć hello grupy zasobów, uruchamiając następujące polecenia cmdlet programu Azure PowerShell hello. Upewnij się, że Azure PowerShell 1.0 lub jest zainstalowany na tym komputerze. Jeśli nie zostało zrobione to przed, wykonaj kroki hello opisane w temacie [jak tooinstall i konfigurowanie programu Azure PowerShell.](/powershell/azure/overview)

Otwórz okno programu PowerShell i uruchom następujące polecenia cmdlet PS hello:

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

Otrzymasz usunięcia hello tooconfirm monitu, jeśli nie używasz hello *-Force* opcji. Na potwierdzenie hello zarządcy zasobów i zostaną usunięte wszystkie zasoby hello, które zawiera.

### <a name="delete-a-resource-group-in-hello-azure-portal"></a>Usuń grupę zasobów w hello portalu Azure
1. Toohello logowania [portalu Azure](https://portal.azure.com).
2. Przejdź toohello klastra sieci szkieletowej usług ma toodelete.
3. Powitania kliknij nazwę grupy zasobów na stronie essentials klastra hello.
4. Spowoduje to wyświetlenie hello **Essentials grupy zasobów** strony.
5. Kliknij polecenie **Usuń**.
6. Wykonaj instrukcje hello na usunięcie hello toocomplete strony tego hello grupy zasobów.

![Usuń grupę zasobów][ResourceGroupDelete]

## <a name="delete-hello-cluster-resource-and-hello-resources-it-uses-but-not-other-resources-in-hello-resource-group"></a>Usuń zasób klastra hello i hello zasoby, które są używane, ale nie innych zasobów w grupie zasobów hello
Jeśli grupa zasobów zawiera tylko tych zasobów, które są powiązane toohello klastra sieci szkieletowej usług ma toodelete, a następnie jest łatwiejsze toodelete hello całej grupy zasobów. Jeśli chcesz tooselectively delete hello zasobów jeden po drugim w grupie zasobów, następnie wykonaj następujące kroki.

Jeśli wdrożono klastra przy użyciu portalu hello lub jednego z szablonów usługi sieć szkieletowa Resource Manager hello z galerii szablonów hello wszystkie zasoby hello hello używa klastra są oznaczone tagiem hello następujące dwa tagi. Można ich używać toodecide zasobów, do których chcesz toodelete.

***Tag #1:*** klucz = Nazwa_klastra, wartość = "Nazwa klastra hello"

***Tag #2:*** klucz = resourceName, wartość = ServiceFabric

### <a name="delete-specific-resources-in-hello-azure-portal"></a>Usuń wybrane zasoby hello portalu Azure
1. Toohello logowania [portalu Azure](https://portal.azure.com).
2. Przejdź toohello klastra sieci szkieletowej usług ma toodelete.
3. Przejdź za**wszystkie ustawienia** na powitania essentials bloku.
4. Polecenie **tagi** w obszarze **zarządzanie zasobami** w bloku ustawienia hello.
5. Kliknij jeden z hello **tagi** w hello tagi bloku tooget listę wszystkich zasobów hello z tym znacznikiem.
   
    ![Tagi zasobów][ResourceTags]
6. Po utworzeniu listy hello oznakowanych zasobów, kliknij każdy z zasobów hello i usuń je.
   
    ![Oznakowane zasobów][TaggedResources]

### <a name="delete-hello-resources-using-azure-powershell"></a>Usuwanie zasobów hello przy użyciu programu Azure PowerShell
Możesz usunąć zasoby powitania po kolei, uruchamiając następujące polecenia cmdlet programu Azure PowerShell hello. Upewnij się, że Azure PowerShell 1.0 lub jest zainstalowany na tym komputerze. Jeśli nie zostało zrobione to przed, wykonaj kroki hello opisane w temacie [jak tooinstall i konfigurowanie programu Azure PowerShell.](/powershell/azure/overview)

Otwórz okno programu PowerShell i uruchom następujące polecenia cmdlet PS hello:

```powershell
Login-AzureRmAccount
```
Dla każdego z zasobów hello mają toodelete, uruchom następujące hello:

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of hello resource group>" -Force
```

toodelete hello zasobu klastra, uruchom następujące hello:

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of hello resource group>" -Force
```

## <a name="next-steps"></a>Następne kroki
Po tooalso hello odczytu więcej informacji na temat uaktualniania klastra i partycjonowania usługi:

* [Więcej informacji na temat uaktualnienia klastra](service-fabric-cluster-upgrade.md)
* [Więcej informacji na temat partycjonowania usługi stanowej maksymalną skalę](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
