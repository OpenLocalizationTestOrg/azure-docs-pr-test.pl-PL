---
title: "aaaOverview dzienników diagnostycznych platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, co to są dzienników diagnostycznych platformy Azure i używania ich toounderstand zdarzeń występujących w ramach zasobów platformy Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: e38991c540626b4bb5b5b9a995276881ee58f368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a>Zbierania i wykorzystywania danych dziennika z zasobów platformy Azure

## <a name="what-are-azure-resource-diagnostic-logs"></a>Co to są dzienniki diagnostyczne zasobów platformy Azure
**Azure dzienników diagnostycznych poziom zasobów** są dzienniki emitowane przez zasób, które zawierają rozbudowane, często dane dotyczące operacji hello tego zasobu. zawartość Hello te dzienniki zależy od typu zasobu. Na przykład liczników reguły grupy zabezpieczeń sieci i usługi Key Vault inspekcje są dwie kategorie dzienników zasobów.

Dzienniki diagnostyczne poziom zasobów różnią się od hello [dziennik aktywności](monitoring-overview-activity-logs.md). Witaj dziennik aktywności zapewnia wgląd w operacji hello, wykonywane na zasobów w ramach subskrypcji, za pomocą Menedżera zasobów, na przykład tworzenia maszyny wirtualnej lub usuwanie aplikacji logiki. Dziennik aktywności Hello jest dziennika poziomu subskrypcji. Dzienniki diagnostyczne poziom zasobów zapewniają wgląd w operacji wykonanych w ramach tego zasobu, na przykład pobierania klucza tajnego z magazynu kluczy.

Dzienniki diagnostyczne poziom zasobów również różnią się od dzienników diagnostycznych na poziomie systemu operacyjnego gościa. Dzienniki diagnostyczne systemu operacyjnego gościa znajdują się te zebranych przez agenta, które działają w ramach maszyny wirtualnej lub inne obsługiwane typu zasobu. Poziom zasobów dzienników diagnostycznych wymagają żadne dane specyficzne dla zasobów agenta do przechwycenia z hello platformy Azure, podczas dzienników diagnostycznych na poziomie systemu operacyjnego gościa przechwycenia danych z systemu operacyjnego hello i aplikacje działające na maszynie wirtualnej.

Nie wszystkie zasoby obsługuje hello nowego typu zasobu dzienników diagnostycznych opisanych tutaj. Ten artykuł zawiera listę sekcji typów zasobów, które obsługują nowe dzienniki diagnostyczne hello poziom zasobów.

