---
title: "aaaAzure rozwiązania analizy SQL w Log Analytics | Dokumentacja firmy Microsoft"
description: "Hello rozwiązania analizy SQL Azure ułatwia zarządzanie bazami danych Azure SQL."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: b2712749-1ded-40c4-b211-abc51cc65171
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: fe228bb3cb3f9d578a84707c3917f02fbeb8a627
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a>Monitorowanie bazy danych SQL Azure przy użyciu analiza SQL Azure (wersja zapoznawcza) w analizy dzienników

![Symbol SQL Analytics Azure](./media/log-analytics-azure-sql/azure-sql-symbol.png)

Witaj rozwiązania analizy SQL Azure w Azure Log Analytics zbiera i wizualizuje ważne metryki wydajności usługi SQL Azure. Za pomocą hello metryki, które należy zebrać z rozwiązaniem hello, można utworzyć niestandardowe reguły monitorowania i alertów. Można monitorować bazy danych SQL Azure i metryki elastycznej puli w wielu subskrypcji platformy Azure i elastyczne pule i ich wizualizacji. rozwiązanie Hello ułatwia również problemy tooidentify w każdej warstwie stosu aplikacji.  Używa [diagnostyki Azure metryki](log-analytics-azure-storage.md) wraz z analizy dzienników widoków toopresent dane dotyczące wszystkich baz danych Azure SQL i pul elastycznych w jednym obszarze roboczym analizy dzienników.

Obecnie to rozwiązanie w wersji zapoznawczej obsługuje too150, 000 baz danych SQL Azure i 5000 SQL pule elastyczne według obszaru roboczego.

Witaj rozwiązania analizy SQL Azure, takich jak inne dostępne dla analizy dzienników pomaga monitorować i otrzymywanie powiadomień o kondycji hello zasobów platformy Azure — w takim przypadku baza danych SQL Azure. Baza danych SQL Azure Microsoft to usługa skalowalne relacyjnej bazy danych, która zapewnia znanych tooapplications możliwości programu SQL Server typu w hello chmury Azure. Log Analytics pomaga toocollect skorelowania i wizualizacji danych strukturalnych i bez struktury.

## <a name="connected-sources"></a>Połączone źródła

Witaj rozwiązania analizy SQL Azure nie używa agentów tooconnect toohello usługi analizy dzienników.

Witaj w poniższej tabeli opisano hello połączone źródeł, które są obsługiwane przez to rozwiązanie.

| Połączone źródło | Pomoc techniczna | Opis |
| --- | --- | --- |
| [Agenci dla systemu Windows](log-analytics-windows-agents.md) | Nie | Bezpośrednie agentów systemu Windows nie są używane przez rozwiązanie hello. |
| [Agenci dla systemu Linux](log-analytics-linux-agents.md) | Nie | Bezpośrednie agentów systemu Linux nie są używane przez rozwiązanie hello. |
| [Grupa zarządzania programu SCOM](log-analytics-om-agents.md) | Nie | Połączenie bezpośrednie z tooLog agenta programu SCOM hello Analytics nie jest używany przez rozwiązanie hello. |
| [Konto usługi Azure Storage](log-analytics-azure-storage.md) | Nie | Analizy dzienników nie odczytuje danych hello z konta magazynu. |
| [Diagnostyka Azure](log-analytics-azure-storage.md) | Tak | Azure metryki dane są wysyłane tooLog Analytics bezpośrednio przez platformę Azure. |

## <a name="prerequisites"></a>Wymagania wstępne

