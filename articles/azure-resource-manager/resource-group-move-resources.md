---
title: "aaaMove zasobów Azure toonew subskrypcji lub grupy zasobów | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure Resource Manager toomove zasobów tooa nową grupę zasobów lub subskrypcji."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: tomfitz
ms.openlocfilehash: 09d35f0afbbcdc0c66779f98a982d878f0807497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-resources-toonew-resource-group-or-subscription"></a>Przenieś grupę zasobów toonew zasobów lub subskrypcji
W tym temacie pokazano, jak tooeither zasobów toomove nową subskrypcję lub nowy zasób grupy w hello tej samej subskrypcji. Można użyć portalu hello, programu PowerShell, interfejsu wiersza polecenia Azure lub hello zasobów toomove interfejsu API REST. Witaj operacji przenoszenia w tym temacie są dostępne tooyou bez żadnych pomoc techniczną platformy Azure.

Podczas przenoszenia zasobów, zarówno hello źródłowej grupy, jak i grupy docelowej hello są zablokowane podczas operacji hello. Zapisu i usuwania działań są zablokowane na temat grup zasobów hello dopiero po zakończeniu przenoszenia hello. Ta blokada oznacza, że nie można dodawać, aktualizować lub usuwać zasobów w grupach zasobów hello, ale nie oznacza to, że zasoby hello są zablokowane. Na przykład jeśli przenosisz programu SQL Server i jego nowej grupy zasobów bazy danych tooa aplikacji korzystającej z bazy danych hello napotyka bez przestojów. On nadal odczytu i zapisu toohello bazy danych.

Nie można zmienić lokalizacji hello hello zasobu. Przeniesienie zasobu tylko przenosi je tooa nową grupę zasobów. Witaj nowej grupy zasobów może mieć inną lokalizację, ale nie zmienia lokalizację hello hello zasobu.

> [!NOTE]
> W tym artykule opisano sposób wysyłania ofert konta toomove zasoby w istniejącą Azure. Jeśli konieczne toochange konta platformy Azure oferty (takich jak uaktualnianie z płatności obejmujące płatności toopre), pozostawiając toowork z istniejących zasobów, zobacz [przełącznika ofertę tooanother subskrypcji platformy Azure](../billing/billing-how-to-switch-azure-offer.md).
>
>

## <a name="checklist-before-moving-resources"></a>Lista kontrolna przed przeniesieniem zasobów
Istnieją pewne ważne czynności tooperform przed przeniesieniem zasobu. Dzięki sprawdzeniu tych warunków można uniknąć błędów.

