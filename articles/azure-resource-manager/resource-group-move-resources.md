---
title: "Przenoszenie zasobów platformy Azure do nowej grupy zasobów lub subskrypcji | Dokumentacja firmy Microsoft"
description: "Umożliwia przenoszenie zasobów do nowej grupy zasobów lub subskrypcji usługi Azure Resource Manager."
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
ms.openlocfilehash: e138f80e808968ab4bf5c11cfd5fd46fe4a1bcce
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="move-resources-to-new-resource-group-or-subscription"></a>Przenoszenie zasobów do nowej grupy zasobów lub subskrypcji
W tym temacie przedstawiono sposób przenoszenia zasobów do nowej subskrypcji lub nowej grupy zasobów w tej samej subskrypcji. Aby przenieść zasobu można użyć portalu, programu PowerShell, interfejsu wiersza polecenia Azure lub interfejsu API REST. Operacji przenoszenia w tym temacie są dostępne bez pomocy w pomocy technicznej platformy Azure.

Podczas przenoszenia zasobów, zarówno grupy źródłowej i docelowej grupy są zablokowane podczas operacji. Zapisu i usuwania działań są zablokowane na grupy zasobów, dopiero po zakończeniu przenoszenia. Ta blokada oznacza, że nie można dodawać, aktualizować lub usuwać zasoby w grupie zasobów, ale nie oznacza to, że zasoby są zablokowane. Na przykład jeśli zostanie przeniesiony do nowej grupy zasobów programu SQL Server i jego bazy danych, aplikacji korzystającej z bazy danych napotyka bez przestojów. Można nadal odczytu i zapisu w bazie danych.

Nie można zmienić lokalizacji zasobu. Przeniesienie zasobu tylko przenosi je do nowej grupy zasobów. Nową grupę zasobów może zawierać innej lokalizacji, ale nie zmienia lokalizację zasobu.

> [!NOTE]
> W tym artykule opisano sposób przenoszenia zasobów w ramach platformy Azure istniejącego konta wysyłania ofert. Jeśli rzeczywiście chcesz zmienić konta platformy Azure oferty (takich jak uaktualnianie z płatność za rzeczywiste użycie wstępnie zapłacenia) podczas kontynuowanie pracy z istniejących zasobów, zobacz [Przełącz subskrypcji platformy Azure do innej oferty](../billing/billing-how-to-switch-azure-offer.md).
>
>

## <a name="checklist-before-moving-resources"></a>Lista kontrolna przed przeniesieniem zasobów
Przed przeniesieniem zasobu należy wykonać kilka ważnych kroków. Dzięki sprawdzeniu tych warunków można uniknąć błędów.