![Diagnostyka zasobów rejestruje vs innych typów dzienników ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a>Co należy zrobić z dzienników diagnostycznych poziom zasobów
Poniżej podano niektóre czynności hello, które można wykonać za pomocą dzienników diagnostycznych zasobu:

![Logiczne umieszczania dzienników diagnostycznych zasobu](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* Zapisz je tooa [ **konta magazynu** ](monitoring-archive-diagnostic-logs.md) inspekcji inspekcji lub ręcznie. Można określić za pomocą czasu (w dniach) przechowywania hello **ustawień diagnostycznych zasobu**.
* [Strumienia ich zbyt**usługi Event Hubs** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) dla wprowadzanie przez usługi innej firmy lub rozwiązania analizy niestandardowych, takich jak usługi Power BI.
* Analizuj je za pomocą [OMS analizy dzienników](../log-analytics/log-analytics-azure-storage.md)

Możesz użyć konta magazynu lub przestrzeni nazw usługi Event Hubs, która nie znajduje się w tej samej subskrypcji Witaj, zgodnie z jedną emitowanie dzienniki hello. Witaj, użytkownik konfiguruje ustawienie hello musi mieć hello odpowiednie RBAC dostępu tooboth subskrypcji.

## <a name="resource-diagnostic-settings"></a>Ustawienia diagnostyczne zasobu
Dzienniki diagnostyczne zasobu z systemem innym niż — obliczeń się, że zasoby są skonfigurowane przy użyciu ustawień diagnostycznych zasobu. **Ustawienia diagnostyczne zasobu** formantów zasobów:

* W przypadku dzienników diagnostycznych zasobu i metryki wysyłania (konto magazynu, centra zdarzeń i/lub analizy dzienników OMS).
* Kategorie dziennika, które są wysyłane i czy dane są także wysyłane.
* Jak długo każdej kategorii dziennika powinny zostać zachowane na koncie magazynu
    - Przechowywanie 0 oznacza, że dzienniki są przechowywane w nieskończoność. W przeciwnym razie wartość hello może być dowolną liczbę dni od 1 do 2147483647.
    - Jeśli zasady przechowywania są skonfigurowane, ale przechowywanie dzienniki na koncie magazynu jest wyłączone (na przykład, jeśli tylko opcje usługi Event Hubs lub OMS są zaznaczone), zasad przechowywania hello nie obowiązują.
    - Zasady przechowywania są stosowane na dzień, więc na powitania koniec dnia (UTC), rejestruje od dnia hello, która jest teraz poza zasady przechowywania hello są usuwane. Na przykład jeśli masz zasady przechowywania jeden dzień początku hello dzisiaj dzień hello hello dzienniki hello dzień przed wczoraj zostaną usunięte.

Te ustawienia można łatwo skonfigurować za pomocą hello ustawień diagnostycznych dla zasobu w hello portalu Azure, za pomocą poleceń programu PowerShell systemu Azure i interfejsu wiersza polecenia lub za pośrednictwem hello [interfejsu API REST Monitor Azure](https://msdn.microsoft.com/library/azure/dn931943.aspx).

> [!WARNING]
> Dzienniki diagnostyczne i metryki z warstwy systemu operacyjnego gościa hello użycia zasobów (na przykład maszyny wirtualne lub sieci szkieletowej usług) obliczeń [odrębny mechanizm konfiguracji i wybór wyjścia](../azure-diagnostics.md).
>
>

## <a name="how-tooenable-collection-of-resource-diagnostic-logs"></a>Jak tooenable zbierania dzienników diagnostycznych zasobu
Można włączyć zbierania dzienników diagnostycznych zasobu [podczas tworzenia zasobu w szablonie usługi Resource Manager](./monitoring-enable-diagnostic-logs-using-template.md) lub po utworzeniu zasobu ze strony tego zasobu w portalu hello. Można również włączyć kolekcji w dowolnym momencie za pomocą poleceń programu Azure PowerShell lub interfejsu wiersza polecenia lub hello interfejsu API REST Monitor Azure.

> [!TIP]
> Te instrukcje mogą nie dotyczyć bezpośrednio tooevery zasobów. Zobacz linki schematu hello u dołu tej strony toounderstand specjalne kroki, które mogą być zastosowane toocertain typów zasobów hello.
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-hello-portal"></a>Włącz zbieranie dzienników diagnostycznych zasobu w portalu hello
Możesz włączyć zbierania dzienników diagnostycznych zasobu w hello Azure portalu po utworzeniu zasobu przez przechodzi do określonego zasobu tooa lub przechodząc tooAzure monitora. tooenable za pomocą monitora Azure:

1. W hello [portalu Azure](http://portal.azure.com), przejdź tooAzure monitora i kliknij na **ustawień diagnostycznych**

    ![Monitorowanie sekcji Azure Monitor](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. Opcjonalnie Filtruj listę hello według grupy zasobów lub typ zasobu, a następnie kliknij na powitania zasobu, dla którego chcesz tooset ustawienie diagnostyczne.

3. Jeśli nie istnieją żadne ustawienia na powitania zasobów, wybrana przez Ciebie, jesteś toocreate zostanie wyświetlony monit o ustawienie. Kliknij pozycję "Włącz diagnostykę."

   ![Dodaj ustawienie diagnostyczne - żadnych istniejących ustawień](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   W przypadku ustawienia istniejące na powitania zasobów, zostanie wyświetlona lista ustawień już skonfigurowana dla tego zasobu. Kliknij przycisk "Dodaj ustawienie diagnostyczne".

   ![Dodaj ustawienie diagnostyczne — istniejące ustawienia](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. Nadaj nazwę ustawienie, hello pola wyboru, dla każdego toowhich docelowego chcesz toosend danych i skonfiguruj zasobów jest używana dla każdej lokalizacji docelowej. Opcjonalnie ustawić liczbę dni tooretain tych dzienników przy użyciu hello **przechowywania (dni)** suwaki (tylko toohello odpowiednie konta miejscem docelowym magazynu). Przechowywanie zero dni przechowuje dzienniki hello nieskończoność.
   
   ![Dodaj ustawienie diagnostyczne — istniejące ustawienia](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. Kliknij pozycję **Zapisz**.

Po kilku chwilach hello nowe ustawienie jest wyświetlane na liście ustawień dla tego zasobu i dzienników diagnostycznych są wysyłane toohello określonych miejsc docelowych zaraz po wygenerowaniu nowych danych zdarzenia.

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a>Włącz zbieranie dzienników diagnostycznych zasobów za pomocą programu PowerShell
Kolekcja tooenable dzienników diagnostycznych zasobów za pomocą programu Azure PowerShell hello Użyj następującego polecenia:

Magazyn tooenable dzienników diagnostycznych na koncie magazynu, użyj tego polecenia:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

Witaj magazynu, który jest identyfikator konta hello identyfikator zasobu dla toowhich konta magazynu hello ma toosend hello dzienniki.

tooenable przesyłania strumieniowego dzienników diagnostycznych tooan Centrum zdarzeń, użyj tego polecenia:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

Identyfikator reguły magistrali usługi Hello jest ciągiem o następującym formacie: `{Service Bus resource ID}/authorizationrules/{key name}`.

tooenable wysyłania dzienników diagnostycznych obszaru roboczego analizy dzienników tooa, użyj tego polecenia:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
```

Można uzyskać Identyfikatora zasobu hello obszaru roboczego analizy dzienników przy użyciu hello następujące polecenie:

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

Tooenable te parametry można łączyć wiele opcji danych wyjściowych.

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a>Włącz zbieranie dzienników diagnostycznych zasobów za pomocą interfejsu wiersza polecenia
Kolekcja tooenable dzienników diagnostycznych zasobu za pośrednictwem hello Azure CLI hello Użyj następującego polecenia:

Magazyn tooenable dzienników diagnostycznych na koncie magazynu, użyj tego polecenia:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

Witaj magazynu, który jest identyfikator konta hello identyfikator zasobu dla toowhich konta magazynu hello ma toosend hello dzienniki.

tooenable przesyłania strumieniowego dzienników diagnostycznych tooan Centrum zdarzeń, użyj tego polecenia:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

Identyfikator reguły magistrali usługi Hello jest ciągiem o następującym formacie: `{Service Bus resource ID}/authorizationrules/{key name}`.

tooenable wysyłania dzienników diagnostycznych obszaru roboczego analizy dzienników tooa, użyj tego polecenia:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
```

Tooenable te parametry można łączyć wiele opcji danych wyjściowych.

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a>Włącz zbieranie dzienników diagnostycznych zasobów za pomocą interfejsu API REST
ustawienia diagnostyki toochange przy użyciu hello interfejsu API REST Monitor Azure, zobacz [tego dokumentu](https://msdn.microsoft.com/library/azure/dn931931.aspx).

## <a name="manage-resource-diagnostic-settings-in-hello-portal"></a>Zarządzanie ustawień diagnostycznych zasobu w portalu hello
Upewnij się, że wszystkie zasoby zostały skonfigurowane przy użyciu ustawień diagnostycznych. Przejdź za**Monitor** w hello portalu i Otwórz **ustawień diagnostycznych**.

![Diagnostycznych dzienników bloku w portalu hello](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

Konieczne może być tooclick sekcji Monitor hello toofind "Więcej usług".

W tym miejscu możesz wyświetlić i filtrować wszystkie zasoby, które obsługują toosee ustawień diagnostycznych, jeśli mają włączoną diagnostykę. Można również przejść do szczegółów toosee skonfigurowanie wielu ustawień do zasobu i sprawdzić, które konta magazynu, przestrzeni nazw usługi Event Hubs i/lub obszar roboczy analizy dzienników, które dane są przesyłane do.

![Wyniki diagnostyki dzienniki w portalu](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

Dodanie ustawienie diagnostyczne wywołuje hello ustawień diagnostycznych widoku, gdzie można włączyć, wyłączyć lub zmodyfikować ustawienia diagnostyczne dla hello wybrany zasobów.

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a>Obsługiwane usługi, kategorie i schematy do dzienników diagnostycznych zasobu
[Znajduje się w artykule](monitoring-diagnostic-logs-schema.md) pełną listę obsługiwanych usług i hello dziennika kategorii i schematy używane przez te usługi.

## <a name="next-steps"></a>Następne kroki

* [Zbyt strumienia dzienników diagnostycznych zasobu**centra zdarzeń**](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Zmień ustawienia diagnostyczne zasobu przy użyciu interfejsu API REST Monitor Azure hello](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [Analizowanie dzienników z usługi Azure storage z analizy dzienników](../log-analytics/log-analytics-azure-storage.md)