1. Witaj subskrypcji źródłowych i docelowych musi istnieć w ramach hello sam [dzierżawy usługi Azure Active Directory](../active-directory/active-directory-howto-tenant.md). obie subskrypcje mają hello sam toocheck Identyfikatorem dzierżawy, użyj programu Azure PowerShell lub interfejsu wiersza polecenia platformy Azure.

  Dla programu Azure PowerShell użyj polecenia:

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  Azure CLI 2.0 należy użyć:

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  Jeśli hello dzierżawy identyfikatory hello źródłowego i docelowego subskrypcje są hello takie same, można spróbować katalogu hello toochange hello subskrypcji. Jednak ta opcja jest tylko dostępne tooService administratorów, którzy są podpisane za pomocą konta Microsoft (nie konta organizacyjnego). Zmienianie katalogu hello, logowanie toohello tooattempt [klasyczny portal](https://manage.windowsazure.com/)i wybierz **ustawienia**i wybierz subskrypcję hello. Jeśli hello **Edytuj katalog** ikona jest dostępna, zaznacz go toochange hello skojarzone usługi Azure Active Directory.

  ![Edytowanie katalogu](./media/resource-group-move-resources/edit-directory.png)

  Tę ikonę nie jest dostępny, musisz skontaktować się obsługa toomove hello zasobów tooa nowej dzierżawy.

2. Usługa Hello należy włączyć hello możliwości toomove zasobów. Ten temat zawiera listę usług, które umożliwiają przenoszenie zasobów i usług, które nie należy włączać przenoszenia zasobów.
3. Witaj, subskrypcji docelowej musi być zarejestrowana do dostawcy zasobów hello zasobu hello przenoszony. Jeśli nie, zostanie wyświetlony komunikat o błędzie informujący, że hello **subskrypcja nie jest zarejestrowana dla typu zasobu**. Ten problem może wystąpić, podczas przenoszenia zasobów tooa nową subskrypcję, ale tej subskrypcji nigdy nie został użyty z tym typem zasobu. toolearn toocheck hello stanu rejestracji i zarejestrować dostawców zasobów, zobacz [dostawców zasobów i typów](resource-manager-supported-services.md).

## <a name="when-toocall-support"></a>Jeżeli obsługują toocall
Można przenieść najwięcej zasobów za pomocą operacji samoobsługi hello wyświetlane w tym temacie. Użyj hello samoobsługi operacje:

* Przenieś zasoby usługi Resource Manager.
* Przenoszenie zasobów klasycznych zgodnie z toohello [ograniczenia wdrażania klasycznego](#classic-deployment-limitations).

Jeśli trzeba z działem pomocy technicznej:

* Przenoszenie zasobów tooa nowe konto platformy Azure (i dzierżawy usługi Azure Active Directory).
* Przenoszenie zasobów klasycznych, ale występują problemy z ograniczeniami hello.

## <a name="services-that-enable-move"></a>Usługi, które pozwalają przenoszenia
Obecnie dostępne są następujące usługi hello, umożliwiając przenoszenie tooboth nową grupę zasobów i subskrypcji:

* API Management
* Usługi aplikacji — aplikacje (aplikacje sieci web) — zobacz [ograniczenia usługi aplikacji](#app-service-limitations)
* Application Insights
* Automatyzacja
* Batch
* Mapy Bing
* CDN
* Usługi w chmurze — zobacz [Classic deployment ograniczenia](#classic-deployment-limitations)
* Cognitive Services
* Content Moderator
* Data Catalog
* Fabryka danych
* Data Lake Analytics
* Data Lake Store
* DNS
* Azure Cosmos DB
* Usługa Event Hubs
* Klastry HDInsight — zobacz [ograniczenia usługi HDInsight](#hdinsight-limitations)
* Centra IoT
* Usługa Key Vault
* Moduły równoważenia obciążenia
* Logic Apps
* Usługa Machine Learning
* Media Services
* Mobile Engagement
* Notification Hubs
* Operational Insights
* Operations Management
* Power BI
* Pamięć podręczna Redis
* Scheduler
* Wyszukiwanie
* Zarządzanie serwerem
* Service Bus
* Service Fabric
* Magazyn
* Magazyn (klasyczne) — zobacz [Classic deployment ograniczenia](#classic-deployment-limitations)
* Stream Analytics — usługi analiza strumienia zadania nie można przenieść uruchomionej w stanie.
* Serwer bazy danych SQL — Witaj bazy danych i serwera musi znajdować się w hello tej samej grupie zasobów. W przypadku przenoszenia programu SQL server, również są przenoszone jej baz danych.
* Traffic Manager
* Maszyny wirtualne
* Maszyny wirtualne z certyfikatem przechowywane w magazynie kluczy - toonew przeniesienie zasobów grupy w tej samej subskrypcji jest włączona, ale przenoszenia między subskrypcji nie jest włączona.
* Maszyny wirtualne (klasyczne) — zobacz [Classic deployment ograniczenia](#classic-deployment-limitations)
* Zestawy skali maszyn wirtualnych
* Sieci wirtualne — obecnie, peered sieci wirtualnej nie można przenieść do momentu równorzędna sieci wirtualnej zostały wyłączone. Po wyłączeniu hello sieci wirtualnej mogą zostać przeniesione pomyślnie i hello sieci wirtualnej komunikacji równorzędnej można włączyć. Ponadto sieci wirtualnej nie może być przeniesiony tooa innej subskrypcji Jeśli hello sieć wirtualna zawiera żadnej podsieci z zasobów łącza nawigacji. Na przykład podsieć sieci wirtualnej ma łącza nawigacji zasobu, gdy zasób redis Microsoft.Cache zostaje wdrożona do tej podsieci.
* VPN Gateway


## <a name="services-that-do-not-enable-move"></a>Usługi, które nie należy włączać przenoszenia
Witaj usług, które aktualnie nie należy włączać przenoszenie zasobu to:

* Usługi domenowe AD
* Usługa kondycji hybrydowe AD
* Application Gateway
* Zestawy dostępności z maszynami wirtualnymi z dyskami zarządzane
* BizTalk Services
* Container Service
* ExpressRoute
* DevTest Labs — przeniesienie grupy zasobów toonew w tej samej subskrypcji jest włączona, ale między przeniesienia subskrypcji nie jest włączona.
* Dynamics LCS
* Obrazy utworzone na podstawie zarządzanych dysków
* Managed Disks
* Zarządzane aplikacje
* Magazyn usług odzyskiwania — również nie przenoszenia hello obliczeniowych, sieci i magazynu zasoby skojarzone z tekst hello usług odzyskiwania magazynu, zobacz [ograniczenia usług odzyskiwania](#recovery-services-limitations).
* Bezpieczeństwo
* Migawek utworzonych z dysków zarządzanych
* Menedżer urządzeń StorSimple
* Maszyny wirtualne z dyskami zarządzanych
* Sieci wirtualne (klasyczne) — zobacz [Classic deployment ograniczenia](#classic-deployment-limitations)
* Nie można przenieść maszyny wirtualne utworzone na podstawie zasobów Marketplace - różnych subskrypcji. Zasób musi toobe anulowana w bieżącej subskrypcji hello i wdrożyć ponownie w nowej subskrypcji hello

## <a name="app-service-limitations"></a>Ograniczenia usługi aplikacji
Podczas pracy z aplikacjami usługi App Service, nie można przenieść plan usługi aplikacji. toomove usługi aplikacji — aplikacje, są następujące opcje:

* Przenieś hello planu usługi aplikacji i innych zasobów usługi aplikacji w tym zasobów grupy tooa nową grupę zasobów, które jeszcze nie ma zasobów usługi aplikacji. To wymaganie, że oznacza, że należy przenieść nawet hello zasobów usługi aplikacji — które nie są skojarzone z hello planu usługi aplikacji.
* Przenieś grupę zasobów różnych tooa aplikacji hello, ale zachować wszystkie plany usługi App Service w grupie zasobów z oryginalnego hello.

Witaj plan nie jest konieczne tooreside w usługi aplikacji hello tej samej grupie zasobów co aplikacja hello dla toofunction aplikacji hello poprawnie.

Na przykład, jeśli zawiera grupie zasobów:

* **sieci Web a** skojarzony z **planu a**
* **sieci Web-b** skojarzony z **plan-b**

Dostępne opcje to:

* Przenieś **sieci web a**, **planu a**, **sieci web-b**, i **plan-b**
* Przenieś **sieci web a** i **b sieci web**
* Przenieś **w sieci web**
* Przenieś **b sieci web**

Wszystkie inne kombinacje obejmują, pozostawiając w niej typ zasobu, który nie może pozostać podczas przenoszenia planu usługi App Service (dowolny typ zasobu usługi App Service).

Jeśli aplikacja sieci web znajduje się w innej grupie zasobów niż swój plan usługi aplikacji, ale ma toomove zarówno tooa nową grupę zasobów, należy wykonać przenoszenia hello w dwóch krokach. Na przykład:

* **sieci Web a** znajduje się w **grupy sieci web**
* **Plan a** znajduje się w **planu grupy**
* Ma **sieci web a** i **planu a** tooreside w **połączeniu grupy**

to przeniesienie, wykonaj dwa operacji przenoszenia oddzielne w powitania po sekwencji tooaccomplish:

1. Przenieś hello **sieci web a** zbyt**planu grupy**
2. Przenieś **sieci web a** i **planu a** za**łączyć grupy**.

Można przenieść certyfikatu usługi aplikacji tooa nową grupę zasobów lub subskrypcji, bez żadnych problemów. Jednak jeśli aplikacja sieci web zawiera certyfikat SSL zakupionych zewnętrznie, a następnie przekazać toohello aplikacji, należy usunąć hello certyfikatu przed aplikacji hello ruchu w sieci web. Na przykład można wykonywać hello następujące kroki:

1. Usuń certyfikat hello przekazany z hello aplikacji sieci web
2. Przenieś hello aplikacji sieci web
3. Przekaż aplikację sieci web toohello certyfikatu hello

## <a name="recovery-services-limitations"></a>Ograniczenia usługi odzyskiwania
Przenieś nie jest włączona dla magazynu, sieci, lub zasoby obliczeniowe używane tooset zapasowej odzyskiwania po awarii z usługi Azure Site Recovery.

Na przykład załóżmy, że po skonfigurowaniu replikacji konta magazynu tooa maszyny lokalnej (Storage1) i ma hello chronione maszyny toocome się po tooAzure pracy awaryjnej jako maszynę wirtualną (VM1) dołączony tooa sieci wirtualnej (Network1). Nie można przenieść żadnego z tych zasobów Azure - Storage1, VM1, oraz Network1 — między zasobów grup w hello takie same subskrypcji lub różnych subskrypcji.

## <a name="hdinsight-limitations"></a>Ograniczenia usługi HDInsight

Można przenieść klastrów HDInsight tooa nowej subskrypcji lub grupy zasobów. Jednak nie można przenieść między subskrypcjami hello sieci klastra usługi HDInsight toohello połączonych zasobów (na przykład hello sieci wirtualnej karty Sieciowej lub usługi równoważenia obciążenia). Ponadto nie można przenieść tooa nową grupę zasobów kartę Sieciową, która jest dołączona tooa maszyny wirtualnej klastra hello.

Podczas przenoszenia HDInsight klastra tooa nową subskrypcję, należy najpierw przenieść innych zasobów (takich jak hello konta magazynu). Następnie przenieś klastra usługi HDInsight hello samodzielnie.

## <a name="classic-deployment-limitations"></a>Wdrożenie klasyczne ograniczenia
Witaj Opcje przenoszenia zasobów wdrażać przy użyciu modelu klasycznego hello różnią się zależności od tego, czy przenosisz hello zasobów w ramach subskrypcji lub tooa nową subskrypcję.

### <a name="same-subscription"></a>Tej samej subskrypcji
Podczas przenoszenia zasobów z jednej grupy tooanother zasobów grupy zasobów w ramach hello zastosowania tej samej subskrypcji, hello następujące ograniczenia:

* Nie można przenieść sieci wirtualnych (klasyczny).
* Maszyny wirtualne (klasyczne) muszą zostać przeniesione z usługą w chmurze hello.
* Usługi w chmurze tylko przeniesienia podczas przenoszenia hello obejmuje wszystkie maszyny wirtualne.
* Usługi w chmurze tylko jeden mogą zostać przeniesione w czasie.
* Jednocześnie można przenosić tylko jedno konto magazynu (klasyczne).
* Konto magazynu (klasyczne) nie może zostać przeniesiony w hello tej samej operacji z maszyny wirtualnej lub usługi w chmurze.

toomove zasoby klasyczne tooa nowej grupy zasobów w hello tej samej subskrypcji, użyj operacji przenoszenia standardowe hello za pośrednictwem hello [portal](#use-portal), [programu Azure PowerShell](#use-powershell), [interfejsu wiersza polecenia Azure](#use-azure-cli), lub [interfejsu API REST](#use-rest-api). Możesz użyć hello tych samych operacji, ponieważ używane do przenoszenia zasoby usługi Resource Manager.

### <a name="new-subscription"></a>Nowa subskrypcja
Podczas przenoszenia zasobów tooa nową subskrypcję, zastosuj hello następujące ograniczenia:

* Wszystkie zasoby klasyczne w subskrypcji hello muszą zostać przeniesione w hello tej samej operacji.
* Witaj, subskrypcji docelowej nie może zawierać inne zasoby klasyczne.
* Przenieś Hello się żądać tylko wtedy za pomocą osobnych interfejsu API REST dla przenosi klasycznego. Witaj standardowe polecenia move Menedżera zasobów nie działają podczas przenoszenia zasobów klasycznych tooa nową subskrypcję.

toomove zasoby klasyczne tooa nowej subskrypcji, użyj operacji REST hello, które są tooclassic określonych zasobów. toouse REST, wykonaj następujące kroki hello:

1. Wyboru, jeśli subskrypcja źródłowa hello mogą uczestniczyć w między subskrypcjami przenieść. Użyj następującej operacji hello:

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     W treści żądania hello obejmują:

  ```json
  {
    "role": "source"
  }
  ```

     Hello odpowiedzi dla operacji sprawdzania poprawności hello jest hello następującego formatu:

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. Wyboru subskrypcji docelowej hello mogą uczestniczyć w między subskrypcjami przenieść. Użyj następującej operacji hello:

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     W treści żądania hello obejmują:

  ```json
  {
    "role": "target"
  }
  ```

     odpowiedź Hello jest hello takiego samego formatu jak hello źródła subskrypcji weryfikacji.
3. Jeśli obie subskrypcje przeszedł sprawdzania poprawności, Przenieś wszystkie zasoby klasyczne z jedną subskrypcją tooanother subskrypcji z hello następującej operacji:

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    W treści żądania hello obejmują:

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

Operacja Hello może trwać kilka minut.

## <a name="use-portal"></a>Korzystanie z portalu
toomove zasobów, wybierz grupę zasobów hello zawierające te zasoby, a następnie wybierz hello **Przenieś** przycisku.

![Przenoszenie zasobów](./media/resource-group-move-resources/select-move.png)

Określ, czy przenosisz hello zasobów tooa nową grupę zasobów lub nową subskrypcję.

Wybierz hello toomove zasobów i grupy zasobów hello docelowego. Potwierdzić wymagane skrypty tooupdate dla tych zasobów i wybierz **OK**. Jeśli wybrano hello edycji subskrypcją ikonę w poprzednim kroku hello, musisz wybrać hello subskrypcji docelowej.

![Wybierz miejsce docelowe](./media/resource-group-move-resources/select-destination.png)

W **powiadomienia**, zobacz ten hello Przenieś uruchomiona operacja.

![Pokaż stan przenoszenia](./media/resource-group-move-resources/show-status.png)

Po ukończeniu, użytkownik jest powiadamiany o hello wynik.

![Pokaż Przenieś wyników](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a>Korzystanie z programu PowerShell
toomove istniejącej grupy zasobów tooanother zasobów lub subskrypcji, użyj hello `Move-AzureRmResource` polecenia.

Witaj w pierwszym przykładzie pokazano sposób toomove jeden zasób tooa nową grupę zasobów.

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

Witaj w drugim przykładzie pokazano sposób toomove wiele zasobów tooa nową grupę zasobów.

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

Nowa subskrypcja tooa toomove zawierać wartość hello `DestinationSubscriptionId` parametru.

Pojawi się monit, które mają toomove hello tooconfirm określonych zasobów.

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a>Użyj interfejsu wiersza polecenia platformy Azure 2.0
toomove istniejącej grupy zasobów tooanother zasobów lub subskrypcji, użyj hello `az resource move` polecenia. Podaj zasobów hello identyfikatorów hello toomove zasobów. Identyfikatory zasobów można uzyskać z hello następujące polecenie:

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

Witaj poniższy przykład pokazuje, jak toomove magazynu konta tooa nową grupę zasobów. W hello `--ids` parametru, podaj rozdzieloną spacjami listę toomove identyfikatorów zasobów hello.

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

toomove tooa nową subskrypcję, podaj hello `--destination-subscription-id` parametru.

## <a name="use-azure-cli-10"></a>Użyj interfejsu wiersza polecenia platformy Azure 1.0
toomove istniejącej grupy zasobów tooanother zasobów lub subskrypcji, użyj hello `azure resource move` polecenia. Podaj zasobów hello identyfikatorów hello toomove zasobów. Identyfikatory zasobów można uzyskać z hello następujące polecenie:

```azurecli
azure resource list -g sourceGroup --json
```

Polecenie to zwraca hello następującego formatu:

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

Witaj poniższy przykład pokazuje, jak toomove magazynu konta tooa nową grupę zasobów. W hello `-i` parametru zawierają toomove identyfikatorów zasobów hello listę rozdzielaną przecinkami.

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

Pojawi się monit, które mają toomove hello tooconfirm określony zasób.

## <a name="use-rest-api"></a>Używanie interfejsu API REST
toomove istniejącą zasobów tooanother grupę zasobów lub subskrypcji, uruchom:

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

W treści żądania hello należy określić hello docelowa grupa zasobów i hello toomove zasobów. Aby uzyskać więcej informacji na temat operacji REST przenoszenia hello zobacz [przenoszenia zasobów](https://msdn.microsoft.com/library/azure/mt218710.aspx).

## <a name="next-steps"></a>Następne kroki
* toolearn o poleceniach cmdlet programu PowerShell do zarządzania subskrypcją, zobacz [przy użyciu programu Azure PowerShell z usługą Resource Manager](powershell-azure-resource-manager.md).
* toolearn o polecenia wiersza polecenia platformy Azure do zarządzania subskrypcją, zobacz [hello Using Azure CLI za pomocą Menedżera zasobów](xplat-cli-azure-resource-manager.md).
* Zobacz toolearn funkcje portalu do zarządzania subskrypcją, [korzystanie z zasobów platformy Azure toomanage portalu hello](resource-group-portal.md).
* toolearn o zastosowaniu logicznej tooyour zasobów organizacji, zobacz [używanie tagów tooorganize zasobami](resource-group-using-tags.md).