- Subskrypcja platformy Azure. Jeśli nie masz, możesz utworzyć jedną dla [wolnego](https://azure.microsoft.com/free/).
- Obszar roboczy analizy dzienników. Można użyć istniejącego, lub możesz [Utwórz nową](log-analytics-get-started.md) przed rozpoczęciem korzystania z tego rozwiązania.
- Włącz diagnostyki Azure dla baz danych Azure SQL i pule elastyczne i [je skonfigurować toosend ich tooLog danych Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).

## <a name="configuration"></a>Konfiguracja

Wykonaj następujące kroki tooadd hello analiza SQL Azure rozwiązania tooyour roboczym hello.

1. Dodaj obszar roboczy tooyour rozwiązania analizy SQL Azure hello z [witrynę Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) lub za pomocą hello procesu opisanego w temacie [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).
2. W portalu Azure hello, kliknij przycisk **nowy** (hello + symbol), następnie hello listy zasobów, wybierz **monitorowanie i zarządzanie**.  
    ![Monitorowanie i zarządzanie](./media/log-analytics-azure-sql/monitoring-management.png)
3. W hello **monitorowanie i zarządzanie** listy kliknij **zobaczyć wszystkie**.
4. W hello **zalecane** kliknij **więcej** , a następnie hello nowej listy, Znajdź **analiza SQL Azure (wersja zapoznawcza)** i wybierz go.  
    ![Rozwiązania analizy SQL Azure](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)
5. W hello **analiza SQL Azure (wersja zapoznawcza)** bloku, kliknij przycisk **Utwórz**.  
    ![Tworzenie](./media/log-analytics-azure-sql/portal-create.png)
6. W hello **Utwórz nowe rozwiązanie** bloku, wybierz hello roboczym mają tooadd hello rozwiązania tooand, następnie kliknij przycisk **Utwórz**.  
    ![Dodaj tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)


### <a name="tooconfigure-multiple-azure-subscriptions"></a>tooconfigure wiele subskrypcji platformy Azure

toosupport wiele subskrypcji, użyj skryptu programu PowerShell hello z [rejestrowania metryki zasobów Azure włączyć przy użyciu programu PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/). Podaj identyfikator zasobu obszaru roboczego hello jako parametr podczas wykonywania hello danych diagnostycznych toosend skryptu z zasobów w obszarze roboczym tooa jedną subskrypcją platformy Azure w innej subskrypcji platformy Azure.

**Przykład**

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-hello-solution"></a>Za pomocą rozwiązania hello

Po dodaniu obszar roboczy tooyour rozwiązania hello powitalne kafelka analiza SQL Azure jest dodawany tooyour obszaru roboczego i wygląda na to, w obszarze Przegląd. Kafelek Hello jest wyświetlana liczba hello baz danych Azure SQL i Azure SQL pule elastyczne, które rozwiązanie hello jest podłączony do.

![Kafelek SQL Analytics Azure](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a>Wyświetlanie danych analiz SQL Azure

Polecenie hello **analiza SQL Azure** nawigacyjnego Azure SQL Analytics hello tooopen kafelka. pulpit nawigacyjny Hello zawiera bloki hello określonych poniżej. Każdy blok zawiera listę zasobów too15 (subskrypcji, serwer puli elastycznej i bazy danych). Kliknij dowolny pulpit nawigacyjny hello tooopen zasobów powitania dla tego konkretnego zasobu. Elastycznej puli lub baza danych zawiera wykresy hello o metryki dla wybranego zasobu. Kliknij okno dialogowe wyszukiwania dziennika hello tooopen wykresu.

| Blok | Opis |
|---|---|
| Subskrypcje | Lista subskrypcji z liczbą połączonych serwerów, pule adresów i baz danych. |
| Serwery | Lista serwerów z liczbą pul połączonych i baz danych. |
| Pule elastyczne | Lista połączonych pul elastycznych z maksymalną GB i liczby jednostek eDTU w hello obserwowanych okresu. |
|Bazy danych | Listy baz danych połączonych z maksymalną GB i jednostek dtu w warstwie w hello obserwowanych okresu.|


### <a name="analyze-data-and-create-alerts"></a>Analizuj dane i tworzyć alerty

Można łatwo tworzyć alerty z danymi hello pochodzące z zasobów bazy danych SQL Azure. Poniżej przedstawiono kilka przydatne [wyszukiwania dziennika](log-analytics-log-searches.md) zapytań, które służy do tworzenia alertu:

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


*Wysoka DTU na bazę danych Azure SQL*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

*Wysoka jednostek DTU w puli elastycznej bazy danych Azure SQL*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

Te tooalert zapytań na podstawie alertu można użyć na określone progi dla bazy danych SQL Azure i elastyczne pule. alert dotyczący obszar roboczy OMS tooconfigure:

#### <a name="tooconfigure-an-alert-for-your-workspace"></a>tooconfigure alert dla obszaru roboczego

1. Przejdź toohello [portalu OMS](http://mms.microsoft.com/) i zaloguj się.
2. Otwórz obszar roboczy hello, skonfigurowanego dla hello rozwiązania.
3. Na stronie Przegląd powitania kliknij hello **analiza SQL Azure (wersja zapoznawcza)** kafelka.
4. Uruchom jedno z hello przykładowych zapytań.
5. W wyszukiwaniu dziennik, kliknij przycisk **alertu**.  
![Utwórz alert podczas wyszukiwania.](./media/log-analytics-azure-sql/create-alert01.png)
6. Na powitania **Dodaj regułę alertu** Ustaw odpowiednie właściwości hello a hello określone progi, które mają, a następnie kliknij przycisk **zapisać**.  
![Dodaj regułę alertów](./media/log-analytics-azure-sql/create-alert02.png)

### <a name="act-on-azure-sql-analytics-data"></a>Wpływ na dane analityczne SQL Azure

Na przykład jeden hello najbardziej przydatne zapytań, które można wykonywać jest użycie jednostek dtu w warstwie hello toocompare dla wszystkich pul elastycznych SQL Azure wszystkich subskrypcji platformy Azure. Jednostki przepływności bazy danych (DTU) zapewnia toodescribe sposób hello relatywną pojemność poziomu wydajności baz danych Basic, Standard i Premium i pul. Liczba jednostek Dtu są oparte na mieszanych pomiarach procesora CPU, pamięci, odczytuje i zapisuje. Jak zwiększyć liczbę jednostek Dtu, hello oferowane przez zwiększa poziom wydajności hello zasilania. Na przykład poziomu wydajności z 5 jednostkami Dtu ma pięć razy więcej mocy niż poziom wydajności z jednostek dtu w warstwie 1. Maksymalny limit przydziału jednostek DTU dotyczy tooeach serwerem i elastyczne puli.

Uruchamiając hello następującego zapytania wyszukiwania dziennika można łatwo stwierdzić, jeśli analizę lub ponad przy użyciu programu SQL Azure elastyczne pule.

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie hello powyżej zapytania spowoduje zmianę następujących toohello.
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

W hello poniższy przykład, widać, że jeden puli elastycznej ma wysokiego użycia bliskie 100% jednostek dtu w warstwie, podczas gdy inne mają bardzo mało użycia. Możesz przejrzeć dalsze tootroubleshoot potencjalnych najnowszych zmian w środowisku przy użyciu dzienników działanie usługi Azure.

![Wyniki wyszukiwania dziennika - wysokie użycie](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a>Zobacz też

- Użyj [dziennik wyszukiwania](log-analytics-log-searches.md) w tooview analizy dzienników szczegółowe danych Azure SQL.
- [Tworzenie własnych pulpity nawigacyjne](log-analytics-dashboards.md) przedstawiający danych Azure SQL.
- [Tworzenie alertów](log-analytics-alerts.md) po wystąpieniu określonych zdarzeń Azure SQL.