1. Subskrypcje źródłowych i docelowych musi istnieć w tym samym [dzierżawy usługi Azure Active Directory](../active-directory/active-directory-howto-tenant.md). Aby sprawdzić, czy obie subskrypcje mają ten sam identyfikator dzierżawy, użyj programu Azure PowerShell lub interfejsu wiersza polecenia platformy Azure.

  Dla programu Azure PowerShell użyj polecenia:

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  Azure CLI 2.0 należy użyć:

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  Dzierżawy identyfikatorów subskrypcji źródłowych i docelowych nie są takie same, możesz spróbować zmienić katalogu dla subskrypcji. Jednak ta opcja jest dostępna tylko dla administratorów usługi, który jest zalogowany za pomocą konta Microsoft (nie konta organizacyjnego). Próba zmiany katalogu, zaloguj się do [klasyczny portal](https://manage.windowsazure.com/)i wybierz **ustawienia**i wybierz subskrypcję. Jeśli **Edytuj katalog** ikona jest dostępna, zaznacz go, aby zmienić skojarzone usługi Azure Active Directory.

  ![Edytowanie katalogu](./media/resource-group-move-resources/edit-directory.png)

  Jeśli tej ikony nie jest dostępna, należy się z pomocą techniczną przeniesienie zasobów do nowej dzierżawy.

2. Usługa musi mieć możliwość przenoszenia zasobów. Ten temat zawiera listę usług, które umożliwiają przenoszenie zasobów i usług, które nie należy włączać przenoszenia zasobów.
3. Subskrypcja docelowa musi być zarejestrowana dla dostawcy przenoszonego zasobu. Jeśli nie, zostanie wyświetlony komunikat o błędzie informujący, że **subskrypcja nie jest zarejestrowana dla typu zasobu**. Ten problem może wystąpić podczas przenoszenia zasobu do nowej subskrypcji, która nigdy nie była używana z tym typem zasobu. Aby dowiedzieć się, jak sprawdzić stan rejestracji i zarejestrować dostawców zasobów, zobacz część [Resource providers and types](resource-manager-supported-services.md) (Dostawcy i typy zasobów).

## <a name="when-to-call-support"></a>Kiedy Zadzwoń do pomocy technicznej
Można przenieść najwięcej zasobów za pomocą operacji samoobsługi wyświetlany w tym temacie. Użyj operacje samoobsługi:

* Przenieś zasoby usługi Resource Manager.
* Przenoszenie zasobów klasycznych zgodnie z [ograniczenia wdrażania klasycznego](#classic-deployment-limitations).

Jeśli trzeba z działem pomocy technicznej:

* Przenoszenie zasobów dla nowego konta platformy Azure (i dzierżawy usługi Azure Active Directory).
* Przenoszenie zasobów klasycznych, ale występują problemy z ograniczeniami.

## <a name="services-that-enable-move"></a>Usługi, które pozwalają przenoszenia
Na razie usługi umożliwiające przeniesienie do nowej grupy zasobów i subskrypcji są:

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
* Baza danych SQL server — bazy danych i serwera musi znajdować się w tej samej grupie zasobów. W przypadku przenoszenia programu SQL server, również są przenoszone jej baz danych.
* Traffic Manager
* Maszyny wirtualne
* Maszyny wirtualne z certyfikatem przechowywane w magazynie kluczy - Przenieś do nowego zasobu, grupy w tej samej subskrypcji jest włączona, ale przenoszenia między subskrypcji nie jest włączona.
* Maszyny wirtualne (klasyczne) — zobacz [Classic deployment ograniczenia](#classic-deployment-limitations)
* Zestawy skali maszyn wirtualnych
* Sieci wirtualne — obecnie, peered sieci wirtualnej nie można przenieść do momentu równorzędna sieci wirtualnej zostały wyłączone. Po wyłączeniu sieci wirtualnej mogą zostać przeniesione pomyślnie i równorzędna sieci wirtualnej można włączyć. Ponadto sieci wirtualnej nie można przenieść do innej subskrypcji, jeśli sieć wirtualna zawiera żadnej podsieci z zasobów łącza nawigacji. Na przykład podsieć sieci wirtualnej ma łącza nawigacji zasobu, gdy zasób redis Microsoft.Cache zostaje wdrożona do tej podsieci.
* VPN Gateway


## <a name="services-that-do-not-enable-move"></a>Usługi, które nie należy włączać przenoszenia
Usługi, które aktualnie nie należy włączać przenoszenie zasobu to:

* Usługi domenowe AD
* Usługa kondycji hybrydowe AD
* Application Gateway
* Zestawy dostępności z maszynami wirtualnymi z dyskami zarządzane
* BizTalk Services
* Container Service
* ExpressRoute
* Włączono DevTest Labs — aby przejść do nowej grupy zasobów w tej samej subskrypcji, ale przenoszenia między subskrypcji nie jest włączona.
* Dynamics LCS
* Obrazy utworzone na podstawie zarządzanych dysków
* Managed Disks
* Zarządzane aplikacje
* Magazyn usług odzyskiwania — czy też nie przeniesienie zasobów obliczeniowych, sieci i magazynu skojarzone z magazynu usług odzyskiwania, zobacz [ograniczenia usług odzyskiwania](#recovery-services-limitations).
* Bezpieczeństwo
* Migawek utworzonych z dysków zarządzanych
* Menedżer urządzeń StorSimple
* Maszyny wirtualne z dyskami zarządzanych
* Sieci wirtualne (klasyczne) — zobacz [Classic deployment ograniczenia](#classic-deployment-limitations)
* Nie można przenieść maszyny wirtualne utworzone na podstawie zasobów Marketplace - różnych subskrypcji. Zasób musi zostać anulowana w bieżącej subskrypcji i wdrożyć ponownie w nowej subskrypcji

## <a name="app-service-limitations"></a>Ograniczenia usługi aplikacji
Podczas pracy z aplikacjami usługi App Service, nie można przenieść plan usługi aplikacji. Aby przenieść aplikacji usługi App Service, dostępne są następujące opcje:

* Przenieś plan usługi aplikacji i innych zasobów usługi aplikacji w tej grupie zasobów do nowej grupy zasobów, które jeszcze nie ma zasobów usługi aplikacji. Wymaganie to oznacza, że należy przenieść nawet zasoby usługi aplikacji, które nie są skojarzone z planu usługi aplikacji.
* Przenieś aplikacje na innej grupie zasobów, ale zachować wszystkie plany usługi App Service w oryginalnej grupy zasobów.

Plan usługi aplikacji nie musi znajdować się w tej samej grupie zasobów co aplikacja dla aplikacji do poprawnego działania.

Na przykład, jeśli zawiera grupie zasobów:

* **sieci Web a** skojarzony z **planu a**
* **sieci Web-b** skojarzony z **plan-b**

Dostępne opcje to:

* Przenieś **sieci web a**, **planu a**, **sieci web-b**, i **plan-b**
* Przenieś **sieci web a** i **b sieci web**
* Przenieś **w sieci web**
* Przenieś **b sieci web**

Wszystkie inne kombinacje obejmują, pozostawiając w niej typ zasobu, który nie może pozostać podczas przenoszenia planu usługi App Service (dowolny typ zasobu usługi App Service).

Jeśli aplikacja sieci web znajduje się w innej grupie zasobów niż swój plan usługi aplikacji, ale chcesz przenieść zarówno do nowej grupy zasobów, należy wykonać czynności w dwóch krokach. Na przykład:

* **sieci Web a** znajduje się w **grupy sieci web**
* **Plan a** znajduje się w **planu grupy**
* Ma **sieci web a** i **planu a** do znajdują się w **połączeniu grupy**

Aby zrobić to przeniesienie, należy wykonać dwie operacje przenoszenia oddzielne w następującej kolejności:

1. Przenieś **sieci web a** do **planu grupy**
2. Przenieś **sieci web a** i **planu a** do **łączyć grupy**.

Certyfikat usługi aplikacji można przenieść do nowej grupy zasobów lub subskrypcji, bez żadnych problemów. Jednak jeśli aplikacja sieci web zawiera certyfikat SSL zakupionych zewnętrznie i przekazane do aplikacji, należy usunąć certyfikatu przed przeniesieniem aplikacji sieci web. Na przykład można wykonać następujące czynności:

1. Usuń przekazany certyfikat z aplikacji sieci web
2. Przenoszenie aplikacji sieci web
3. Przekaż certyfikat do aplikacji sieci web

## <a name="recovery-services-limitations"></a>Ograniczenia usługi odzyskiwania
Przenieś nie jest włączona dla magazynu, sieci lub używana do konfigurowania odzyskiwania po awarii z usługą Azure Site Recovery zasoby obliczeniowe.

Na przykład załóżmy, że skonfigurowano replikację maszyn lokalnych do konta magazynu (Storage1) i chcesz chronionej maszyny znaleziona po w tryb failover na platformie Azure jako maszynę wirtualną (VM1) dołączona do sieci wirtualnej (Network1). Nie można przenieść żadnego z tych zasobów Azure - Storage1 VM1 i Network1 - między grupami zasobów w ramach tej samej subskrypcji lub różnych subskrypcji.

## <a name="hdinsight-limitations"></a>Ograniczenia usługi HDInsight

Klastry usługi HDInsight można przenieść do nowej subskrypcji lub grupy zasobów. Jednak nie można przenieść w subskrypcjach zasoby sieciowe połączone z klastrem usługi HDInsight (na przykład sieci wirtualnej, karty Sieciowej lub usługi równoważenia obciążenia). Ponadto nie można przenieść do nowej grupy zasobów kart interfejsu Sieciowego, który jest dołączony do maszyny wirtualnej do klastra.

Podczas przenoszenia klastra usługi HDInsight na nową subskrypcję, należy najpierw przenieść innych zasobów (takich jak konta magazynu). Następnie przenieś klastra usługi HDInsight przez samego siebie.

## <a name="classic-deployment-limitations"></a>Wdrożenie klasyczne ograniczenia
Opcje przenoszenia zasobów wdrażać przy użyciu modelu klasycznego różnią się w zależności od tego, czy są przenoszenia zasobów w ramach subskrypcji lub do nowej subskrypcji.

### <a name="same-subscription"></a>Tej samej subskrypcji
Przenoszenie zasobów między grupami zasobów w innej grupie zasobów w ramach tej samej subskrypcji, mają zastosowanie następujące ograniczenia:

* Nie można przenieść sieci wirtualnych (klasyczny).
* Maszyny wirtualne (klasyczne) muszą zostać przeniesione z usługą w chmurze.
* Usługi w chmurze tylko przeniesienia po przeniesieniu obejmuje wszystkie maszyny wirtualne.
* Usługi w chmurze tylko jeden mogą zostać przeniesione w czasie.
* Jednocześnie można przenosić tylko jedno konto magazynu (klasyczne).
* Nie można przenieść konta magazynu (klasyczne) w tej samej operacji z maszyny wirtualnej lub usługi w chmurze.

Aby przenieść zasoby klasyczne do nowej grupy zasobów w ramach tej samej subskrypcji, użyj operacji przenoszenia standardowe, za pomocą [portal](#use-portal), [programu Azure PowerShell](#use-powershell), [interfejsu wiersza polecenia Azure](#use-azure-cli), lub [interfejsu API REST](#use-rest-api). Możesz użyć tej samej operacji, ponieważ używane do przenoszenia zasoby usługi Resource Manager.

### <a name="new-subscription"></a>Nowa subskrypcja
Podczas przenoszenia zasobów na nową subskrypcję, obowiązują następujące ograniczenia:

* Wszystkie zasoby klasyczne w subskrypcji muszą zostać przeniesione w tej samej operacji.
* Subskrypcja docelowa nie może zawierać inne zasoby klasyczne.
* Przeniesienie się żądać tylko wtedy za pomocą osobnych interfejsu API REST dla przenosi klasycznego. Standardowe polecenia move Menedżera zasobów nie działają podczas przenoszenia zasobów klasycznych na nową subskrypcję.

Aby przenieść zasoby klasyczne do nowej subskrypcji, użyj operacji REST, które są specyficzne dla zasobów klasycznych. Aby używać REST, wykonaj następujące czynności:

1. Sprawdź, czy subskrypcja źródłowa mogą uczestniczyć w przeniesienia między subskrypcjami. Użyj następujących operacji:

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     W treści żądania obejmują:

  ```json
  {
    "role": "source"
  }
  ```

     Odpowiedź dla operacji sprawdzania poprawności jest w następującym formacie:

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. Sprawdź, czy subskrypcji docelowej mogą uczestniczyć w przeniesienia między subskrypcjami. Użyj następujących operacji:

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     W treści żądania obejmują:

  ```json
  {
    "role": "target"
  }
  ```

     Odpowiedź jest w tym samym formacie co sprawdzania poprawności subskrypcji źródłowej.
3. Jeśli obie subskrypcje przeszedł sprawdzania poprawności, Przenieś wszystkie zasoby klasyczne z jedną subskrypcję, do innej subskrypcji z następujących operacji:

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    W treści żądania obejmują:

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

Operacja może trwać kilka minut.

## <a name="use-portal"></a>Korzystanie z portalu
Instrukcję przenoszenia zasobów, wybierz grupę zasobów, zawierające te zasoby, a następnie wybierz **Przenieś** przycisku.

![Przenoszenie zasobów](./media/resource-group-move-resources/select-move.png)

Określ, czy przenosisz zasobów do nowej grupy zasobów lub nową subskrypcję.

Wybierz zasoby do przeniesienia i docelowej grupy zasobów. Potwierdzić, że trzeba zaktualizować skrypty dla tych zasobów i wybierz **OK**. Jeśli w poprzednim kroku zostało wybrane ikonę Edytuj subskrypcję, musisz wybrać subskrypcji docelowej.

![Wybierz miejsce docelowe](./media/resource-group-move-resources/select-destination.png)

W **powiadomienia**, zobaczysz, że działa operacji przenoszenia.

![Pokaż stan przenoszenia](./media/resource-group-move-resources/show-status.png)

Po ukończeniu, użytkownik jest powiadamiany o wynik.

![Pokaż Przenieś wyników](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a>Korzystanie z programu PowerShell
Aby przenieść istniejące zasoby do innej grupy zasobów lub subskrypcji, należy użyć `Move-AzureRmResource` polecenia.

Pierwszym przykładzie pokazano, jak można przenieść jeden zasób do nowej grupy zasobów.

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

Drugi przykład przedstawia sposób przenoszenia wielu zasobów do nowej grupy zasobów.

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

Aby przejść do nowej subskrypcji, zawierają wartość `DestinationSubscriptionId` parametru.

Zostanie wyświetlona prośba o potwierdzenie, że chcesz przenieść określonych zasobów.

```powershell
Confirm
Are you sure you want to move these resources to the resource group
'/subscriptions/{guid}/resourceGroups/newRG' the resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a>Użyj interfejsu wiersza polecenia platformy Azure 2.0
Aby przenieść istniejące zasoby do innej grupy zasobów lub subskrypcji, należy użyć `az resource move` polecenia. Podaj identyfikatorów zasobów przenoszenia zasobów. Można pobrać identyfikatorów zasobów za pomocą następującego polecenia:

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

Poniższy przykład przedstawia sposób przenoszenia konta magazynu do nowej grupy zasobów. W `--ids` parametru, podaj rozdzieloną spacjami listę identyfikatorów przenoszenia zasobów.

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

Aby przejść do nowej subskrypcji, należy podać `--destination-subscription-id` parametru.

## <a name="use-azure-cli-10"></a>Użyj interfejsu wiersza polecenia platformy Azure 1.0
Aby przenieść istniejące zasoby do innej grupy zasobów lub subskrypcji, należy użyć `azure resource move` polecenia. Podaj identyfikatorów zasobów przenoszenia zasobów. Można pobrać identyfikatorów zasobów za pomocą następującego polecenia:

```azurecli
azure resource list -g sourceGroup --json
```

Polecenie to zwraca następujący format:

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

Poniższy przykład przedstawia sposób przenoszenia konta magazynu do nowej grupy zasobów. W `-i` parametru zawierają rozdzielaną przecinkami listę identyfikatorów przenoszenia zasobów.

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

Zostanie wyświetlona prośba o potwierdzenie, że chcesz przenieść określonego zasobu.

## <a name="use-rest-api"></a>Używanie interfejsu API REST
Aby przenieść istniejące zasoby do innej grupy zasobów lub subskrypcji, uruchom polecenie:

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

W treści żądania Określ docelowa grupa zasobów i zasobów, aby przenieść. Aby uzyskać więcej informacji na temat operacji REST przenoszenia zobacz [przenoszenia zasobów](https://msdn.microsoft.com/library/azure/mt218710.aspx).

## <a name="next-steps"></a>Następne kroki
* Aby dowiedzieć się więcej na temat poleceń cmdlet programu PowerShell do zarządzania subskrypcją, zobacz [przy użyciu programu Azure PowerShell z usługą Resource Manager](powershell-azure-resource-manager.md).
* Informacje na temat polecenia wiersza polecenia platformy Azure do zarządzania subskrypcją, zobacz [przy użyciu wiersza polecenia platformy Azure z usługą Resource Manager](xplat-cli-azure-resource-manager.md).
* Aby dowiedzieć się więcej o funkcjach portalu do zarządzania subskrypcją, zobacz [przy użyciu portalu Azure do zarządzania zasobami](resource-group-portal.md).
* Informacje na temat stosowania logiczna organizacji do zasobów, zobacz [przy użyciu tagów do organizowania zasobów](resource-group-using-tags.md).
